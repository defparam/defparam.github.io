---
layout: post
title: "Hello World for FPGA"
date: 2018-05-09
description: Hello world! Here is an LED in verilog. This activity is mostly a test post. But I hope you enjoy the writeup nonetheless.
tags: 
 - FPGA
---

# Hello World

Welcome to this site! As you can imagine this post was mainly to test out my first blog posting on reconfig.io, but I suppose you are looking for a proper "Hello World" for FPGAs, huh? Well Okay, let me try:


Let's assume an FPGA design where you have an input 100 MHz clock signal and a reset (active low signal). If we want to blink an LED once every millesecond-ish then how is that accomplished?

## Here is the design:

```verilog
module hello_world(
	input clk,
	input rstn,
	output reg led
);

reg [15:0] counter;

always @(posedge clk or negedge rstn) begin
	if (~rstn) begin
		led <= 1'b1; // active low (turn off on reset)
		counter <= 20'b0;
	end else begin
		counter <= counter + 1; // adder
		if (&counter) led <= ~led; // invert when all 1's, blink the LED!
	end
end

endmodule
```

## I/O:

* input *clk* - This clock is a 100 MHz clock. It will be used to clock our counter register.
* input *rstn* - The reset signal is active low, when the signal is '0' our counter will initialize back to 0.
* output reg *led* - This is our output LED signal. In verilog you can specify it as a "reg" type right in the port declaration. A "reg" type is a data type assumed to hold a value.

## Registers

As mentioned before the LED output of the port declaration is a register in its own right. However this design also declares another group of registers called *counter*. This counter register is 16 indivdual registers grouped together to hold a counter state.  

## Sequential Clocked Process

In our sequential clocked process is where everything comes together. First we have the two events that trigger this clocked process which is a rising edge of clk or a negative edge of rstn. This block is evaluated only on those events. Next is the conditional if statement checking the condition of the rstn signal. Since it is checked first it has a higher priority than all other stimulus. On FPGA this style of code is inferred as an asynchronous reset structure. When this occurs all control registers should be placed in a healthy default state. In the case of the code block above we set the led to 1 (off) and the counter register to 0.

Next is the else case of the condition when rstn is not active. The only other logical entry into this code block is when clk is going through a posedge event. In this block we have 2 things that occur. First we have our endless wrapping 16-bit plus 1 adder. Every clock cycle the value is counter is increased by 1. The next line of code is a interesting conditional to check if all bits of the counter register are set to 1. This would mean on the next clock cycle the counter register will wrap to 0. The **&counter** syntax is a way to describe a bitwise AND of all bits in the counter register. If all bits are 1 then the result of that operator will be 1. At that point led is assigned to the inverse of itself basically toggling it on or off every 2^16 clocks.

## Math
2^16 is 65536. If the clk is 100MHz then the counter increases by 1 every 1/100000000 seconds which means that led performs a toggle every 65536/100000000 seconds or 655 microseconds. If the LED toggles every 655 microseconds then its period of blink is once every 1.3 milleseconds.


Yup that's right, a blinking LED. Anyway, that was fun practice, so this site will contain a collection of random postings having to do with various projects and research on FPGA, Security and more. So while you are waiting for more content check out my [About Me](/about.html) area.
