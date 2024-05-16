# VLSI-LAB-EXP-4
# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

# AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.

# APPARATUS REQUIRED:

Vivado 2023.1

# PROCEDURE:
1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.


**LOGIC DIAGRAM**

# SR FLIPFLOP
![324383228-4e11d72e-7401-4fa7-9e17-977a8e5c056a](https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/ea45bd0f-51fa-41c1-afdb-f4c88765d254)


# JK FLIPFLOP
![324383595-20ec58e1-ff7d-48ad-896f-325fd15b9978](https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/a64f2fc4-91ab-4ebc-a9e1-4128f10496b0)


# T FLIPFLOP
![324383825-f59a93a1-c4a1-4f0d-b8ec-59afae83aaba](https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/3b941f70-6059-4033-97ca-ef6717f97fd7)



# D FLIPFLOP
![324383952-061329ff-7ea8-4011-88a0-a346b84b7329](https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/737d66b1-c066-4c46-924d-e0bd6a04bf20)


# COUNTER
![324384065-48d8dfc6-1504-43fc-8178-4baca02ac055](https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/b55a4359-b58e-408d-8ef2-8ad399ef29fb)



# VERILOG CODE:

# D Flip Flop
```
module DFlipFlop (D, clk, reset, Q) ;
input D;
input clk;
input reset; 
output reg Q; 
always @ (posedge clk)
begin
    if(reset == 1'b1)
        Q <= 1'b0;
    else
        Q <= D;
end
endmodule
```
# JK Flip Flop
```
module JK_flipflop (q, q_bar, j,k, clk, reset);
  input j,k,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin
    if(!reset)        q <= 0;
    else 
  begin
      case({j,k})
        2'b00: q <= q;  
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1;
        2'b11: q <= ~q; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
# SR Flip Flop
```
module SR_flipflop (q, q_bar, s,r, clk, reset);
  input s,r,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin 
    if(!reset)        q <= 0;
    else 
  begin
      case({s,r})
        2'b00: q <= q;    
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1; 
        2'b11: q <= 1'bx; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
# T Flip Flop
```
module tff (t,clk, rstn,q);  
 input t,clk, rstn;
 output reg q;
  always @ (posedge clk) begin  
    if (!rstn)  
      q <= 0;  
    else  
        if (t)  
            q <= ~q;  
        else  
            q <= q;  
  end  
endmodule
```
# Ripple Carry Counter
```
module D_FF(q, d, clk, reset);
output q;
input d, clk, reset;
reg q;
always @(posedge reset or negedge clk)
if (reset)
q = 1'b0;
else
q = d;
endmodule
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q); 
endmodule
module ripple_carry_counter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tffo(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
```
# MOD 10 Counter
```
module counter(
input clk,rst,enable,
output reg [3:0]counter_output
);
always@ (posedge clk)
begin 
if( rst | counter_output==4'b1001)
counter_output <= 4'b0000;
else if(enable)
counter_output <= counter_output + 1;
else
counter_output <= 0;
end
endmodule
```
UP-DOWN COUNTER

VERILOG CODE:
```
module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
```

# OUTPUT WAVEFORM:

# D Flip Flop
![327071393-1594f4d7-8e42-43ca-9cc0-f8dbebdd367f](https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/a7dcde9d-e820-4859-b888-367c257c552d)

<img width="962" alt="327071413-656845cc-29e9-48d0-b2d7-d510d921ee6c" src="https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/88ab6e5c-8164-433d-bfd3-1e4f50d726ff">


# JK Flip Flop

![327071445-02ef104f-8e85-4ec2-a6ea-2b24dd40eabf](https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/155a20f0-7ceb-4001-8193-68b8336deb2b)

<img width="962" alt="327071467-7a065d7c-9898-4c7f-88d3-3357386ce2e0" src="https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/6c346845-3847-4d21-8572-2907977801f0">




# SR Flip Flop
![327071505-b2267d45-902d-4e3f-9569-e98b50cfee9f](https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/7eccf94f-4532-48f7-a2c9-752c8babe153)


<img width="962" alt="327071535-bea76a0e-4ef9-48b5-954a-c88ec757408a" src="https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/c0b18a44-ff9f-4682-b86f-7b3f16c1a7bc">


# T Flip Flop
![327071572-e37658b4-49e8-417f-afcb-03c3e1f20b39](https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/490d7253-a769-472b-8067-6001e4382e76)
<img width="962" alt="327071595-6d52d36b-f685-416e-85d6-7faad0c8aee3" src="https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/592c9a4e-8b85-4af9-986a-230665b5b072">



# MOD-10 Counter
<img width="962" alt="327071620-f3a3b9bc-9645-4ce1-91bf-65237fdd5b93" src="https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/34aba7c0-e42e-4a0f-9e7e-7e1fb2347a8f">
<img width="962" alt="327071657-01931e66-6c86-4542-86a8-100f296cd0e4" src="https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/441e0d7a-86a3-4ad3-bd3d-9d4f6e38ee82">



# Ripple Carry Counter
<img width="962" alt="327071685-21a39d4e-fd2d-43bb-955e-78c6781c53bd" src="https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/cc67e946-6988-4e48-9494-8d5c972668c3">
<img width="962" alt="327071711-f01225a9-b09b-4a7e-a9ae-b50cbe80c779" src="https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/bb6736d1-11d7-46fc-bda8-1285352f57ca">


# UP Down Counter

<img width="617" alt="327071740-3988b689-eaa0-4ef2-8a4d-c0c035f5c232" src="https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/2e3340e7-ca67-443c-b2ce-e5a7e61ab671">
<img width="962" alt="327071763-5dc92778-9179-41f6-b14d-37740f2cb1c8" src="https://github.com/madhan2206/VLSI-LAB-EXP-4/assets/170016170/4c8378e9-2e8c-4f7a-95ab-694aea85efb4">


# RESULT:
Hence thus given To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using vivado
