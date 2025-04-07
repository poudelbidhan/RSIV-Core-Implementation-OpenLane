

# Table of Content 


|Days      |         Content|
|------------------------------------|---------------------------------------------------------------|
|[Day 0](/README/Day0.md)| Work Environment Step up  & Tool Installation                                    |
|[DAy 1](/README/Day1.md) | Introduction to Verilog RTL design and Synthesis |
|[Day 2](/README/Day2.md) | Timing libs, Hierarchical vs. Flat Synthesis, Flip-Flop coding styles |
|[Day 3](/README/Day3.md) | Combinational and Sequential Optimization |
|[Day 4](/README/Day4.md) |Gate Level Simulation (GLS) and Synthesis-Simulation mismatch |
|[Day 5](/README/Day5.md) | C code compilation using gcc and RISC-V compilers |
|[Day 6](/README/Day6.md) | RISC_V Design Synthesis and Gate Level Simulation |
| [Day 7 ](/README/Day7.md) | [Introduction to STA](/README/Day7.md) <br>[STA Results](/README/Day7.2.md)| 
| [Day 8 ](/README/Day8.md) | Advanced SDC and Synthesis |
| [Day 9](/README/Day9.md) | PVT Corner Analysis (Post-Synthesis Timing) of the RISC-V CPU Design |
| [Day 10](/README/Day_10.md) | Familiarization with OpenLANE flow | 
| [Day_11](/README/Day_11.md) | Floorplanning |
| [Day_12](README/Day_12.md ) | Placement |
| [Day_13](README/Day_13.md) |  Library Cell design using Magic and Characterization using Ngspice |
| [Day_14](README/Day_14.md) | Integrating Custom Inveter Cell in the OpenLane Flow | 
| [Day_15](README/Day_15.md) | RTL To GDS Flow of RISC_V design on OpenLane2 with Post Synthesis PVT timing |









## Tool Installation 
### System Information
1. OS: Ubuntu 22.04
2. RAM: 8 GB
3. Storage: 100 GB
4. Processor: 4 Core



### Yosys: Synthesis

```sh
sudo apt-get update
git clone https://github.com/YosysHQ/yosys.git
cd yosys
sudo apt install make # If make is not installed please install it
sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
make config-gcc
make 
sudo make install
```
![Screenshot from 2024-06-06 20-50-06](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/cdb64531-ef3f-4d21-876b-dc78a66a2c56)

### iVerilog

```
sudo apt install iverilog
iverilog -v

```



![Screenshot from 2024-06-06 21-19-24](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/fe6a9b25-1ce5-4b62-a794-a58204a7db8f)



### GTKWave
```
sudo apt install gtkwave
gtkwave
```
![Screenshot from 2024-06-06 21-31-09](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/3591863c-a35f-4237-ba05-f542f9ca4217)


## ASIC Design Flow
The ASIC (Application-Specific Integrated Circuit) design flow is a multi-step process used to design and manufacture a custom integrated circuit tailored for a specific application. Here's an overview of the key steps involved in the ASIC design flow

### 1. Specification and Requirements:

* Define the functionality, performance, power, area, and cost requirements of the ASIC.
* Create a detailed specification document outlining the design goals and constraints.
  
### 2. Architectural Design:

* Develop a high-level architecture of the ASIC, including block diagrams and system-level design.
* Perform initial simulations to validate the architecture against the specifications.

### 3. RTL Design:

* Write the Register Transfer Level (RTL) code using hardware description languages (HDLs) like Verilog or VHDL.
* Describe the logic and functionality of the ASIC at the register transfer level.

### 4. Functional Verification:

* Verify the RTL code through simulation to ensure it meets the functional requirements.
* Use testbenches, assertions, and coverage metrics to validate the design.
  
### 5. Synthesis:
* Convert the RTL code into a gate-level netlist using synthesis tools.
* Optimize the design for area, timing, and power during synthesis.

### 6. Design for Test (DFT):
* Incorporate test structures like scan chains and Built-In Self-Test (BIST) into the design.
* Ensure the design is testable for manufacturing defects.
  
### 7. Floorplanning:

