# Ripple Carry Adder


## Truth Table (Sample Cases)

| A[3:0] | B[3:0] | Cin | Sum[3:0] | Cout |
|--------|--------|-----|----------|------|
| 0000   | 0000   | 0   | 0000     | 0    |
| 0100   | 0100   | 0   | 1000     | 0    |
| 0001   | 0001   | 0   | 0010     | 0    |
| 0101   | 0101   | 0   | 1010     | 0    |
| 0011   | 0011   | 0   | 0110     | 0    |
| 0111   | 0111   | 0   | 1110     | 0    |
| 1111   | 1111   | 0   | 1110     | 1    |

## Verilog Code

```verilog
`timescale 1ns / 1ps

module ripple_carry_adder_4bit(
    input[3:0] a,
    input[3:0] b,
    input cin,
    output[3:0] sum,
    output cout
    );
    wire[2:0] w;
    
    full_adder a1(.A(a[0]), .B(b[0]), .Cin(cin), .Carry(w0), .Sum(sum[0]));
    full_adder a2(.A(a[1]), .B(b[1]), .Cin(w0), .Carry(w1), .Sum(sum[1]));
    full_adder a3(.A(a[2]), .B(b[2]), .Cin(w1), .Carry(w2), .Sum(sum[2]));
    full_adder a4(.A(a[3]), .B(b[3]), .Cin(w2), .Carry(cout), .Sum(sum[3]));
   
endmodule

module full_adder(A,B,Cin,Carry,Sum);

input A,B,Cin;
output Carry,Sum;

assign Sum = A^B^Cin;
assign Carry = (A&B) | Cin & (A^B);

endmodule
```

## Testbench

```verilog
`timescale 1ns / 1ps

module tb_ripple_carry_adder_4bit();

reg [3:0] a, b;
reg cin;
wire [3:0] sum;
wire cout;

ripple_carry_adder_4bit dut(
    .a(a), 
    .b(b),
    .cin(cin), 
    .sum(sum),
    .cout(cout)
);

initial begin
    cin = 0;
    a = 4'b0000; b = 4'b0000;
    #10;
    a = 4'b0001; b = 4'b0001; 
    #10;
    a = 4'b0010; b = 4'b0011;
    #10;
    a = 4'b0001; b = 4'b0110;
    #10;
    
    $display("SUM = %b, COUT = %b", sum, cout);
    $finish;
end
      
endmodule
```

## Schematic
![Ripple Carry Adder Schematic](https://i.ibb.co/SsMw5sH/Ripple_Carry_Adder.png)

## Simulation Waveform
![Ripple Carry Adder Simulation](https://i.ibb.co/0FnvV5h/Ripple_Adder_simu.png)
