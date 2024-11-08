# Adding Signal Output Causes Abnormal Simulation Results in Icarus Verilog

In the following two code snippets, y is the output wire.

```
assign y = {
            forvar19
           };
```

```
assign y = {
            wire7,
            forvar19
           };
```

The original design of the two statements generated `syn_vivado.v` after synthesis in Vivado, and I simulated the synthesized code. 

Theoretically, if all other conditions remain the same, the simulation output in the `forvar19` section should be consistent, meaning that the lower bits of `y` should be the same for the `forvar19` value in both cases.

However, when I simulated using iverilog, with all other conditions being equal, the two produced different simulation outputs.
 (both `wire7` and `forvar19` I constructed are 2-bit).

![381f76d24632fb2f668830e87b70f851](https://github.com/steveicarus/iverilog/assets/168843330/92d566c4-1d21-4d83-9b85-dd0821fe1a45)
The left side only includes the `forvar19` output as shown (highlighted in yellow for the `forvar19` output section); 
the right side includes the output with the `wire7` signal as shown (highlighted in yellow for the `forvar19` output section). 

Inconsistencies appeared on lines 6, 7, and 14. 

Therefore, I used Vivado's simulation tool to simulate the synthesized output of the two statements, and the lower bits of the `forvar19` output were consistent.

![583f0e2024c1d3fcca1791c26356941b](https://github.com/steveicarus/iverilog/assets/168843330/f378a88d-f243-41df-88c7-c0df34b57401)
The left side only includes the `forvar19` output as shown (highlighted in yellow for the `forvar19` output section); 
the right side includes the output with the `wire7` signal as shown (highlighted in yellow for the `forvar19` output section). 

**Comparing the outputs of the two simulation tools mentioned above, I think that the issue might be caused by adding signal output, leading to abnormal simulation results in iverilog.** 