* Define the physical layout of the ASIC, including the placement of major functional blocks.
* Plan the power and clock distribution networks.
  
### 8. Placement and Routing:
* Place the standard cells and macros within the defined floorplan.
* Route the interconnections between cells while meeting timing and design rule constraints.

### 9. Static Timing Analysis (STA):

* Perform timing analysis to ensure the design meets the required timing constraints.
* Identify and fix timing violations in the design.
  
### 10. Power Analysis:
* Analyze the power consumption of the ASIC.
* Optimize the design to meet power requirements and mitigate power-related issues.

### 11. Physical Verification:

* Verify the physical design against design rules (DRC) and layout vs. schematic (LVS) checks.
* Ensure the design is manufacturable and free of physical design errors.

### 12. Sign-off and Tape-out:
* Perform final sign-off checks, including timing, power, and physical verification.
* Generate the final GDSII or OASIS file for tape-out, which is sent to the foundry for manufacturing.

### 13. Fabrication:
* The ASIC is manufactured in a semiconductor fabrication plant (foundry).
* Process steps include wafer fabrication, die preparation, packaging, and testing.

 ### 14. Post-Silicon Validation and Testing:

* Test the fabricated ASICs to ensure they meet the design specifications and functional requirements.
* Perform validation in real-world scenarios and environments.

### 15. Production and Deployment:
* Once validated, the ASIC is produced in volume and deployed in the target application.
* Continuous monitoring and testing may be conducted to ensure long-term reliability and performance.


Each step in the ASIC design flow is iterative and may require multiple cycles of design, verification, and optimization to achieve the desired outcome.





## Day 1: Introduction to Verilog RTL Design and Synthesis
### Functional Simulation of RTL Design Using iverilog and rtkwave

1. Clone the GitHub repo with skywater130-based library files and example designs with corresponding test benches.
    ```
    git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
    ```
2. Use iverilog to read and interpret source and testbench file and generate a compiled output. 
    Here we are using good_mux.v as an example design file.
  
           iverilog good_mux.v tb_good_mux.v
   
4. The compiled output file is then executed to perform verilog simulation which generates .vcd file.

        ./a.out

5. Generated vcd files can be viewed using gtkwave
   
       gtkwave tb_good_mux.vcd

    
![Screenshot from 2024-06-14 06-41-57](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/bdfe72fa-81f3-40c0-a6e4-807e9dcbb577)


### Logic Synthesis using Yosys
Here we will perform gate-level synthesis of our simulated example design using Yosys and Sky130 library file
1. Invoke Yosys shell
   
       yosys

2. Read the libraray file

        read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib

3. Read Design File

       read_verilog good_mux.v

4. Perform the Synthesis

       synth -top good_mux

5. Generate the gate-level Netlist

       abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
![Screenshot from 2024-06-14 12-49-53](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/ffa42d42-8dfd-408c-a662-27f189aefb5c)


6. Graphical Diagram realized by the tool

       yosys> show

![Screenshot from 2024-06-14 07-47-13](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/1cf08dab-fdc2-4e32-bf09-5d4369bb6c04)

7. Generate output Netlist

       write_verilog -noattr good_mux_netlist.v

    Generated Netlist:
   
![Screenshot from 2024-06-14 12-58-30](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/e853522d-c84e-4a23-9f9b-e52d8e32f859)




## Day 2: Timing libs, Hierarchical vs. Flat Synthesis, Flip-Flop coding styles

### Hierarchical vs. Flat Synthesis
Here we observe how Yosys tool performs synthesis and generates the netlist for multi-modules with and without preserving the design hierarchy. 

1. Hierarchical Synthesis

        read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
        read_verilog multiple_modules.v
        synth -top multiple_modules
        abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
        write_verilog -noattr multiple_modules_hier.v
        show -stretch multiple_modules
        show sub_module1
        show sub_module2

Synthesis preserving Hierarchy 

![Screenshot from 2024-06-15 07-12-20](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/63355063-ed76-40ce-8a7a-4dffa290ffff)

![Screenshot from 2024-06-15 07-12-45](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/dc626e92-a84c-467a-a465-4066a89e88b1)

