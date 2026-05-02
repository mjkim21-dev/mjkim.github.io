---
title: Subsystem A2 Review and Reflection
---

## Review of Module's Success

Subsystem A2 successfully met its primary requirement of designing and manufacturing a reliable Bluetooth Low Energy (BLE) communication using the `aioble` library. So, overall, I would say I was successful in achieving the overall goal, as I was also able to connect over a hardwired connection to subsystem A1 and a Bluetooth connection to subsystem A3.

## Microcontroller/Module Startup Tips

- Verify your development environment early, including firmware, board definitions, and library compatibility.  
- If working in a large group, communicate early and often.
- Take your time when designing the schematic and PCB, make sure traces are the correct size and pinouts are correct. 
- Double-check pin configurations and hardware connections before assuming software faults.  
- Read library documentation carefully, especially for BLE libraries like `aioble`.  
- Test each subsystem independently before attempting integration and pairing.  
- Keep your code modular so components can be debugged efficiently.  
- Use version control frequently to preserve working configurations.  
- Allocate sufficient time for debugging and iteration.  

## Lessons Learned

One of the most important lessons learned from this project is the importance of design. I really felt that procrastinating and rushing through the schematic and PCB designs came back to haunt me. As a student, really allow yourself to handle criticism because in this early stage, when nothing has been manufactured, is where you want to take the most criticism and really understand your design process. 

Another key takeaway is that debugging embedded systems requires a large amount of patience. I caught myself multiple times getting angry at the world when my board shorted the fuse, or the power at the test points was not working. It's exactly like building a LEGO set, as in my experience, I have the directions in front of me, yet I still build a part of the set wrong. So take a deep breath and carry on when the mind is calm.

Lastly, time management also proved critical, as integration and debugging required more time than initially expected. This reinforced the importance of early testing and iterative development. Clear communication between subsystems is necessary to avoid integration conflicts. Additionally, writing clean and well-documented code improves maintainability and simplifies debugging. Overall, the project emphasized adaptability, persistence, and systematic problem-solving.

## Recommendations for Future Students

1. Develop a strong understanding of microcontrollers and communication protocols such as UART, I2C, SPI, and BLE before starting the project.  
2. Begin implementation early and focus on building a simple working prototype before adding complexity.  
3. Break the system into smaller subsystems and verify each independently before full integration.  
4. Use version control and maintain clear documentation throughout the project lifecycle.  
5. Plan for extensive debugging and testing time, especially during subsystem integration.  
