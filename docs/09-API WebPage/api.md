---
title: API WebPage
---

## Overview 
My communication for Subsystem A2 is apart of a buffer system with Subsystem A3 (Neel). We have a simple structure where we connect and allopw information to be passed from the robot and to the controller. In this case I am responsible for the controller side of the communication. 

<h3>Example: Message Type 64 -- Motor Speed Setpoint</h3>

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
      <td><code>message_type</code></td>
      <td><code>motor_id</code></td>
      <td><code>motor_speed</code></td>
    </tr>
    <tr>
      <td><strong>Variable Type</strong></td>
      <td><code>uint8_t</code></td>
      <td><code>uint8_t</code></td>
      <td><code>int8_t</code></td>
    </tr>
    <tr>
      <td><strong>Min Value</strong></td>
      <td>0</td>
      <td>1</td>
      <td>-100</td>
    </tr>
    <tr>
      <td><strong>Max Value</strong></td>
      <td>9</td>
      <td>5</td>
      <td>100</td>
    </tr>
    <tr>
      <td><strong>Example</strong></td>
      <td>1</td>
      <td>3</td>
      <td>-30</td>
    </tr>
  </tbody>
</table>