![Screenshot from 2024-06-15 07-13-11](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/935cac03-6372-48cf-b153-2ea66d7bc814)

2. Flattened

       flatten
        write_verilog -noattr multiple_modules_flat.v
        show -stretch multiple_modules

![Screenshot from 2024-06-15 07-19-51](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/e5fc1996-d072-4974-b8f3-aed6b54319e0)




## Day 3: Combinational and Sequential Optimization 

### Combinational Logic Optimization

1. lab1 : opt_check.v
    
                             
        module opt_check (input a , input b , output y);
                assign y = a?b:0;
        endmodule

Synthesis Result
![Screenshot from 2024-06-20 19-40-58](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/e30e827c-81c0-4e72-bd98-5703037fe754)


2. lab2 : opt_check2.v


synthesis Result: 
![Screenshot from 2024-06-20 19-44-50](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/795d00b8-5256-49b8-97d5-d25bd8f3323f)


3. lab3: opt_check3.v

Synthesis Result: 
![Screenshot from 2024-06-20 19-47-15](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/94e1719f-23d6-474a-99df-91ff6398bb3d)


4. lab 4:

Synthesis Result: 
![Screenshot from 2024-06-20 19-59-33](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/9a8eb8bf-a55b-4e34-a80b-521cd224358d)


5. lab 5:

Synthesis Result: 

![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/f8d8143d-4929-4fa9-b428-837a90b9aed7)



6. lab 6;
![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/e9e2cf19-4dbc-4590-8c7c-eba2ddf0b837)




### Sequential Logic Optimization 

lab1. dff_const1.v

Simulation Result 
![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/dfe2a5aa-9832-478c-bb4b-a0d58bdf77c0)


Synthesis Result: 

![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/49765ce4-6aeb-428e-9065-fb6affe935da)

        
lab2 : dff_const2.v

Simulation Result 

![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/2444420d-c5c8-44c0-8298-1be7bf6e3369)



Synthesis Result: 

![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/99396dbb-6fa0-4124-827a-2426285f8345)


lab3: dff_const3.v

simulation Result
![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/2c9aebb0-28ae-47a3-9dcb-a7b09e5c3456)


Synthesis Result
![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/ed67ec45-c022-46be-b641-edb8fa208915)


lab4 : dff_const4.v

Simulation Result 

![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/77e3b51b-766f-4978-a914-29388356c900)


Synthesis Result
![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/15562af8-5d83-467a-a7dc-abbeb5227577)


lab 5: dff_const5.v
Simulation Result: 
![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/b064f121-f2bd-4966-8f08-46c85baeda81)


Synthesis Result: 
![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/1f427922-13c4-45ab-928a-6615e97478a6)



lab 6: Counter_opt.v

Simulation Result
![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/24b89303-711d-44d9-bd61-2ab61c176c1b)


Synthesis Result
![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/28f0fbf4-d28a-4e1d-81fb-ad27733c20b2)








## Day 4: Gate Level Simulation (GLS) and Synthesis-Simulation mismatch

lab1: ternary_operator_mux.v 

Simulation Result
![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/c7a54d5c-aa9f-4dd2-8c80-409a605d6f8e)


Synthesis Result: 

![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/1e82486a-d557-423a-970b-b982b899bca9)

GLS Simulation Result : 
![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/09045fac-d818-4747-9c8b-3e98c62da959)





lab2 : bad_mux.v 
RTL Simulation : 
![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/5bb03538-1f00-4788-ab00-91204bc6d619)


Synthesis Result: 

![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/9012430f-3970-4bc6-a3fb-113c7a478b46)


GLS Result: 
![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/8e2412a1-c03c-420e-ba27-d108daceca47)



lab: blocking_caveat.v 

RTL Simulation: 
![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/4df0c4df-233c-450d-9a27-1c13a9138b84)


Synthesis Result: 

![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/941144b9-ab81-438a-8377-b77dcdb9c9b8)


GLS Result: 
![image](https://github.com/poudelbidhan/VSD-HDP/assets/69006235/64972f06-694a-4305-8a2f-88168870325e)

