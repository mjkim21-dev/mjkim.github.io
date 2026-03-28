---
title: API WebPage
---

## Overview 
My communication for Subsystem A2 is a part of a buffer system with Subsystem A3 ([Neel](https://neelgarde.github.io/NeelGarde/)). We have a simple structure that allows information to be passed from the robot to the controller. In this case, I am responsible for the controller side of the communication. For this system, Neel and I are sharing a package containing uInt8; from then on, my code will have buffers to send to Subsystem A1 ([Isaac](https://isrysm52.github.io/EGR314_isrysm52.github.io/07-API/API/)). 

<h3>To Subsystem A1 (Isaac): Message Type 9 -- Bluetooth Error</h3>
<table>
<thead>
<tr>
<th></th>
<th>Byte 1</th>
<th>Byte 2</th>
<th>Byte 3</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Variable Name</strong></td>
<td><code>sender_id</code></td>
<td><code>receiver_id</code></td>
<td><code>message_type</code></td>
</tr>
<tr>
<td><strong>Variable Type</strong></td>
<td><code>char</code></td>
<td><code>char</code></td>
<td><code>uint8_t</code></td>
</tr>
<tr>
<td><strong>Value</strong></td>
<td>B or C</td>
<td>A</td>
<td>9</td>
</tr>
<tr>
<td><strong>Example</strong></td>
<td>C</td>
<td>A</td>
<td>9</td>
</tr>
</tbody>
</table>


<h3>To Subsystem A1 (Isaac): Message Type 10 -- BLE Relay (To Client)</h3>
<table>
<thead>
<tr>
<th></th>
<th>Byte 1</th>
<th>Byte 2</th>
<th>Byte 3</th>
<th>Byte 4</th>
<th>Byte 5</th>
<th>Byte 6</th>
<th>Byte 7</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Variable Name</strong></td>
<td><code>sender_id</code></td>
<td><code>receiver_id</code></td>
<td><code>message_type</code></td>
<td><code>relay_sender</code></td>
<td><code>relay_receiver</code></td>
<td><code>data_1</code></td>
<td><code>data_2</code></td>
</tr>
<tr>
<td><strong>Variable Type</strong></td>
<td><code>char</code></td>
<td><code>char</code></td>
<td><code>uint8_t</code></td>
<td><code>char</code></td>
<td><code>char</code></td>
<td><code>uint8_t</code></td>
<td><code>uint8_t</code></td>
</tr>
<tr>
<td><strong>Value</strong></td>
<td>B</td>
<td>A</td>
<td>10</td>
<td>A–J</td>
<td>A–J</td>
<td>0–255</td>
<td>0–255</td>
</tr>
<tr>
<td><strong>Example</strong></td>
<td>B</td>
<td>A</td>
<td>10</td>
<td>H</td>
<td>A</td>
<td>125</td>
<td>0</td>
</tr>
<tr>
<td><strong>Notes</strong></td>
<td colspan="7">Relayed message types include: 5 (Speed), 6 (Distance), 7 (Temperature), 12 (Role Call)</td>
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
<th>Byte 5</th>
<th>Byte 6</th>
<th>Byte 7</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Variable Name</strong></td>
<td><code>sender_id</code></td>
<td><code>receiver_id</code></td>
<td><code>message_type</code></td>
<td><code>relay_sender</code></td>
<td><code>relay_receiver</code></td>
<td><code>data_1</code></td>
<td><code>data_2</code></td>
</tr>
<tr>
<td><strong>Variable Type</strong></td>
<td><code>char</code></td>
<td><code>char</code></td>
<td><code>uint8_t</code></td>
<td><code>char</code></td>
<td><code>char</code></td>
<td><code>uint8_t</code></td>
<td><code>uint8_t</code></td>
</tr>
<tr>
<td><strong>Value</strong></td>
<td>B</td>
<td>C</td>
<td>10</td>
<td>A–J</td>
<td>A–J</td>
<td>0–255</td>
<td>0–255</td>
</tr>
<tr>
<td><strong>Example</strong></td>
<td>B</td>
<td>C</td>
<td>10</td>
<td>J</td>
<td>X</td>
<td>53</td>
<td>0</td>
</tr>
</tbody>
</table>


<h3>To Subsystem A3 (Neel): Message Type 11 -- BLE Heartbeat</h3>
<table>
<thead>
<tr>
<th></th>
<th>Byte 1</th>
<th>Byte 2</th>
<th>Byte 3</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Variable Name</strong></td>
<td><code>sender_id</code></td>
<td><code>receiver_id</code></td>
<td><code>message_type</code></td>
</tr>
<tr>
<td><strong>Variable Type</strong></td>
<td><code>char</code></td>
<td><code>char</code></td>
<td><code>uint8_t</code></td>
</tr>
<tr>
<td><strong>Value</strong></td>
<td>B</td>
<td>C</td>
<td>11</td>
</tr>
<tr>
<td><strong>Example</strong></td>
<td>B</td>
<td>C</td>
<td>11</td>
</tr>
</tbody>
</table>


<h3>Broadcast: Message Type 12 -- Role Call</h3>
<table>
<thead>
<tr>
<th></th>
<th>Byte 1</th>
<th>Byte 2</th>
<th>Byte 3</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Variable Name</strong></td>
<td><code>sender_id</code></td>
<td><code>receiver_id</code></td>
<td><code>message_type</code></td>
</tr>
<tr>
<td><strong>Variable Type</strong></td>
<td><code>char</code></td>
<td><code>char</code></td>
<td><code>uint8_t</code></td>
</tr>
<tr>
<td><strong>Value</strong></td>
<td>A–J</td>
<td>X (broadcast)</td>
<td>12</td>
</tr>
<tr>
<td><strong>Example</strong></td>
<td>A</td>
<td>X</td>
<td>12</td>
</tr>
</tbody>
</table>
