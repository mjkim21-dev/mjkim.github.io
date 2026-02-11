---
title: Module's Selected Major Components
---

## Module's Selected Major Components

The following sections are the selected major components necessary for  .....

### Power Management

(**remove this note/placeholder**: this is where your 3.3 volt switching regulator, any other needed power regulator, and power source {if applicable} **THAT WERE SELECTED**)

For more details, review the ["Appendix - Component Selection Process - Power Management"](https://embedded-systems-design.github.io/EGR314DataSheetTemplate/Appendix/01-Componet-Selection/Component-Selection-Process/#power-management) selection.


## Major Component Selection

**External Clock Module**

1. XC1259TR-ND surface mount crystal

    ![replace this](.png)

    * $1/each
    * [link to product](http://www.digikey.com/product-detail/en/ECS-40.3-S-5PX-TR/XC1259TR-ND/827366)

    | Pros                                      | Cons                                                             |
    | ----------------------------------------- | ---------------------------------------------------------------- |
    | Inexpensive                               | Requires external components and support circuitry for interface |
    | Compatible with PSoC                      | Needs special PCB layout.                                        |
    | Meets surface mount constraint of project |

**Rationale:** A clock oscillator is easier ...

**External Clock Module 2**

2. XC1259TR-ND surface mount crystal

    ![replace this](.png)

    * $3/each
    * [link to product](http://www.digikey.com/product-detail/en/ECS-40.3-S-5PX-TR/XC1259TR-ND/827366)

    | Pros                                      | Cons                                                             |
    | ----------------------------------------- | ---------------------------------------------------------------- |
    | Inexpensive                               | Requires external components and support circuitry for interface |
    | Compatible with PSoC                      | Needs special PCB layout.                                        |
    | Meets surface mount constraint of project |

**Rationale:** A clock oscillator 2 is easier ...


## Microcontroller Selection
### My Contribution to the Team
For this subsytem, I am responsible for creating a bluetooth subssystem, my goal is to send and receive information to a host bluetooth.


### ESP32-S3-WROOM-1-N4 pinout
  ![PinOut](ESP-pin.png)


### Rationale to the ESP
The Esp was chosen because of its...

## Power Budget
