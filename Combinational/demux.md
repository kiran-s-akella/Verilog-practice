# 4: Demultiplexers


## 1. 1 × 2 Demux

### Truth Table

| sel | din | dout_1 | dout_0 |
|-----|-----|--------|--------|
| 0   | d   | 0      | d      |
| 1   | d   | d      | 0      |

### Verilog Code

```verilog
module demux_1x2 (
    input wire din,
    input wire sel,
    output wire dout_0,
    output wire dout_1
);

assign dout_0 = (sel) ? 1'b0 : din;
assign dout_1 = (sel) ? din : 1'b0;

endmodule
```

### Testbench

```verilog
module testbench_demux_1x2;

reg din;
reg sel;
wire dout_0;
wire dout_1;

demux_1x2 dut ( .din(din), .sel(sel), .dout_0(dout_0), .dout_1(dout_1) );

initial begin
    din = 1'b0; sel = 0;
    #10;
    din = 1'b1; sel = 0;
    #10;
    din = 1'b1; sel = 1;
    #10;
    din = 1'b0; sel = 1;
    #10;
    $finish;
end
always @(dout_0, dout_1) begin
    $display("sel = %b, din = %b, dout_0 = %b, dout_1 = %b", sel, din, dout_0, dout_1);
end
endmodule
```

### Schematic
![1x2 Demux Schematic](https://i.ibb.co/vCW1r3K/Demux_1X2.png)

### Simulation Waveform
![1x2 Demux Simulation](https://i.ibb.co/wyksGxV/Demux_1X2_Simu.png)

---

## 2. 1 × 4 Demux

### Truth Table

| sel[1:0] | dout_0 | dout_1 | dout_2 | dout_3 |
|----------|--------|--------|--------|--------|
| 00       | din    | 0      | 0      | 0      |
| 01       | 0      | din    | 0      | 0      |
| 10       | 0      | 0      | din    | 0      |
| 11       | 0      | 0      | 0      | din    |

### Verilog Code

```verilog
module demux_1x4 (
    input wire din,
    input wire [1:0] sel,
    output wire dout_0,
    output wire dout_1,
    output wire dout_2,
    output wire dout_3 );

assign dout_0 = (sel == 2'b00) ? din : 1'b0;
assign dout_1 = (sel == 2'b01) ? din : 1'b0;
assign dout_2 = (sel == 2'b10) ? din : 1'b0;
assign dout_3 = (sel == 2'b11) ? din : 1'b0;

endmodule
```

### Testbench

```verilog
module testbench_demux_1x4;

reg din;
reg [1:0] sel;
wire dout_0;
wire dout_1;
wire dout_2;
wire dout_3;

demux_1x4 uut ( .din(din), .sel(sel), .dout_0(dout_0), .dout_1(dout_1), .dout_2(dout_2), 
.dout_3(dout_3) );

initial begin
    din = 1'b0; sel = 2'b00; #10;

    din = 1'b1; sel = 2'b00; #10;

    din = 1'b1; sel = 2'b01; #10;

    din = 1'b0; sel = 2'b10; #10;

    din = 1'b1; sel = 2'b11; #10;
    $finish;
end

always @(dout_0, dout_1, dout_2, dout_3) begin
    $display("sel = %b, din = %b, dout_0 = %b, dout_1 = %b, dout_2 = %b, dout_3 = %b", 
						sel, din, dout_0, dout_1, dout_2, dout_3);
end

endmodule
```

### Schematic
![1x4 Demux Schematic](https://i.ibb.co/N9VD11h/Demux_1X4.png)

### Simulation Waveform
![1x4 Demux Simulation](https://i.ibb.co/8zrrXCH/Demux_1X4_Simu.png)

---

## 3. 1 × 8 Demux

### Truth Table

| sel[2:0] | Active Output |
|----------|---------------|
| 000      | dout_0 = din  |
| 001      | dout_1 = din  |
| 010      | dout_2 = din  |
| 011      | dout_3 = din  |
| 100      | dout_4 = din  |
| 101      | dout_5 = din  |
| 110      | dout_6 = din  |
| 111      | dout_7 = din  |

*(All other outputs remain 0 for each row.)*

### Verilog Code

```verilog
module demux_1x8 (
    input wire din,
    input wire [2:0] sel,
    output wire dout_0,
    output wire dout_1,
    output wire dout_2,
    output wire dout_3,
    output wire dout_4,
    output wire dout_5,
    output wire dout_6,
    output wire dout_7
);

assign dout_0 = (sel == 3'b000) ? din : 1'b0;
assign dout_1 = (sel == 3'b001) ? din : 1'b0;
assign dout_2 = (sel == 3'b010) ? din : 1'b0;
assign dout_3 = (sel == 3'b011) ? din : 1'b0;
assign dout_4 = (sel == 3'b100) ? din : 1'b0;
assign dout_5 = (sel == 3'b101) ? din : 1'b0;
assign dout_6 = (sel == 3'b110) ? din : 1'b0;
assign dout_7 = (sel == 3'b111) ? din : 1'b0;

endmodule
```

### Testbench

```verilog
module testbench_demux_1x8;

reg din;
reg [2:0] sel;
wire dout_0;
wire dout_1;
wire dout_2;
wire dout_3;
wire dout_4;
wire dout_5;
wire dout_6;
wire dout_7;

demux_1x8 dut ( .din(din), .sel(sel), .dout_0(dout_0), .dout_1(dout_1), .dout_2(dout_2),
    .dout_3(dout_3), .dout_4(dout_4), .dout_5(dout_5), .dout_6(dout_6), .dout_7(dout_7));

initial begin
    din = 1'b0; sel = 3'b000; #10;

    din = 1'b1; sel = 3'b000; #10;

    din = 1'b1; sel = 3'b001; #10;

    din = 1'b0; sel = 3'b010; #10;

    din = 1'b1; sel = 3'b111; #10;

    $finish;
end

always @(dout_0, dout_1, dout_2, dout_3, dout_4, dout_5, dout_6, dout_7) begin
    $display("sel = %b, din = %b, dout_0 = %b, dout_1 = %b, dout_2 = %b, dout_3 = %b, dout_4 = %b, dout_5 = %b, dout_6 = %b, dout_7 = %b", sel, din, dout_0, dout_1, dout_2, dout_3, dout_4, dout_5, dout_6, dout_7);
end

endmodule
```

### Schematic
![1x8 Demux Schematic](https://i.ibb.co/F3CdXzs/Demux_1X8.png)

### Simulation Waveform
![1x8 Demux Simulation](https://i.ibb.co/qJSWSzy/Demux_1X8_Simu.png)
