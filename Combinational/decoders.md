# 6: Decoders


## 1. 2 to 4 Decoder

### Truth Table

| in[1:0] | out[3:0] |
|---------|----------|
| 00      | 0001     |
| 01      | 0010     |
| 10      | 0100     |
| 11      | 1000     |

### Verilog Code

```verilog
`timescale 1ns / 1ps

module decoder_2to4 (
    input [1:0] in,
    output reg [3:0] out
);

always @(*) begin
    case(in)
        2'b00: out = 4'b0001;
        2'b01: out = 4'b0010;
        2'b10: out = 4'b0100;
        2'b11: out = 4'b1000;
        default: out = 4'b0000;
    endcase
end

endmodule
```

### Testbench

```verilog
`timescale 1ns / 1ps

module testbench;

reg [1:0] in;
wire [3:0] out;

decoder_2to4 dut (.in(in), .out(out));

initial begin

in = 2'b00; #10;
in = 2'b01; #10;
in = 2'b10; #10;
in = 2'b11; #10;
end

endmodule
```

### Schematic
![2 to 4 Decoder Schematic](https://i.ibb.co/yXC4t2y/2-to-4-Decoder.png)

### Simulation Waveform
![2 to 4 Decoder Simulation](https://i.ibb.co/5FmzGpQ/2-to-4-Decoder-simu.png)

---

## 2. 3 to 8 Decoder

### Truth Table

| in[2:0] | out[7:0]  |
|---------|-----------|
| 000     | 0000_0001 |
| 001     | 0000_0010 |
| 010     | 0000_0100 |
| 011     | 0000_1000 |
| 100     | 0001_0000 |
| 101     | 0010_0000 |
| 110     | 0100_0000 |
| 111     | 1000_0000 |

### Verilog Code

```verilog
`timescale 1ns / 1ps

module decoder_3to8 (
    input [2:0] in,
    output reg [7:0] out
);
integer i;
always @(*) begin
    out = 8'b00000000; 
    for (i = 0; i < 8; i = i + 1) begin
        if (i == in) begin
            out[i] = 1'b1; 
        end
    end
end

endmodule
```

### Testbench

```verilog
`timescale 1ns / 1ps

module testbench;

    reg [2:0] in;
    wire [7:0] out;
    
    decoder_3to8 dut ( .in(in), .out(out) );

    initial begin
        in = 3'b000; #10;
        $display("Input = %b, Output = %b", in, out);
        in = 3'b001; #10;
        $display("Input = %b, Output = %b", in, out);
        in = 3'b010; #10;
        $display("Input = %b, Output = %b", in, out);
        in = 3'b011; #10;
        $display("Input = %b, Output = %b", in, out);
        in = 3'b100; #10;
        $display("Input = %b, Output = %b", in, out);
        in = 3'b101; #10;
        $display("Input = %b, Output = %b", in, out);
        in = 3'b110; #10;
        $display("Input = %b, Output = %b", in, out);
        in = 3'b111; #10;
        $display("Input = %b, Output = %b", in, out);
        
        $finish;
    end

endmodule
```

### Schematic
![3 to 8 Decoder Schematic](https://i.ibb.co/XytTMLt/3-to-8-Decoder.png)

### Simulation Waveform
![3 to 8 Decoder Simulation](https://i.ibb.co/2t089ph/3-to-8-Decoder-simu.png)

---

## 3. 4 to 16 Decoder

### Truth Table (Sample rows)

| in[3:0] | Active Output |
|---------|----------------|
| 0000    | out[0] = 1     |
| 0001    | out[1] = 1     |
| 0010    | out[2] = 1     |
| 0011    | out[3] = 1     |
| ...     | ...            |
| 1111    | out[15] = 1    |

*(Only one of the 16 output bits is `1` for any given 4-bit input; all others remain `0`.)*

### Verilog Code

```verilog
`timescale 1ns / 1ps

module decoder_4to16 (
    input [3:0] in,
    output [15:0] out
);

assign out[0] = (in == 4'b0000) ? 1'b1 : 1'b0;
assign out[1] = (in == 4'b0001) ? 1'b1 : 1'b0;
assign out[2] = (in == 4'b0010) ? 1'b1 : 1'b0;
assign out[3] = (in == 4'b0011) ? 1'b1 : 1'b0;
assign out[4] = (in == 4'b0100) ? 1'b1 : 1'b0;
assign out[5] = (in == 4'b0101) ? 1'b1 : 1'b0;
assign out[6] = (in == 4'b0110) ? 1'b1 : 1'b0;
assign out[7] = (in == 4'b0111) ? 1'b1 : 1'b0;
assign out[8] = (in == 4'b1000) ? 1'b1 : 1'b0;
assign out[9] = (in == 4'b1001) ? 1'b1 : 1'b0;
assign out[10] = (in == 4'b1010) ? 1'b1 : 1'b0;
assign out[11] = (in == 4'b1011) ? 1'b1 : 1'b0;
assign out[12] = (in == 4'b1100) ? 1'b1 : 1'b0;
assign out[13] = (in == 4'b1101) ? 1'b1 : 1'b0;
assign out[14] = (in == 4'b1110) ? 1'b1 : 1'b0;
assign out[15] = (in == 4'b1111) ? 1'b1 : 1'b0;

endmodule
```

### Testbench

```verilog
`timescale 1ns / 1ps

module tb_decoder_4to16;

reg [3:0] in;
wire [15:0] out;

decoder_4to16 dut ( .in(in), .out(out) );

initial begin

    in = 4'b0000;#10;
    
    in = 4'b0001;#10;
    
    in = 4'b0010;#10;
    
    in = 4'b0011;#10;
    
    in = 4'b1111;#10;
    
    $finish;
end

always @(out) begin
    $display("Input: %b, Output: %b", in, out);
end

endmodule
```

### Schematic
![4 to 16 Decoder Schematic](https://i.ibb.co/cvW1YVX/4-to-16-decoder.png)

### Simulation Waveform
![4 to 16 Decoder Simulation](https://i.ibb.co/M5bKp69/4-to-16-decoder-simu.png)
