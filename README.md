# EXPERIMENT 3: Simulation of All Flip-Flops using Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **blocking assignment (`=`)** inside the `always` block.  
Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps
module SRflipflop(S,R,clk,reset,q);
input S,R,clk,reset;
output reg q;
always @ (posedge clk)
begin
if (reset==1)
q=0;
else 
begin 
case({S,R})

2'b00:q=q;
2'b01:q=1'b0;
2'b10:q=1'b1;
2'b00:q=1'bx;
endcase
end
end
endmodule
```
### SR Flip-Flop Test bench 
```verilog
module tb_srff;
  reg S, R, clk, reset;
  wire Q;

  SRflipflop UUT (S, R, clk, reset, Q);

  always #5 clk = ~clk;

  initial begin
    clk = 0; S = 0; R = 0; reset = 1;

    #10 reset = 0;
    #10 S = 1; R = 0;
    #10 S = 0; R = 0;
    #10 S = 0; R = 1;
    #10 S = 1; R = 1;
    #10 S = 0; R = 0;

    #20 $finish;
  end
endmodule


```
#### SIMULATION OUTPUT

<img width="1919" height="1196" alt="image" src="https://github.com/user-attachments/assets/97692bc9-1551-4846-95a6-0d52e134fba6" />

---

### JK Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps
module JKflipflop(J, K, clk, reset, q);
input J, K, clk, reset;
output reg q;
always @ (posedge clk) begin
if (reset == 1)
q=0;   
else begin
case ({J, K})
2'b00: q = q;     
2'b01: q = 1'b0;  
2'b10: q = 1'b1;  
2'b11: q = ~q;    
endcase
end
end
endmodule
```
### JK Flip-Flop Test bench 
```verilog
module tb_jkff;
reg J, K, clk, reset;
wire Q;
JKflipflop uut (J, K, clk, reset, Q);
always #5 clk = ~clk;
initial begin
clk = 0; J = 0; K = 0; reset = 1;

#10 reset = 0;
#10 J = 1; K = 0;   
#10 J = 0; K = 1;   
#10 J = 1; K = 1;   
#10 J = 0; K = 0;   
#10 J = 1; K = 1;   
#20 $finish;
end
endmodule


```
#### SIMULATION OUTPUT

<img width="1917" height="1199" alt="image" src="https://github.com/user-attachments/assets/d5f2993c-9682-4cd2-9588-76c189091c4e" />

---
### D Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps

module Dflipflop(D, clk, reset, Q);
input D, clk, reset;
output reg Q;

always @ (posedge clk) begin
if (reset == 1)
Q = 0;        
else
Q = D;        
end
endmodule
```
### D Flip-Flop Test bench 
```verilog
module tb_dff;
reg D, clk, reset;
wire Q;
Dflipflop UUT (D, clk, reset, Q);
  always #5 clk = ~clk;

initial begin
clk = 0; D = 0; reset = 1;
#10 reset = 0;
#10 D = 1;   
#10 D = 0;   
#10 D = 1;   
#10 D = 1;   
#10 D = 0;   
#10 D = 1;   

#20 $finish;
end
endmodule



```

#### SIMULATION OUTPUT

<img width="1916" height="1199" alt="image" src="https://github.com/user-attachments/assets/30494b94-ef77-40d2-9eec-a948f37a348e" />

---
### T Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps
module Tflipflop(T, clk, reset, Q);
  input T, clk, reset;
  output reg Q;
  always @ (posedge clk) begin
    if (reset == 1)
      Q = 0;          
    else if (T == 1)
      Q = ~Q;         
    else
      Q = Q;          
  end
endmodule
```
### T Flip-Flop Test bench 
```verilog
module tb_tff;
  reg T, clk, reset;
  wire Q;
  Tflipflop UUT (T, clk, reset, Q);
  always #5 clk = ~clk;

  initial begin
    
    clk = 0; T = 0; reset = 1;
    #10 reset = 0;
    #10 T = 1;   
    #20 T = 0;   
    #20 T = 1;   
    #20 T = 0;  

    #20 $finish;
  end
endmodule


```

#### SIMULATION OUTPUT

<img width="1919" height="1199" alt="image" src="https://github.com/user-attachments/assets/f023acd5-be6e-4229-8d44-f63ea6296745" />


---

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
