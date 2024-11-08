# VerFuzzer
## [Generating Syntax Valid Verilog Programs to Test Logic Synthesis Tools by Prompting Large Language Models](https://github.com/WeneneW/VerFuzzer)

***
**Env dependencies:**
1. **python 3.8**
2. **openai 1.17.1**
3. **pyverilog 1.3.0**
4. **Provide an API for large language models in src/openai_client.py**

***
**Fuzz Testing Targets:(logic synthesis tools and simulated tools)**
1. **Vivado 2023.2**
2. **Yosys 0.39+165**
3. **Icarus Verilog V12_0**
4. **Quartus Prime 23.1**
***

## Our Work
In modern electronic system design, the **logic synthesis and functional simulation steps of Field-Programmable Gate Arrays (FPGAs) play a crucial role**. 
These steps are performed by **Electronic Design Automation tools**, which **convert Hardware Description Language (HDL) code into logic gates and circuit layouts**, and **simulate their behavior to ensure the correctness and stability of the design**. 
However, **logic synthesis tools and simulation tools may contain defects** that can cause the design to exhibit unexpected behavior when being implemented in hardware, leading to serious consequences. 
Although existing FPGA fuzzers face limitations such as **limited complexity and diversity of test cases, fixed and single input signals**, as well as **inadequate consideration of clock variations**, which restrict their effectiveness in thoroughly testing logic synthesis tools.
To address these limitations, we propose a novel fuzzing method named **VerFuzzer**, the **first fuzz testing tool that leverages the prompting large language models for generating valid Verilog programs** to test logic synthesis tools.
By leveraging prompt learning, VerFuzzer **generates Verilog programs that accommodate both syntax evolution and diversification**, thereby resolving the aforementioned challenges. 
Furthermore, its **generation pattern, based on syntax tree branching structures**, facilitates **bug identification and test case reduction** by comparing HDL designs before and after expansion. 
Through **differential testing**, VerFuzzer effectively **reveals potential defects in logic synthesis and simulation tools**.

***
## directory structure
```
VerFuzzer-main/
├── README.md
├── check.py
├── config/
│   └── config.toml
├── src/
│   ├── AST.py
│   ├── code_generate.py
│   ├── code_inspect.py
│   ├── config_extract.py
│   ├── equiv_check.py
│   ├── equivcheck_code.py
│   ├── error_feedback.py
│   ├── generate.py
│   ├── openai_client.py
│   ├── prompt_generate.py
│   ├── run.sh
│   ├── run_main.sh
│   ├── run_symbiyosys.sh
│   ├── synthesis.py
│   ├── testbench.py
│   └── Tool/
│       ├── Icarus.py
│       ├── Vivado.py
│       └── Yosys.py
│   └── temp_save/
│       ├── tem_ast.txt
│       └── temp.v
```

The directory structure of the document is as follows. After adding the API, you can run the command below to execute:
```bash run.sh <outputdir> <number>```
***
## These are the errors we have discovered (./errors)
| ID    | Summary                                                                     | Software |
|-------|-----------------------------------------------------------------------------|----------|
| error1  | Yosys Mishandles Bit Operations on Empty Strings                            | Yosys    |
| error2  | Yosys Synthesis Causes Netlist Discrepancies with Original Design           | Yosys    |
| error3  | Yosys read_verilog Command Doesn’t Respect Signed Keyword                   | Yosys    |
| error4  | Abnormal Output from Yosys Synthesis                                        | Yosys    |
| error5  | Port Declaration Syntax Error with Yosys                                    | Yosys    |
| error6  | Incorrect Right Shift Operation in Yosys                                    | Yosys    |
| error7  | Adding Signal Output Causes Abnormal Simulation Results in Iverilog         | Iverilog |
| error8  | Abnormal Simulation Output in Icarus Verilog                                | Iverilog |
| error9  | Direct operations on strings will result in synthesis errors                | Quartus  |
| error10 | Increment Operation (++) Causes Error                                       | Quartus  |
| error11 | Segmentation Fault During Synthesis in Vivado: Memory Access Issues         | Vivado   |
| error12 | Vivado Synthesis Crash Due to Tcl_PanicVA and TclEvalObjEx Errors           | Vivado   |
| error13 | Vivado Synthesis Crash Due to NPinC and ConstProp Errors                    | Vivado   |
| error14 | Vivado Synthesis Crash Due to HARTNIUtil, HARTLutMap Errors                 | Vivado   |
| error15 | Vivado Synthesis Crash Due to DFNode::calcConstantBinaryInt Errors          | Vivado   |
| error16 | Vivado Synthesis Crash Due to HARTOptMux::groupMFFC Errors                  | Vivado   |
| error17 | Vivado Synthesis Crash Due to HARTOptMux::createPartition Errors            | Vivado   |
| error18 | Vivado Synthesis Crash Due to HOptGenControl::areaInSource Errors           | Vivado   |
| error19 | Vivado Synthesis Crash Due to DFLink::findIndexForPortName Errors           | Vivado   |
| error20 | Bit-Width Definition Inconsistencies Leading to Different Outputs           | Vivado   |

We are grateful to the staff of these tools for their assistance in discovering and confirming vulnerabilities.
