---
layout: page 
title: Projects
---

# Projects

This website is first and formost a place for me to describe my projects on [Github](https://github.com/defparam). Here is a list of some of the more popular projects:

* [21FX](https://github.com/defparam/21FX) - This is a PCB board + CPLD targeting the origion SNES console. This research was spun out of understanding the bottom expasion connector hardware on that console. From there I was able to produce a design to actively master the SNES CPU and interact with the ROM running on the cart.
* [pciworm](https://github.com/defparam/pciworm) - The project spun off of my desire to explore how to write a Windows 10 driver for an FPGA connected to host via PCIe. This alone serves as a beautiful example of a UMDF driver accessing FPGA address space and forwarding that interface to userland applications via IOCTLs.
* [higan-verilog](https://github.com/defparam/higan-verilog) - Emulators and HW simulators are evil twins accomplishing the same motivation, to model the hardware. This example shows a way to compile in a simulation engine (verilator) to an emulator target (higan SFC).
* [diagrams](https://github.com/defparam/diagrams) - As I continue forward with my research I'll document any confusing data structures in the form of an image. This repo is here to host these diagrams for everyone to use.
