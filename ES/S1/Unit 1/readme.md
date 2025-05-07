## What is Embedded System?

Embedded system is a computational system that is developed based on an `integration of both hardware and software` in order to perform a given task. 

It can be said as a dedicated computer system has been developed for some particular reason. But it is not our traditional computer system or general-purpose computers, these are the Embedded systems that may work independently or attached to a larger system to work on a few specific functions. These embedded systems can work without human intervention or with little human intervention. 

![embedded system image 1](image.png)

- Components of Embedded Systems

1. Hardware 
2. Software :

Application code

Operating system (optional, often RTOS)

Drivers and middleware

- drivers are software programs that act as intermediaries between the operating system (OS) and hardware devices.

3. Firmware

- Application of Embedded System

Home appliances

Transportation

Health care

Business sector & offices

Defense sector

Aerospace

Agricultural Sector

# Embedded processor

A Processor is a hardware that performs data input/output, processing, and storage functions for a computer system.

## Types of Embedded Processors

![alt text](<Screenshot 2025-03-01 at 12.34.09 PM.png>)

1. General Purpose Processors (GPPs) :

> General-Purpose Processors (GPPs) in embedded systems are often microprocessors (MPUs), but they can also be microcontrollers (MCUs).

![alt text](image-1.png)

### Features

- Instruction set: General purpose processors have a large and complex instruction set, which allows them to perform a wide range of tasks.
- Multi-core: Many general-purpose processors are multi-core, which means they have multiple processors on a single chip. This allows them to perform multiple tasks concurrently, improving performance.
- Clock speed: The clock speed of a processor determines how fast it can execute instructions. General-purpose processors typically have high clock speeds, which allows them to perform tasks quickly.
- Cache: General-purpose processors have one or more levels of cache, which is a small amount of high-speed memory that is used to store frequently accessed data. This helps to improve the performance of the processor.
- Compatibility: General-purpose processors are typically compatible with a wide range of operating systems and software applications.
- Virtualization: Many general-purpose processors support virtualization, which allows them to run multiple virtual machines on a single physical machine.
- Power consumption: General-purpose processors can have high power consumption, which can be a concern in devices where power is limited.

2. Application specific Instruction set processor (ASIP) : 

ASIP (Application-Specific Instruction-set Processor) is a type of processor designed with a customized instruction set tailored to meet the specific performance, power, and area requirements of a particular application or domain.

- MicroControllers :

A microcontroller (MCU) is a small computer on a single integrated circuit that is designed to control specific tasks within electronic systems. It combines the functions of a central processing unit (CPU), memory, and input/output interfaces, all on a single chip.

![alt text](<Screenshot 2025-03-01 at 1.15.06 PM.png>)

MP :    Only contains the CPU; requires external RAM, ROM, and I/O interfaces. eg: ARM Cortex-M. appl :  laptops.

MC :    Includes CPU, RAM, ROM (Flash), and I/O ports in a single chip. eg : Qualcomm Snapdragon, mc 8051.  appl : smart wearables.

![alt text](image-2.png)

- DSP (Digilal Signal Procesor)

![alt text](<Screenshot 2025-03-01 at 2.58.18 PM.png>)

![alt text](image-3.png)

**A single chip with multiple processors is referred a s System on chip (SOC)**

3. Single-Purpose Embedded Processor or ASIC

SPEP : It is hardwired for a specific function and cannot be reprogrammed for other tasks.

### GCD using SPP

![alt text](<Screenshot 2025-03-01 at 6.28.24 PM.png>)


## A Watchdog Timer (WDT) 
is a hardware or software timer used to monitor the operation of a system, specifically embedded systems. Its main purpose is to detect and recover from malfunctions or errors that could cause the system to freeze or become unresponsive.

How It Works:
- The watchdog timer starts counting when the system starts running.
- The system must reset or "kick" the timer at regular intervals to indicate that it is functioning properly.
- If the system fails to reset the watchdog timer within the predefined time limit (because of a system hang, freeze, or crash), the watchdog timer will trigger a reset of the system to recover from the malfunction.
- This helps ensure that the system continues to run smoothly and doesn’t remain in an error state for too long.


