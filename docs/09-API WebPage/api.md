---
title: API WebPage
---

## Overview 
My communication for Subsystem A2 is a part of a buffer system with Subsystem A3 ([Neel](https://neelgarde.github.io/NeelGarde/)). We have a simple structure that allows information to be passed from the robot to the controller. In this case, I am responsible for the controller side of the communication. For this system, Neel and I are sharing a package containing uInt8; from then on, my code will have buffers to send to Subsystem A1 ([Isaac](https://isrysm52.github.io/EGR314_isrysm52.github.io/)). 

<h3> To Subsystem A1 (Isaac) : Message Type 9 -- Bluetooth Error </h3>

<table>
  <thead>
    <tr>
      <th></th>
      <th>Byte 1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Variable Name</strong></td>
      <td><code>message_type</code></td>
    </tr>
    <tr>
      <td><strong>Variable Type</strong></td>
      <td><code>uint8_t</code></td>
    </tr>
    <tr>
      <td><strong>Value</strong></td>
      <td>9</td>
    </tr>
    <tr>
      <td><strong>Example</strong></td>
      <td>9</td>
    </tr>
  </tbody>
</table>

<h3>To Subsystem A1 (Isaac): Message Type 10 -- BLE To Client (Relay)</h3>

<table>
  <thead>
    <tr>
      <th></th>
      <th>Byte 1</th>
      <th>Byte 2</th>
      <th>Byte 3</th>
      <th>Byte 4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Variable Name</strong></td>
      <td><code>message_type</code></td>
      <td><code>sender_id</code></td>
      <td><code>receiver_id</code></td>
      <td><code>data</code></td>
    </tr>
    <tr>
      <td><strong>Variable Type</strong></td>
      <td><code>uint8_t</code></td>
      <td><code>uint8_t</code></td>
      <td><code>uint8_t</code></td>
      <td><code>uint8_t</code></td>
    </tr>
    <tr>
      <td><strong>Value</strong></td>
      <td>10</td>
      <td>0–255</td>
      <td>0–255</td>
      <td>0–255</td>
    </tr>
    <tr>
      <td><strong>Example</strong></td>
      <td>10</td>
      <td>2</td>
      <td>1</td>
      <td>50</td>
    </tr>
  </tbody>
</table>

<h3>To Subsystem A3 (Neel): Message Type 10 -- BLE Tunnel</h3>

<table>
  <thead>
    <tr>
      <th></th>
      <th>Byte 1</th>
      <th>Byte 2</th>
      <th>Byte 3</th>
      <th>Byte 4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Variable Name</strong></td>
      <td><code>message_type</code></td>
      <td><code>sender_id</code></td>
      <td><code>receiver_id</code></td>
      <td><code>data</code></td>
    </tr>
    <tr>
      <td><strong>Variable Type</strong></td>
      <td><code>uint8_t</code></td>
      <td><code>uint8_t</code></td>
      <td><code>uint8_t</code></td>
      <td><code>uint8_t</code></td>
    </tr>
    <tr>
      <td><strong>Value</strong></td>
      <td>10</td>
      <td>0–255</td>
      <td>0–255</td>
      <td>0–255</td>
    </tr>
    <tr>
      <td><strong>Example</strong></td>
      <td>10</td>
      <td>2</td>
      <td>3</td>
      <td>120</td>
    </tr>
  </tbody>
</table>

<h3> To Subsystem A3 (Neel): Message Type 11 -- BLE Heartbeat </h3>

<table>
  <thead>
    <tr>
      <th></th>
      <th>Byte 1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Variable Name</strong></td>
      <td><code>message_type</code></td>
    </tr>
    <tr>
      <td><strong>Variable Type</strong></td>
      <td><code>uint8_t</code></td>
    </tr>
    <tr>
      <td><strong>Value</strong></td>
      <td>11</td>
    </tr>
    <tr>
      <td><strong>Example</strong></td>
      <td>11</td>
    </tr>
  </tbody>
</table>

<h3>Broadcast: Message Type 12 -- Roll Call</h3>

<table>
  <thead>
    <tr>
      <th></th>
      <th>Byte 1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Variable Name</strong></td>
      <td><code>message_type</code></td>
    </tr>
    <tr>
      <td><strong>Variable Type</strong></td>
      <td><code>uint8_t</code></td>
    </tr>
    <tr>
      <td><strong>Value</strong></td>
      <td>12</td>
    </tr>
    <tr>
      <td><strong>Example</strong></td>
      <td>12</td>
    </tr>
  </tbody>
</table>

