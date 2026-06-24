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
**2h**

This module introduces **I**ndustrial **A**utomation **C**ontrol **S**ystems **IACS** and **PLCs**, explaining their role in controlling devices like conveyors and grippers with fixed cycle times. It covers **IEC 61131-2/9 standards** for hardware and communication interfaces, then explores major **fieldbuses**, e.g. EtherCAT, IO-Link, Modbus RTU, with their latency characteristics: EtherCAT offers sub-millisecond real-time performance, IO-Link provides $2–5 [ms]$ point-to-point communication for smart sensors, and Modbus RTU delivers simplicity at the cost of $10–100 [ms]$ latency. The choice of fieldbus significantly impacts integration time and project cost. Finally, PLCs are presented as modules executing cyclic code within larger systems that require real-time monitoring without the ability to pause execution.

## Module 02, [PLC programming quick start](./ADP_Module_02_PLC_QuickStart/README.md).
**4h**

The objective is to briefly present IEC 61131-3 PLC programming in order to understand how it differs from Python-type script programming and what the constraints are in terms of types and cycle time when you want to access data.

## Module 03, [Node-red, Flow Based Programming](./ADP_Module_03_Flow_Based_Programming/README.md).

**2h**

Node-RED is a flow-based, low-code development tool for visual programming. Some basics presented in this module.

## Module 04, [A Dashboard with Node-RED](./ADP_Module_04_User_Interface/README.md).

**4h**

Module 04 covers Node-RED Dashboard 2.0, a professional UI solution for building human-machine interfaces without extensive web development knowledge. The module introduces dashboard architecture, **pages, groups, widgets** and detailed documentation of key nodes including: *inputs, buttons, text, number, sliders*, and notifications. Dashboard 2.0 is actively maintained and suitable for real-world industrial applications, as demonstrated by professional-grade examples. The module emphasizes practical implementation with configuration options, icons from Material Design, and dynamic parameter usage for interactive dashboards.

## Module 05, [Connecting Node-RED to the automation system](./ADP_Module_05_Machine_Interface/README.md).

**4h**

This module covers machine interfaces and industrial communication protocols, focusing on how Node-RED connects to automation systems, **IACS**, through OPC-UA and DataLayer protocols. It explains data structure differences across programming languages: **IEC 61131-3, JavaScript, Python, JSON** and demonstrates practical operations: reading, writing, and subscribing to variables, as well as invoking PLC methods. The emphasis is on understanding secure client-server communication, data type mapping, and real-world implementation using the ctrlX Automation palette for reliable industrial automation integration.

## Module 06, [Node-RED Subflows](./ADP_Module_06_Sub_Flows/README.md)

**2h**
This module presents Node-RED fundamentals for  writing functions to process messages, managing variables across different scopes, **global**, **flow**, node, and environment, and creating reusable **subflows** to encapsulate and organize automation logic for production environments.

## Module 07, [File Management](https://github.com/hei-dls-adp/adp_lab_04_2026)

**4h**

Reading and writing on files with Node-RED. See : [Lab 04, Management of CSV and JSON files](https://github.com/hei-dls-adp/adp_lab_04_2026).

## Module 08, [Annex 11](https://github.com/hei-dls-adp/adp-docs/tree/main/ADP_Module_08_Annex_11)

**2h** Introduction to good manufacturing practices.

## Module 09, [Data Storage and Visualisation](https://github.com/hei-dls-adp/adp_lab_05_2026)

**4h**


## Module 10, Small project, URS + FS + DS

**4h**

Theory + workshop in the lab, see [adp_lab_06_2026, annex 11](https://github.com/hei-dls-adp/adp_lab_06_2026).

## Module 11, Small project, IQ, OQ, PQ

**4h**

Theory + workshop in the lab, see [adp_lab_06_2026, annex 11](https://github.com/hei-dls-adp/adp_lab_06_2026).

---

## List of Labs

  1. [Introduction to PLC](https://github.com/hei-dls-adp/adp_lab_01_2026)
  2. [Flow Based Programming](https://github.com/hei-dls-adp/adp_lab_02_2026)
  3. [Machine Interface](https://github.com/hei-dls-adp/adp_lab_03_2026)
  4. [Management of CSV and JSON files](https://github.com/hei-dls-adp/adp_lab_04_2026)
  5. [Data Storage and Visualisation](https://github.com/hei-dls-adp/adp_lab_05_2026)
  6. [Project management according & annex 11/GMP, 2 labs](https://github.com/hei-dls-adp/adp_lab_06_2026)

<!-- End of file -->
