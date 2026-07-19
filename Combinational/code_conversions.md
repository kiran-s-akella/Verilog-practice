# 7: Code Conversion (Gray & Binary)


## 1. Binary to Gray Code Conversion

**Conversion Rule:** The MSB of Gray code is the same as the MSB of Binary. Every other Gray bit is the XOR of the current and previous Binary bit.
`gray[i] = bin[i] ⊕ bin[i+1]` (for i from 0 to n-2), `gray[n-1] = bin[n-1]`

### Truth Table

| Binary | Gray | Binary | Gray |
|--------|------|--------|------|
| 0000   | 0000 | 1000   | 1100 |
| 0001   | 0001 | 1001   | 1101 |
| 0010   | 0011 | 1010   | 1111 |
| 0011   | 0010 | 1011   | 1110 |
| 0100   | 0110 | 1100   | 1010 |
| 0101   | 0111 | 1101   | 1011 |
| 0110   | 0101 | 1110   | 1001 |
| 0111   | 0100 | 1111   | 1000 |

### Verilog Code

```verilog
`timescale 1ns / 1ps

module binary_to_gray(bin,gray);
input[3:0]bin; 
output[3:0]gray; 
assign gray[3]=bin[3];
assign gray[2]=bin[3]^bin[2]; 
assign gray[1]=bin[2]^bin[1]; 
assign gray[0]=bin[1]^bin[0]; 
endmodule
```

### Conceptual Diagram
![Binary to Gray Conversion](https://media.geeksforgeeks.org/wp-content/uploads/20220420085103/Screenshot695-300x191.png)

### Testbench

```verilog
`timescale 1ns / 1ps

module testbench_binary_to_gray;
  reg [3:0] bin;
  wire [3:0] gray;
  integer i;
  binary_to_gray dut (.bin(bin),.gray(gray));

  initial begin
    bin = 4'b0000;
    $display("Input (Binary) | Output (Gray)");
    for (i = 0; i < 16; i = i + 1) begin
    $display("%4b     | %4b", bin, gray);
    bin = bin + 1;
    #10;
    end
    $finish;
  end

endmodule
```

### Schematic
![Binary to Gray Schematic](https://i.ibb.co/g9X3fjc/bin_to_gray.png)

### Simulation Waveform
![Binary to Gray Simulation](https://i.ibb.co/hyMRGr6/Bin_to_gray_simu.png)

---

## 2. Gray to Binary Code Conversion

**Conversion Rule:** The MSB of Binary is the same as the MSB of Gray. Every other Binary bit is the XOR of the current Gray bit and the previously computed Binary bit.
`bin[n-1] = gray[n-1]`, `bin[i] = bin[i+1] ⊕ gray[i]` (for i from n-2 down to 0)

### Truth Table

| Gray | Binary | Gray | Binary |
|------|--------|------|--------|
| 0000 | 0000   | 1100 | 1000   |
| 0001 | 0001   | 1101 | 1001   |
| 0011 | 0010   | 1111 | 1010   |
| 0010 | 0011   | 1110 | 1011   |
| 0110 | 0100   | 1010 | 1100   |
| 0111 | 0101   | 1011 | 1101   |
| 0101 | 0110   | 1001 | 1110   |
| 0100 | 0111   | 1000 | 1111   |

### Verilog Code

```verilog
`timescale 1ns / 1ps

module gray_to_binary(gray, bin);
  input [3:0] gray;
  output reg [3:0] bin;

  always @(gray) begin
    bin[3] = gray[3];
    bin[2] = gray[3] ^ gray[2];
    bin[1] = bin[2] ^ gray[1];
    bin[0] = bin[1] ^ gray[0];
  end
endmodule
```

### Conceptual Diagram
![Gray to Binary Conversion](https://media.geeksforgeeks.org/wp-content/uploads/20220420085103/Screenshot696-300x206.png)

### Testbench

```verilog
`timescale 1ns / 1ps

module testbench_gray_to_binary;

  reg [3:0] gray;
  wire [3:0] bin;
  integer i;
  gray_to_binary dut (.gray(gray),.bin(bin));
  initial begin
    $display("Input (Gray) | Output (Binary)");

    for (i = 0; i < 16; i = i + 1) begin
    gray = i;
      
    $display("%4b          | %4b", gray, bin);
    #10;
    end
    $finish;
  end

endmodule
```

### Schematic
![Gray to Binary Schematic](https://i.ibb.co/KXvyssC/gray_to_bin.png)

### Simulation Waveform
![Gray to Binary Simulation](https://i.ibb.co/FqDkBLC/gray_to_bin_simu.png)
