# Exp-4-Mux-Demux
# Design and Verification of 2:1 Multiplexer and 1:2 Demultiplexer
## Aim
To design and verify a 2:1 Multiplexer and a 1:2 Demultiplexer using Verilog HDL.
## Theory / Synopsis
A 2:1 Multiplexer (MUX) selects one of two data inputs, A or B, and routes it to a single output Y based on the value of the select line S. A 1:2 Demultiplexer (DEMUX) performs the reverse operation: it routes a single data input D to one of two outputs, Y0 or Y1, based on the select line S.
Boolean Functions
### 2:1 Multiplexer:
•	Y = S'.A + S.B
### 1:2 Demultiplexer:
•	Y0 = S'.D
•	Y1 = S.D
## Files to be Created

<img width="575" height="65" alt="image" src="https://github.com/user-attachments/assets/04c2d90c-0b6b-4b35-b603-d0e10e1e4f00" />

## Design / RTL Program
```
module mux (
    input  wire A,      // input line 0
    input  wire B,      // input line 1
    input  wire S,      // select line
    output wire Y       // output
);
    assign Y = (~S & A) | (S & B);
endmodule
 
module demux (
    input  wire D,      // data input
    input  wire S,      // select line
    output wire Y0,     // output line 0
    output wire Y1      // output line 1
);
    assign Y0 = (~S) & D;
    assign Y1 = S & D;
endmodule
```
## **Testbench Program
```
module tb;
reg  A, B, S, D;
    wire Y;
    wire Y0, Y1;
 
    // Instantiate the 2:1 Multiplexer
    mux mux_uut (
        .A(A),
        .B(B),
        .S(S),
        .Y(Y)
    );
 
    // Instantiate the 1:2 Demultiplexer
    demux demux_uut (
        .D(D),
        .S(S),
        .Y0(Y0),
        .Y1(Y1)
    );
 
    initial begin
        // ---- VCD dump setup ----
        $dumpfile("mux_demux.vcd");   // name of the VCD file to be generated
        $dumpvars(0, tb);             // dump all signals in this testbench hierarchy
 
        // ---- Apply all input combinations ----
        $monitor("Time=%0t S=%b A=%b B=%b Y=%b | D=%b Y0=%b Y1=%b",
                  $time, S, A, B, Y, D, Y0, Y1);
 
        // MUX select = 0 -> Y should follow A
        S = 0; A = 0; B = 0; D = 0; #10;
        S = 0; A = 0; B = 1; D = 1; #10;
        S = 0; A = 1; B = 0; D = 1; #10;
        S = 0; A = 1; B = 1; D = 0; #10;
 
        // MUX select = 1 -> Y should follow B
        S = 1; A = 0; B = 0; D = 0; #10;
        S = 1; A = 0; B = 1; D = 1; #10;
        S = 1; A = 1; B = 0; D = 1; #10;
        S = 1; A = 1; B = 1; D = 0; #10;
 
        #10 $finish;
    end
endmodule
```
## Truth Table

<img width="625" height="206" alt="WhatsApp Image 2026-11-03 at 11 58 39 AM" src="https://github.com/user-attachments/assets/ae322fbd-a0f5-44d4-a906-75753ce5c6a4" />


## Simulation Procedure

STEP 1 – Open Terminal
Open a terminal in the experiment folder.

STEP 2 – Load Synopsys Environment
source /synopsys/start.sh

STEP 3 – Compile Using VCS
vcs mux_demux.v mux_demux_tb.v -full64
If compilation is successful, VCS generates the simulation executable:
simv

STEP 4 – Run Simulation
./simv
The terminal displays the input combinations and corresponding outputs Y, Y0, and Y1.
A VCD waveform file is also generated:
mux_demux.vcd

STEP 5 – Open DVE

dve -full64
Other option
dve -full64 &
A DVE environment will open.
DVE Waveform Verification
In DVE:
•	Open the testbench hierarchy.
•	Locate the signals:
o	A
o	B
o	S
o	Y
o	D
o	Y0
o	Y1
•	Add the signals to the waveform window.
•	Run/inspect the waveform.
•	Verify that Y = A whenever S = 0, and Y = B whenever S = 1.
•	Verify that Y0 = D and Y1 = 0 whenever S = 0, and Y1 = D and Y0 = 0 whenever S = 1.
•	Confirm that Y0 and Y1 are never both high at the same time, since only one output is active per select value.
The waveform should agree with the truth table.

## Expected Result

The 2:1 Multiplexer and 1:2 Demultiplexer were realized using Verilog HDL:

•	Y = S'.A + S.B
•	Y0 = S'.D, Y1 = S.D

The design was compiled and simulated using Synopsys VCS, and the functionality was verified using DVE waveform analysis, matching the expected truth table.

## Output
MUX:
<img width="1533" height="250" alt="WhatsApp Image 2026-11-06 at 8 28 22 AM" src="https://github.com/user-attachments/assets/6a6f297e-bc01-499d-9f0f-42202a605761" />

DEMUX:
<img width="1473" height="232" alt="WhatsApp Image 2026-11-04 at 8 12 20 AM" src="https://github.com/user-attachments/assets/3a10155f-384a-41f1-bd24-3b6b7d5d3d4e" />



## Result

Thus, the 2:1 Multiplexer and 1:2 Demultiplexer were designed, implemented using Verilog HDL, successfully simulated using Synopsys VCS, and verified using Synopsys DVE.



