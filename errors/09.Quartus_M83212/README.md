## Direct operations on strings will result in synthesis errors


```verilog
module test1 (y, clk);
  output wire y;
  input wire clk; 
  wire wire1; 
  assign wire1 = $signed((~""));
  assign y = wire1;
endmodule

```

```verilog
module test1 (y, clk);
  output wire y;
  input wire clk; 

  wire wire1; 
  reg str = "";
  assign wire1 = $signed(~str);
  assign y = wire1;
endmodule

```
