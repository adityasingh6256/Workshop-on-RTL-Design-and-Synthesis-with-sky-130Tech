# Workshop-on-RTL-Design-and-Synthesis-with-sky-130Tech
Details of workshop on RTL design and synthesis using opensource tools - iverilog, gtkwave, yosys and sky 130nm standard cell libraries.
# Table of contents
 - [Day-1- Introduction to Verilog RTL Design and Synthesis](#1-Introduction-to-Verilog-RTL-Design-and-Synthesis)
    - [1.1 Introduction](#11-Introduction)
    - [1.2 Introduction to iverilog and gtkwave based simulation](#12-Introduction-to-iveriilog-and-gtkwave-based-simulation)
    - [1.3 Introduction to Yosys and Logic Synthesizer](#13-Introduction-to-Yosys-and-Logic-Synthesizer)
  - [Day-2- Timing Libraries, Hierarchical and Flat Synthesis](#2-Timing-Libraries-Hierarchical-and-Flat-Synthesis)
    - [2.1 Introduction to Timing Libraries](#21-Introduction-to-Timing-Libraries)
    - [2.2 Hierarchical Synthesis and Flat Synthesis](#22-Hierarchical-Synthesis-and-Flat-Synthesis)
    - [2.3 Various Flip Flop coding Styles and Optimizations](#23-Various-Flip-Flop-coding-Styles-and-Optimizations)
    - [2.4 Interesting Optimizations](#24-Interesting-Optimizations)
  - [Day-3- Combinational and Sequential Optimization](#3-Combinational-and-Sequential-Optimization)
    - [3.1 Introduction to Optimizations](#31-Introduction-to-Optimizations)
    - [3.2 Combinational Logic Optimizations](#32-Combinational-Logic-Optimizations)
    - [3.3 Sequential Logic Optimizations](#33-Sequential-Logic-Optimizations)
    - [3.4 Sequential Optimization for unused outputs](#34-Sequential-Optimization-for-unused-outputs)
  - [Day-4- GLS, Blocking vs Nonblocking and Synthesis-Simulation Mismatch](#4-GLS-Blocking-vs-Nonblocking-and-Synthesis-Simulation-Mismatch)
    - [4.1 GLS Concepts And Flow](#41-GLS-Concepts-And-Flow)
    - [4.2 Synthesis Simulation Mismatch](#42-Synthesis-Simulation-Mismatch)
    - [4.3 Missing Sensitivity List](#43-Missing-Sensitivity-List)
    - [4.4 Blocking and Nonblocking Statements in Verilog](#44-Blocking-and-Nonblocking-Statements-in-Verilog)
  - [Day-5- If, case, for and for generate](#5-If-case-for-and-for-generate)
    - [5.1 If and Case Construct](#51-If-and-Case-Construct)
    - [5.2 Looping Constructs in Verilog](#52-Looping-Constructs-in-Verilog)
  - [Acknowledgement](#6-Acknowledgment)

# 1. Introduction to Verilog RTL Design and Synthesis
## 1.1 Introduction
### What is a design?
Design is the actual verilog code or set of verilog codes which has the intended functionality to meet the required specifications.
### What is a testbench?
Testbench is the setup to apply stimulus to the design to check for its functionality
### Simulator and its working
Simulator is a tool used for checking a verilog design. RTL design is basically the implementation of the design specifications. RTL design is checked for adherence to the specifications by simulating the design. Simulator looks for changes on the input signals. Upon any chaange to the input, output is evaluated. If there are no changes in the input, simulator will not evaluate the output. 
<p align="center">
  <img width=""1000 height="400" src="https://github.com/adityasingh6256/Workshop-on-RTL-Design-and-Synthesis-with-sky-130Tech/blob/c49c180adbfb16a7fb78bfc7cb9930897f53cee3/images/Pic1.png">
</p><br>
Here, design will be instantiated  in the testbench so that there is a mechanism to apply the stimulus. Design may have one or more primary inputs and one or more primary outputs. Whereas the testbench has no primary inputs and primary outputs.

## 1.2 Introduction to iveriilog and gtkwave based simulation
Create a folder vlsi.  
Move into this folder and clone the git repository https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git.    
and also clone the vsdflow repository  https://github.com/kunalg123/vsdflow.git     

```
mkdir vlsi
cd vlsi
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
git clone https://github.com/kunalg123/vsdflow.git
cd sky130RTLDesignAndSynthesisWorkshop
ls
```
<br><br>
Here,folders in sky130RTLDesignAndSynthesisWorkshop are
DC_WORKSHOP , lib , my_lib  ,README.md , verilog_files , yosys_run.sh 
<br><br>

`my_lib` contains to subfolder `verilog_model`. `lib` contains the sky130 stdcell library which is used for synthesis. `verilog_model` contains standard cell verilog models od the cells present in the `lib` file. `verilog_files` contains all the lab experiments needed for the workshop.<br><br>
Iverilog takes the design and testbench as the input and generates a `vcd` file as the output. This `vcd` file stands for value change dump which can be opened with `gtkwave`. 
<p align="center">
  <img width=""1000 height="400" src="https://github.com/adityasingh6256/Workshop-on-RTL-Design-and-Synthesis-with-sky-130Tech/blob/8437307664d3bc875ef8dc67c804d822fc7cb91f/images/Pic2.png">
</p><br>
As an example, goodmux.v is simulated with the testbench tb_goodmux.v.

```
cd verilog_files
iverilog good_mux.v tb_good_mux.v
./a.out
gtkwave tb_good_mux.vcd
```

<p align="center">
  <img width=""1000 height="250" src="https://github.com/adityasingh6256/Workshop-on-RTL-Design-and-Synthesis-with-sky-130Tech/blob/8437307664d3bc875ef8dc67c804d822fc7cb91f/images/Pic3.png">
</p><br>
