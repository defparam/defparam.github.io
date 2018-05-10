---
layout: post
title: "Hello World"
date: 2018-05-09
description: My introduction to the world. Come check it out. 
tags: 
 - FPGA
---

## Hello World

Welcome to this site! I suppose you are looking for a proper "Hello World" for FPGAs, huh? Well OKAY, let me try:

```verilog
module hello_world(
	input clk,
	input rstn,
	output reg led
);

reg [19:0] counter;

always @(posedge clk or negedge rstn) begin
	if (rstn) begin
		led <= 1'b1; // active low (turn off on reset)
		counter <= 20'b0;
	end else begin
		counter <= counter + 1; // adder
		if (&counter) led <= ~led; // invert when all 1's
	end
end

endmodule
```

Yup that's right, a blinking LED. Anyway so this site will contain a collection of random postingx having to do with various projectx and research I'll be conducting. So while you are waiting for more content check out my [About Me](/about.html) area.
