***HDLBits***

# HDL Bits Solutions
## Problem sets
### - Getting Started
### - Verilog Language
   - Basics
   - Vectors
   - Modules:Hierarchy
   - Procedures
   - More Verilog Features
### - Circuits
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

```
