# 4-BIT-RIPPLE-COUNTER
AIM:

To implement 4 Bit Ripple Counter using verilog and validating their functionality using their functional tables

SOFTWARE REQUIRED:

Quartus prime

THEORY

4 Bit Ripple Counter

A binary ripple counter consists of a series connection of complementing flip-flops (T or JK type), with the output of each flip-flop connected to the Clock Pulse input of the next higher-order flip-flop. The flip-flop holding the least significant bit receives the incoming count pulses. The diagram of a 4-bit binary ripple counter is shown in Fig. below.

image

In timing diagram Q0 is changing as soon as the negative edge of clock pulse is encountered, Q1 is changing when negative edge of Q0 is encountered(because Q0 is like clock pulse for second flip flop) and so on.

image

image

Procedure

/* write all the steps invloved */

PROGRAM
```
module Bit_Ripple(
    input clk,     // Clock input
    input reset,   // Reset input (active high)
    output [3:0] q // 4-bit output
);
    // Internal signals for flip-flops
    reg [3:0] q_int;

    // Assign internal register to output
    assign q = q_int;

    always @(posedge clk or posedge reset) begin
        if (reset) 
            q_int[0] <= 1'b0; // Reset the first bit to 0
        else 
            q_int[0] <= ~q_int[0]; // Toggle the first bit on clock edge
    end

    // Generate the other flip-flops based on the output of the previous one
    genvar i;
    generate
        for (i = 1; i < 4; i = i + 1) begin : ripple
            always @(posedge q_int[i-1] or posedge reset) begin
                if (reset) 
                    q_int[i] <= 1'b0; // Reset the bit to 0
                else 
                    q_int[i] <= ~q_int[i]; // Toggle the bit on clock edge of previous stage
            end
        end
    endgenerate
endmodule
```
/* Program for 4 Bit Ripple Counter and verify its truth table in quartus using Verilog programming.

Developed by: S.SUMAIYA RegisterNumber: 25016731

RTL LOGIC FOR 4 Bit Ripple Counter

TIMING DIGRAMS FOR 4 Bit Ripple Counter

RESULTS
