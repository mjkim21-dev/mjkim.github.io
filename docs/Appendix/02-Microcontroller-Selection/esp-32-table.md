## Microcontroller Selection

*Table 3: Microcontroller selection*

| **Solution**                      |        **Facts**                   |                            **Contribution**                        |
| ---------------------------------- | ----------------------------------| -------------------------------------------------------------------|
| ![replace this](Microcon.webp)<br>Final Choice.<br> ESP32-S3-WROOM-1-N4 <br>$5.06/each<br>[product link](https://www.digikey.com/en/products/detail/espressif-systems/ESP32-S3-WROOM-1-N4/16162639)       | \* Bluetooth, WiFi 802.11b/g/n, Bluetooth v5.0 Transceiver Module 2.4GHz PCB Trace Surface Mount <br>\* Meets surface mount constraint of subsystem A2     | \* For this subsystem, I am responsible for creating a Bluetooth subsystem. My goal is to send and receive information. Subsystem A2 is in charge of Bluetooth communication. We plan to use Bluetooth Low Energy (BLE) for this, and A3 will be the client on the controller side of the project.  |

### ESP32-S3-WROOM-1-N4 pinout

  ![PinOut](ESP-pin.png)


### Rationale for the ESP
The ESP32-S3-WROOM-1-N4 was chosen primarily because it supports native BLE communication and is available in a surface-mount module, satisfying the project requirement that all components be surface-mounted. The ESP32 provides sufficient processing power and peripherals for BLE client operation. Required pins for this project include 3.3V and GND.
