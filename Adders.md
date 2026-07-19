# Day 1: Half Adder & Full Adder



## 1. Half Adder


### Truth Table

| A | B | Sum (S) | Carry (C) |
|---|---|---------|-----------|
| 0 | 0 | 0       | 0         |
| 0 | 1 | 1       | 0         |
| 1 | 0 | 1       | 0         |
| 1 | 1 | 0       | 1         |

**Boolean Equations:**
- `Sum = A ⊕ B`
- `Carry = A · B`

### Verilog Code (Dataflow Modeling)

```verilog
`timescale 1ns / 1ps

module half_adder_dataflow( input A,B, output Sum,Carry);

assign Sum = A^B;
assign Carry = A&B;

endmodule
```

### Testbench

```verilog
`timescale 1ns / 1ps

module half_adder_dataflow_tb;
reg A_tb;
reg B_tb;

wire Carry_tb;
wire Sum_tb;
half_adder_dataflow dut (.A(A_tb), .B(B_tb), .Sum(Sum_tb), .Carry(Carry_tb));

initial begin
A_tb = 1'b0; B_tb = 1'b0;
#10 A_tb = 1'b0; B_tb = 1'b1;
#10 A_tb = 1'b1; B_tb = 1'b0;
#10 A_tb = 1'b1; B_tb = 1'b1;
#10 $stop;

end

endmodule
```

### Schematic
![Half Adder Schematic](https://i.ibb.co/CJ91XVS/Half_Adder.png)

### Simulation Waveform
![Half Adder Simulation](https://i.ibb.co/tLLPdM8/Half_adder_sim.png)

---

## 2. Full Adder


### Truth Table

| A | B | Cin | Sum (S) | Carry (Cout) |
|---|---|-----|---------|--------------|
| 0 | 0 | 0   | 0       | 0            |
| 0 | 0 | 1   | 1       | 0            |
| 0 | 1 | 0   | 1       | 0            |
| 0 | 1 | 1   | 0       | 1            |
| 1 | 0 | 0   | 1       | 0            |
| 1 | 0 | 1   | 0       | 1            |
| 1 | 1 | 0   | 0       | 1            |
| 1 | 1 | 1   | 1       | 1            |

**Boolean Equations:**
- `Sum = A ⊕ B ⊕ Cin`
- `Carry = (A · B) + (Cin · (A ⊕ B))`

### Verilog Code (Dataflow Modeling)

```verilog
`timescale 1ns / 1ps

module Full_Adder_DF(
    input A,B,Cin,
    output Sum,Carry
    );
    assign Sum = A^B^Cin;
    assign Carry = (A&B) | Cin & (A^B);
endmodule
```

### Testbench

```verilog
`timescale 1ns / 1ps

module full_adder_tb;

reg A_tb,B_tb,Cin_tb;
wire Sum_tb,Carry_tb;

Full_Adder_DF dut (.A(A_tb), .B(B_tb), .Cin(Cin_tb), .Sum(Sum_tb), .Carry(Carry_tb) );

initial begin

A_tb = 1'b0; B_tb = 1'b0; Cin_tb = 1'b0;
#10 A_tb = 1'b0; B_tb = 1'b0; Cin_tb = 1'b1;
#10 A_tb = 1'b0; B_tb = 1'b1; Cin_tb = 1'b0;
#10 A_tb = 1'b0; B_tb = 1'b1; Cin_tb = 1'b1;
#10 A_tb = 1'b1; B_tb = 1'b0; Cin_tb = 1'b0;
#10 A_tb = 1'b1; B_tb = 1'b0; Cin_tb = 1'b1;
#10 A_tb = 1'b1; B_tb = 1'b1; Cin_tb = 1'b0;
#10 A_tb = 1'b1; B_tb = 1'b1; Cin_tb = 1'b1;
#10 $stop;
end

endmodule
```

### Schematic
![Full Adder Schematic](https://i.ibb.co/hgQ01V1/FA.png)

### Simulation Waveform
![Full Adder Simulation](https://i.ibb.co/6BF4BMC/FA_Sim.png)
