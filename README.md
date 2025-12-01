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
## [Connecting ports by position] 
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
## [Connecting ports by name]
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
## Module shift [Three modules]
```bash
module top_module ( input clk, input d, output q );
wire q1,q2;
my_dff m1(.clk(clk),.d(d),.q(q1));
my_dff m2(.clk(clk),.d(q1),.q(q2));
my_dff m3(.clk(clk),.d(q2),.q(q));
endmodule
```
## Module shift8 [Modules and vectors]
```bash
module top_module ( 
    input clk, 
    input [7:0] d, 
    input [1:0] sel, 
    output [7:0] q 
);
wire [7:0]q1,q2,q3;
my_dff8 m1(.clk(clk),.d(d),.q(q1));
my_dff8 m2(.clk(clk),.d(q1),.q(q2));
my_dff8 m3(.clk(clk),.d(q2),.q(q3));
always @(*)
    begin
 case(sel)
     2'b00:q=d;
     2'b01:q=q1;
     2'b10:q=q2;
     2'b11:q=q3;
 endcase
     end
endmodule
```
## Module add [Adder-1]
```bash
module top_module(
    input [31:0] a,
    input [31:0] b,
    output [31:0] sum
);
wire c1,c2;
add16 inst1(.a(a[15:0]),.b(b[15:0]),.cin(1'b0),.sum(sum[15:0]),.cout(c1));
add16 inst2(.a(a[31:16]),.b(b[31:16]),.cin(c1),.sum(sum[31:16]),.cout(c2));
   
endmodule
```
## Module fadd [Adder-2]
```bash
module top_module (
    input [31:0] a,
    input [31:0] b,
    output [31:0] sum
);
wire c1,c2;
add16 inst1(.a(a[15:0]),.b(b[15:0]),.cin(1'b0),.sum(sum[15:0]),.cout(c1));
add16 inst2(.a(a[31:16]),.b(b[31:16]),.cin(c1),.sum(sum[31:16]),.cout(c2));
endmodule

module add1 ( input a, input b, input cin,   output sum, output cout );
assign sum=a^b^cin;
assign cout=a&b | b&cin | cin&a;
endmodule
```
## Module cseladd [Carry-select adder]
```bash
module top_module(
    input [31:0] a,
    input [31:0] b,
    output [31:0] sum
);
wire w1,w2,w3;
    reg [15:0]sum1,sum2;
    add16 a1(a[15:0],b[15:0],1'b0,sum[15:0],w1);
    add16 a2(a[31:16],b[31:16],1'b0,sum1[15:0],w2);
    add16 a3(a[31:16],b[31:16],1'b1,sum2[15:0],w3);  
    always@(*)
        case(w1)
            0:sum[31:16]=sum1[15:0];
            1:sum[31:16]=sum2[15:0];
        endcase
endmodule
```
## Module addsub [Adder-subtractor]
```bash
module top_module(
    input [31:0] a,
    input [31:0] b,
    input sub,
    output [31:0] sum
);
    wire w1,w2;
    wire [31:0]w;
      assign w = b ^ {32{sub}};  
    add16 a1(a[15:0],w[15:0],sub,sum[15:0],w1);
    add16 a2(a[31:16],w[31:16],w1,sum[31:16],w2);
endmodule
```
## [alwaysblock1]
```bash
module top_module(
    input a, 
    input b,
    output wire out_assign,
    output reg out_alwaysblock
);
assign out_assign=a&b;
    always@(*)
        out_alwaysblock=a&b;
endmodule
```
## [alwaysblock2]
```bash
module top_module(
    input clk,
    input a,
    input b,
    output wire out_assign,
    output reg out_always_comb,
    output reg out_always_ff   );
assign out_assign=a^b;
    always @(*)
        out_always_comb=a^b;
    always@(posedge clk)
        out_always_ff<=a^b;
endmodule
```
## [always if]
```bash
module top_module(
    input a,
    input b,
    input sel_b1,
    input sel_b2,
    output wire out_assign,
    output reg out_always   ); 
    always@(*)
        begin
            if(sel_b1&&sel_b2)
            begin
            out_always=b;
            end
        else
            begin
            out_always=a;
            end
        end    
    assign out_assign=sel_b2?(sel_b1?b:a):a;      
endmodule
```
## [always if2]
```bash
module top_module (
    input      cpu_overheated,
    output reg shut_off_computer,
    input      arrived,
    input      gas_tank_empty,
    output reg keep_driving  ); //

    always @(*) begin
           shut_off_computer = cpu_overheated;
    end

    always @(*)
        begin
        if (~arrived&&~gas_tank_empty)
           keep_driving = 1;
        else
            keep_driving =0;
        end
endmodule
```
## [Always case]
```bash
module top_module ( 
    input [2:0] sel, 
    input [3:0] data0,
    input [3:0] data1,
    input [3:0] data2,
    input [3:0] data3,
    input [3:0] data4,
    input [3:0] data5,
    output reg [3:0] out);
    always@(*) begin  
        case(sel)
             3'b000 : out= data0;
             3'b001 : out= data1;
             3'b010 : out= data2;
             3'b011 : out= data3;
             3'b100 : out= data4;
             3'b101 : out= data5;
             3'b110 : out=0;
             3'b111 : out=0;
        endcase  
    end
endmodule
```
## Always case2[Parity encoder]
```bash
module top_module (
    input [3:0] in,
    output reg [1:0] pos);
    always@(*)
        begin
        if(in[0]==1)
            pos=0;
    else if(in[1]==1)
            pos=1;
    else if(in[2]==1)
            pos=2;
    else if(in[3]==1)
        pos=3;
    else
        pos=0;
        end    
endmodule

```
## Always casez[priority encoder]
```bash
module top_module (
    input [7:0] in,
    output reg [2:0] pos );
    always@(*)
        begin
            casez(in[7:0])
                8'bzzzzzzz1 : pos=0;
                8'bzzzzzz1z : pos=1;
                8'bzzzzz1zz : pos=2;
                8'bzzzz1zzz : pos=3;
                8'bzzz1zzzz : pos=4;
                8'bzz1zzzzz : pos=5;
                8'bz1zzzzzz : pos=6;
                8'b1zzzzzzz : pos=7;
                default : pos=0;
            endcase
        end   
endmodule
```
## [Always nolatches]
```bash
module top_module (
    input [15:0] scancode,
    output reg left,
    output reg down,
    output reg right,
    output reg up); 
    always@(*)
        begin
         up = 0; down = 0; left = 0; right = 0;
        case(scancode)
         16'he06b  : left=1 ;
         16'he072  : down=1;
         16'he074  : right=1;
         16'he075  : up=1;
         endcase
         end  
endmodule
```
## [conditional- ternary operator]
```bash
module top_module (
    input [7:0] a, b, c, d,
    output [7:0] min);
    wire[7:0]r1,r2;
    assign r1 = (a<b)?a: b;
    assign r2 = (c<d)?c: d;
    assign min = (r1<r2)?r1: r2;
endmodule
```
## [Reduction operator]
```bash
module top_module (
    input [7:0] in,
    output parity); 
    assign parity=in[0]^in[1]^in[2]^in[3]^in[4]^in[5]^in[6]^in[7];
endmodule
```
## [Reduction- Gate_100]
```bash
module top_module( 
    input [99:0] in,
    output out_and,
    output out_or,
    output out_xor 
);
assign out_and= &in;
assign out_or= |in;
assign out_xor= ^in;
endmodule
```
## [Vector100r]
### Method 1
```bash
module top_module( 
    input [99:0] in,
    output [99:0] out
);
    integer i;
    always@(*)
        begin
      for(i=0;i<=99;i=i+1)
           begin
               out[i]=in[99-i];
           end
        end
endmodule
```
### Method 2
```bash
module top_module( 
    input [99:0] in,
    output [99:0] out
);
    integer i;
    always@(*)
        begin
            for(i=99;i>=0;i=i-1)
           begin
               out[99-i]=in[i];
           end
        end
endmodule
```
## [Popcount255]
```bash
module top_module( 
    input [254:0] in,
    output [7:0] out );
    integer i;
    always@(*)
         begin
            out=0;
             for(i=0;i<=254;i=i+1)
        if(in[i]==1)
        out=out+1;
             else;
         end
endmodule
```
