<h1 align="left">
  <br>
  <img src="./img/hei-en.png" alt="HEI-Vs Logo" width="350">
  <br>
  Automation in Development and Production
  <br>
</h1>

Course : **DLS / ADP**


Author: [Cédric Lenoir](mailto:cedric.lenoir@hevs.ch)

---

# Started..

Courses for 2026: From February 20.


[A good document to start with Node-RED and its Flow Fuse Dashboard](/documentation/ebook_%20The%20Ultimate%20Beginner%20Guide%20to%20a%20Professional%20Node-RED-V!.pdf).

# List of Modules

## Module 01, [Introduction to industrial automation](./ADP_Module_01_Industrial_Automation/README.md). 
This module introduces **I**ndustrial **A**utomation **C**ontrol **S**ystems **IACS** and **PLCs**, explaining their role in controlling devices like conveyors and grippers with fixed cycle times. It covers **IEC 61131-2/9 standards** for hardware and communication interfaces, then explores major **fieldbuses**, e.g. EtherCAT, IO-Link, Modbus RTU, with their latency characteristics: EtherCAT offers sub-millisecond real-time performance, IO-Link provides $2–5 [ms]$ point-to-point communication for smart sensors, and Modbus RTU delivers simplicity at the cost of $10–100 [ms]$ latency. The choice of fieldbus significantly impacts integration time and project cost. Finally, PLCs are presented as modules executing cyclic code within larger systems that require real-time monitoring without the ability to pause execution.

## Module 02, [PLC programming quick start](./ADP_Module_02_PLC_QuickStart/README.md).
The objective is to briefly present IEC 61131-3 PLC programming in order to understand how it differs from Python-type script programming and what the constraints are in terms of types and cycle time when you want to access data.

## Module 03, [Node-red, Flow Based Programming](./ADP_Module_03_Flow_Based_Programming/README.md).
Node-RED is a flow-based, low-code development tool for visual programming. Some basics presented in this module.

## Module 04, [A Dashboard with Node-RED](./ADP_Module_04_User_Interface/README.md).
Module 04 covers Node-RED Dashboard 2.0, a professional UI solution for building human-machine interfaces without extensive web development knowledge. The module introduces dashboard architecture, **pages, groups, widgets** and detailed documentation of key nodes including: *inputs, buttons, text, number, sliders*, and notifications. Dashboard 2.0 is actively maintained and suitable for real-world industrial applications, as demonstrated by professional-grade examples. The module emphasizes practical implementation with configuration options, icons from Material Design, and dynamic parameter usage for interactive dashboards.

## Module 05, [Connecting Node-RED to the automation system](./ADP_Module_05_Machine_Interface/README.md).
This module covers machine interfaces and industrial communication protocols, focusing on how Node-RED connects to automation systems, **IACS**, through OPC-UA and DataLayer protocols. It explains data structure differences across programming languages: **IEC 61131-3, JavaScript, Python, JSON** and demonstrates practical operations: reading, writing, and subscribing to variables, as well as invoking PLC methods. The emphasis is on understanding secure client-server communication, data type mapping, and real-world implementation using the ctrlX Automation palette for reliable industrial automation integration.

---

# List of Labs
## Lab 01, [Modules 01 & 02, in practice](https://github.com/hei-dls-adp/adp-lab-01_2026).
*Prérequis: modules 01 et 02.*
This lab presents **practical examples** designed to demonstrate, on a small demonstration conveyor, some basic concepts of industrial or laboratory automation.



<!-- End of file -->
