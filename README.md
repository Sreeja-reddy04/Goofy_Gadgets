***HDLBits -->[Visit Problem sets](https://hdlbits.01xz.net/wiki/Problem_sets)***

# HDL Bits Solutions
## Problem sets
#### - Getting Started
#### - Verilog Language
   - Basics
   - Vectors
   - Modules:Hierarchy
   - Procedures
   - More Verilog Features
#### - Circuits
   - Combinational
   - Sequential 
## [Getting Started]
```bash
module top_module(output one);
  assign one=1;
endmodule
```
## [Output Zero]
```bash
module top_modulw(output zero);
  assign zero=0;
endmodule
```
## [simple wire]
```bash
module top_module( input in, output out );
assign out=in;
endmodule
```
## [Four wire]
```bash
module top_module( 
    input a,b,c,
    output w,x,y,z );
assign w=a,x=b,y=b,z=c;
endmodule
```
## [inverter]
```bash
module top_module( input in, output out );
assign out=~in;
endmodule
```
## [AND gate]
```bash
module top_module( 
    input a, 
    input b, 
    output out );
assign out=a&b;
endmodule
```
## [NOR gate]
```bash
module top_module( 
    input a, 
    input b, 
    output out );
    assign out=~(a|b);
endmodule
```
## [XNOR gate]
```bash
module top_module( 
    input a, 
    input b, 
    output out );
    assign out= ~(a^b);
endmodule
```
## [Declaring Wires]
```bash
`default_nettype none
module top_module(
    input a,
    input b,
    input c,
    input d,
    output out,
    output out_n   ); 
wire a1,a2,a3;
    assign a1=a&b,
           a2=c&d, 
           a3=a1|a2;
	   
    assign out=a3, 
           out_n= ~(a3);
endmodule
```
## [7458 chip]
```bash
module top_module ( 
    input p1a, p1b, p1c, p1d, p1e, p1f,
    output p1y,
    input p2a, p2b, p2c, p2d,
    output p2y );
wire w1,w2,w3,w4;
    assign w1 = p2a&p2b, 
           w2 = p2c&p2d, 
           p2y= w1|w2;        
    assign w3= p1a&p1b&p1c, 
           w4= p1d&p1e&p1f,
           p1y= w3|w4;
endmodule
```
## [Vectors]
```bash
module top_module ( 
    input wire [2:0] vec,
    output wire [2:0] outv,
    output wire o2,
    output wire o1,
    output wire o0  );
    assign outv=vec[2:0];
    assign o2=vec[2];
    assign o1=vec[1];
    assign o0=vec[0];
endmodule
```
## [Vector 1]
```bash
`default_nettype none    
module top_module( 
    input wire [15:0] in,
    output wire [7:0] out_hi,
    output wire [7:0] out_lo );
    assign out_lo=in[7:0];
    assign out_hi=in[15:8];
endmodule
```
## [Vector 2]
```bash
module top_module( 
    input [31:0] in,
    output [31:0] out );//
    assign out[31:24]=in[7:0];
    assign out[23:16]=in[15:8];
    assign out[15:8]=in[23:16];
    assign out[7:0]=in[31:24];
endmodule
```
## [4 input gate]
```bash
module top_module( 
    input [3:0] in,
    output out_and,
    output out_or,
    output out_xor
);
    assign out_and=in[3]&in[2]&in[1]&in[0];
    assign out_or=in[3]|in[2]|in[1]|in[0];
    assign out_xor=in[3]^in[2]^in[1]^in[0];
endmodule
```
## [Vector 3 - Concatination]
```bash
module top_module (
    input [4:0] a, b, c, d, e, f,
    output [7:0] w, x, y, z );//
    assign {w[7:0],x[7:0],y[7:0],z[7:0]}={a[4:0],b[4:0],c[4:0],d[4:0],e[4:0],f[4:0],2'b11};
endmodule
```
## [Vector Reversing]
```bash
module top_module( 
    input [7:0] in,
    output [7:0] out);
    assign out[7:0]={in[0], in[1], in[2], in[3], in[4], in[5], in[6], in[7]};
endmodule
```
## [Vector 4 -Replication]
```bash
module top_module (
    input [7:0] in,
    output [31:0] out );
    assign out={{24{in[7]}},in};
endmodule
```
## [Vector 5]
### Method 1
```bash
module top_module (
    input a, b, c, d, e,
    output [24:0] out );
    assign out=~{{5{a}},{5{b}},{5{c}},{5{d}},{5{e}}}^{5{a,b,c,d,e}};  
endmodule
```
### Method 2
```bash
module top_module (
    input a, b, c, d, e,
    output [24:0] out );
    
    wire [24:0] top = { {5{a}}, {5{b}}, {5{c}}, {5{d}}, {5{e}} };
    wire [24:0] bottom = {5{ {a, b, c, d, e} }};
    assign out = top ~^ bottom;
endmodule
```
# Module
## [Vector 5]
### Method 1
```bash
module top_module ( input a, input b, output out );
mod_a m1(a,b,out);
endmodule
```
### Method 2
```bash
module top_module ( input a, input b, output out );
mod_a m1(.in1(a),.in2(b),.out(out));
endmodule
```
## Connecting ports by position 
```bash
module top_module ( 
    input a, 
    input b, 
    input c,
    input d,
    output out1,
    output out2
);
mod_a m1(out1,out2,a,b,c,d);
endmodule
```
## Connecting ports by port name
```bash
module top_module ( 
    input a, 
    input b, 
    input c,
    input d,
    output out1,
    output out2
);
mod_a m(.in1(a),.in2(b),.in3(c),.in4(d),.out1(out1),.out2(out2));
endmodule
```
## Three ports
```bash
module top_module ( input clk, input d, output q );
wire q1,q2;
my_dff m1(.clk(clk),.d(d),.q(q1));
my_dff m2(.clk(clk),.d(q1),.q(q2));
my_dff m3(.clk(clk),.d(q2),.q(q));
endmodule
```
