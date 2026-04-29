---
title: Resources
---

## Overview
“Subsystem A2 is implemented using Bluetooth Low Energy (BLE) communication via the aioble library, which provides a GATT-based interface; this allows it to exchange data with Subsystem A3 (Neel) within the overall system architecture.” 

For how my code is structured, each protocol is implemented as its own async def task, and then at the bottom, there’s a central async def main() that calls all of them using asyncio.gather(). Because we’re using asyncio, we get cooperative concurrency, meaning each task runs until it hits an await, then the event loop switches to another task. This lets multiple parts of the system (BLE, UART, etc.) run responsively without blocking each other. Instead of using traditional blocking delays or writing interrupt-style logic, we rely on event-driven await calls and non-blocking sleeps to handle timing and communication.

To download files, [here](314_final.zip) is a zip file containing everything from the kiCAD files to the code used.

Below is the uploaded code in the main.py file. 
```c
import bluetooth
import asyncio
import aioble
from machine import Pin, UART
import time 

# --- CONFIGURATION ---
_BLE_SERVICE_UUID = bluetooth.UUID('8bbd8ff7-3d84-4e81-9d46-70b6cb79e76a')
_BLE_UPSTREAM_UUID = bluetooth.UUID('5699aead-41fc-4705-9c65-7c84d8bcb04c')
_BLE_DOWNSTREAM_UUID = bluetooth.UUID('a037a1df-ccaf-480c-b7a4-6526a6848887')
_BLE_ROLLCALL_UUID = bluetooth.UUID('d9cba376-e9c9-4db7-a6f2-4c6783c1dade')
A3_MAC = "00:70:07:84:DC:FA"

team_ids = ['A','B','C','D','E','F','G','H','I','J','X']
rollcall_msg_type = 'C'

current_connection = None
remote_downstream_char = None
remote_rollcall_char = None
uart_lock = asyncio.Lock()

# Pins & UART
led_conn = Pin(8, Pin.OUT)    # Red: Solid ON when connected
led_rx = Pin(36, Pin.OUT)     # Green: Flash on Activity
button = Pin(35, Pin.IN, Pin.PULL_UP)
uart = UART(1, baudrate=9600, tx=43, rx=44)

# Global variables
recByte = 0
bufferIndex = 0
endBytes = 0
Recieving = 0

# --- BLE SETUP ---
ble_service = aioble.Service(_BLE_SERVICE_UUID)
upstream_char = aioble.Characteristic(ble_service, _BLE_UPSTREAM_UUID, read=True, notify=True)
downstream_char = aioble.Characteristic(ble_service, _BLE_DOWNSTREAM_UUID, read=True, write=True, capture=True, notify=True)
rollcall_char = aioble.Characteristic(ble_service, _BLE_ROLLCALL_UUID, read=True, write=True, capture=True, notify=True)
aioble.register_services(ble_service)

# --- TASKS ---

async def flash_activity_led():
    led_rx.value(1)
    await asyncio.sleep(0.05)
    led_rx.value(0)

async def ble_downstream():
    print("[INFO] BLE Downstream Task: Status -> RUNNING")
    while True:
        try:
            write_event = await downstream_char.written()
            
            if write_event:
                connection, data = write_event
                print(f'[INFO] BLE_RX: Received {len(data)} bytes')
                print(f'[INFO] Content: {data}')
                
                asyncio.create_task(flash_activity_led())
                
                #Forward to UART
            else:
                print('[INFO] BLE_downstream: recieved message: ',msg)
                swriter = asyncio.StreamWriter(uart, {})
                swriter.write(msg)
                print('[INFO] UART_TX: sent message: ',msg)
                await swriter.drain()

        except Exception as e:
            print(f"[ERROR] Downstream Task Exception: {e}")
            await asyncio.sleep(1) 

async def button_task():  #testing purposes, to test without isaac 
    print("[INFO] Button Task: Monitoring Pin 35")
    last_state = 1
    
    while True:
        current_state = button.value()
        
        # Falling edge detection (Button Pressed)
        if last_state == 1 and current_state == 0:
            # 1. Define your mixed variables
            header = "AZ"          # String
            team_id = "B"          # String (Sender)
            receiver_id = "F"      # String (Receiver)
            msg_type = "D"           # A-Z (Will be cast to string by the f-string)
            command = ""        # String
            footer = "YB"          # String
            
            msg_str = f"{header}{team_id}{receiver_id}{msg_type}{command}{footer}"
            
            msg_uint8 = bytearray(msg_str, 'utf-8')

            try:
                #upstream_char.write(msg_uint8)
                
                if remote_downstream_char:    #sends to A3
                    await remote_downstream_char.write(msg_uint8)
                
                asyncio.create_task(flash_activity_led())
                print(f"[BUTTON] Sent message: {msg_str} (Length: {len(msg_uint8)})")
                
            except Exception as e:
                print(f"[BUTTON] BLE Transmission failed: {e}")
                
            await asyncio.sleep(0.3)
            
        last_state = current_state
        
        await asyncio.sleep(0.05)
        
async def uart_upstream():
    print("[INFO] UART Upstream task started")
    while True:
        if uart.any():
            raw_data = uart.read()
            
            if raw_data:
                filtered_data = uart_filter(raw_data)
                
                if filtered_data is not None:
                    try:
                        await remote_downstream_char.write(filtered_data)
                        asyncio.create_task(flash_activity_led())
                        print(f"[INFO] UART -> BLE: Sent {len(filtered_data)} bytes: ",filtered_data)
                    except Exception as e:
                        print(f"[ERROR] UART Upstream (BLE Push): {e}")
                        
        await asyncio.sleep(0.01)
        
def uart_filter(raw_msg):
    if len(raw_msg) >= 6:
        print('[INFO] UART_RX: valid message size')
        if raw_msg[0] == ord('A') and raw_msg[1] == ord('Z'):
            print('[INFO] UART_RX: valid start bytes recieved')
            if raw_msg[len(raw_msg) - 2] == ord('Y') and raw_msg[len(raw_msg) - 1] == ord('B'):
                print('[INFO] UART_RX: valid stop bytes recieved')
                if chr(raw_msg[2]) in team_ids:
                    print('[INFO] UART_RX: valid sender ID')
                    if raw_msg[2] == ord('C'):
                        print('[INFO] UART_RX: recieved message sent by self. Ignoring.')
                        return None
                    elif chr(raw_msg[3]) in team_ids:
                        print('[INFO] UART_RX: valid reciever ID')
                        return raw_msg
                    else:
                        print('[ERROR] UART_RX: invalid reciever ID')
                else:
                    print('[ERROR] UART_RX: invalid sender ID')
            else:
                print('[ERROR] UART_RX: failed to identify stop bytes')
        else:
            print('[ERROR] UART_RX: failed to identify start bytes')
    else:
        print('[ERROR] UART_RX: message size invalid')
    return None

async def trigger_rollcall_as_x():
    """Sends Rollcall"""
    if remote_downstream_char:
        try:
            await remote_downstream_char.write(b'X') 
            print("[ROLLCALL] sent to A3.")
        except Exception as e:
            print(f"[ROLLCALL] Failed: {e}")
    
    async with uart_lock: 
        uart.write(b'X')
    asyncio.create_task(flash_activity_led())

async def rollcall_handler():
    while True:
        res = await rollcall_char.written()
        if not res: 
            continue
        
        _, data = res
        
        if data and len(data) > 0:
            print(f"[ROLLCALL] Received: {data}")
            if data[0:1] == b'X': 
                print("[ROLLCALL] Peer responded with 'X'")
        else:
            print("[ROLLCALL] Received empty packet.")

async def trigger_rollcall():
    """Initiate a rollcall broadcast."""
    if remote_downstream_char:
        print("[ROLLCALL] Initiating broadcast...")
        await remote_downstream_char.write(b'?')

async def central_scanner():
    global remote_downstream_char, remote_rollcall_char
    while True:
        device = aioble.Device(aioble.ADDR_PUBLIC, A3_MAC)
        print("SCANNING: Searching for Subsystem A3...")
        try:
            conn = await device.connect(timeout_ms=5000)
            print("CONNECTED: Subsystem A3")
            led_conn.value(1)
            
            service = await conn.service(_BLE_SERVICE_UUID)
            remote_downstream_char = await service.characteristic(_BLE_DOWNSTREAM_UUID)
            remote_rollcall_char = await service.characteristic(_BLE_ROLLCALL_UUID)
            
            remote_upstream_char = await service.characteristic(_BLE_UPSTREAM_UUID)
            await remote_upstream_char.subscribe() 
            print("[INFO] Subscribed to A3 Upstream notifications")

            while conn.is_connected():
                data = await remote_upstream_char.notified()
                if data:
                    print(f"[A3 -> A2] Received: {data}")
                    asyncio.create_task(flash_activity_led())
                    
                    async with uart_lock:
                        uart.write(data)
                        
        except Exception as e:
            print(f"SCANNER: Connection/Subscription to A3 failed: {e}")
        finally:
            remote_downstream_char = None
            remote_rollcall_char = None 
            print("DISCONNECTED: Subsystem A3")
            if not current_connection: 
                led_conn.value(0)
        await asyncio.sleep(5)
        
async def peripheral_advertiser():
    global current_connection
    while True:
        print("ADVERTISING: Waiting for connection...")
        try:
            async with await aioble.advertise(250_000, name="Subsystem A2", services=[_BLE_SERVICE_UUID]) as connection:
                await asyncio.sleep(0.5)
                print("CONNECTED: Central device (Phone/Host)")
                current_connection = connection
                led_conn.value(1)
                await connection.disconnected()
                current_connection = None
                led_conn.value(0)
                print("DISCONNECTED: Central device")
        except Exception as e:
            print(f"ADV ERROR: {e}")
            await asyncio.sleep(1)

async def main():
    await asyncio.gather(
        peripheral_advertiser(), 
        central_scanner(), 
        uart_upstream(),
        ble_downstream(),
        rollcall_handler(),
        button_task()
    )

asyncio.run(main())

```
