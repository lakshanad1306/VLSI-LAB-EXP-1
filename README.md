# Simulation and Implementation of Logic Gates, Adder and Subtractor
AIM: To simulate and synthesis Logic Gates,Adders and Subtractor using Xilinx ISE.

APPARATUS REQUIRED: Vivado 2023.1

PROCEDURE: 
1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

Logic Diagram :

Logic Gates:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/ee17970c-3ac9-4603-881b-88e2825f41a4)


Half Adder:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/0e1ecb96-0c25-4556-832b-aeeedfdfe7b9)


Full adder:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/9bb3964c-438f-469d-a3de-c1cca6f323fb)


Half Subtractor:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/731470b7-eb4e-49f8-8bb7-2994052a7184)


Full Subtractor:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/d66f874b-c1f2-44b3-a035-7149b56430c1)


8 Bit Ripple Carry Adder

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/7385a408-40a5-4203-8050-b72818622d79)


VERILOG CODE:
# Full Adder:
```
module fulladder (sum, cout, a,b,c);
input a,b,c;
output sum, cout;
wire w1,w2,w3,w4,w5;
xor x1(w1,a,b);
xor x2(sum,w1,c);
and al(w2,a,b);
and a2(w3,b,c);
and a3(w4,a,c);
or o1(w5,w2,w3); or o2(cout,w5,w4);
endmodule
```
# Full Subractor:
```
module full_subtractor(a, b, c,D, Bout);
input a, b, c;
output D, Bout;
assign D = a^b^c;
assign Bout = (~a & b) | (~(a^ b) & c);
endmodule
```

# Half Adder:
```
module half_adder(a,b,sum,carry);
input a,b;
output sum,carry;
or(sum,a,b);
and(carry,a,b);
endmodule
```

# Half Subractor:
```
module half_subtractor(D,Bo,A,B);
input A,B;
output D,Bo;
assign D=A^B;
assign Bo=(~A)&B;
endmodule
```
# Logic Gates:
```
module logicgates(a,b,andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate);
input a,b;
output andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate;
and(andgate,a,b);
or(orgate,a,b);
xor(xorgate,a,b);
nand(nandgate,a,b);  
nor(norgate,a,b);
xnor(xnorgate,a,b);
not(notgate,a);
endmodule
```
# Ripple Carry Adder 4Bit:
```
module rippe_adder(S, Cout, X, Y,Cin);
 input [3:0] X, Y;// Two 4-bit inputs
 input Cin;
 output [3:0] S;
 output Cout;
 wire w1, w2, w3;fulladder u1(S[0], w1,X[0], Y[0], Cin);
 fulladder u2(S[1], w2,X[1], Y[1], w1);
 fulladder u3(S[2], w3,X[2], Y[2], w2);
 fulladder u4(S[3], Cout,X[3], Y[3], w3);
endmodule
module fulladder(S, Co, X, Y, Ci);
  input X, Y, Ci;
  output S, Co;  
  wire w1,w2,w3;  
  xor G1(w1, X, Y); 
  xor G2(S, w1, Ci);
  and G3(w2, w1, Ci);
  and G4(w3, X, Y);
  or G5(Co, w2, w3);
endmodule
```
# Ripple Carry Adder 8bit
```
module fulladder(a,b,c,sum,carry);
input a,b,c;
output sum,carry;
wire w1,w2,w3;
xor(w1,a,b);
xor(sum,w1,c);
and(w2,w1,c);
and(w3,a,b);
or(carry,w2,w3);
endmodule

module rca_8bit(a,b,cin,s,cout);
input [7:0]a,b;
input cin;
output [7:0]s;
output cout;
wire [7:1]w;
fulladder f1(a[0], b[0], cin, s[0], w[1]);
fulladder f2(a[1], b[1], w[1], s[1], w[2]);
fulladder f3(a[2], b[2], w[2], s[2], w[3]);
fulladder f4(a[3], b[3], w[3], s[3], w[4]);
fulladder f5(a[4], b[4], w[4], s[4], w[5]);
fulladder f6(a[5], b[5], w[5], s[5], w[6]);
fulladder f7(a[6], b[6], w[6], s[6], w[7]);
fulladder f8(a[7], b[7], w[7], s[7], cout);
endmodule
```

# OUTPUT:

# Full Adder
![Screenshot 2024-04-04 214228](https://github.com/lakshanad1306/VLSI-LAB-EXP-1/assets/161121355/5861d9cc-f439-4d6f-9637-e207327496d9)

<img width="632" alt="image" src="https://github.com/lakshanad1306/VLSI-LAB-EXP-1/assets/161121355/77971412-b208-47e6-a7a3-83ed932000c4">


# Full Subractor
![Screenshot 2024-04-04 214258](https://github.com/lakshanad1306/VLSI-LAB-EXP-1/assets/161121355/9cba1528-e76b-488b-b225-a2d1d1719521)

<img width="490" alt="image" src="https://github.com/lakshanad1306/VLSI-LAB-EXP-1/assets/161121355/2fb76565-dba4-4d30-8307-ddbd07374350">


# Half Adder
![Screenshot 2024-04-04 214327](https://github.com/lakshanad1306/VLSI-LAB-EXP-1/assets/161121355/ef26f9ed-47ad-465f-abba-e1c83fcd7ae4)

![Screenshot 2024-04-22 135737](https://github.com/lakshanad1306/VLSI-LAB-EXP-1/assets/161121355/f80953ae-1db6-4e23-a04b-ace1dfedbebe)


# Half Subractor
![Screenshot 2024-04-04 214348](https://github.com/lakshanad1306/VLSI-LAB-EXP-1/assets/161121355/bd30eda2-6717-4c26-9457-4ab8c7ae86c4)

<img width="488" alt="image" src="https://github.com/lakshanad1306/VLSI-LAB-EXP-1/assets/161121355/fcf37701-b2ac-4d85-905e-b593841d4afe">


# Logic Gates
![Screenshot 2024-04-04 214410](https://github.com/lakshanad1306/VLSI-LAB-EXP-1/assets/161121355/2d24d1a6-a293-41ef-b8a9-e84471cd9c54)

<img width="556" alt="image" src="https://github.com/lakshanad1306/VLSI-LAB-EXP-1/assets/161121355/51100cd9-c792-4faa-9c9b-1b5de2260066">


# Ripple Carry Adder 4bit
![Screenshot 2024-04-04 214432](https://github.com/lakshanad1306/VLSI-LAB-EXP-1/assets/161121355/a9e07040-1295-4b54-a60d-59b0c8ad9f5c)

<img width="632" alt="image" src="https://github.com/lakshanad1306/VLSI-LAB-EXP-1/assets/161121355/ea7e9859-5a42-45f4-aaec-bfd7efeece9c">


# Ripple Carry Adder 8bit
![Screenshot 2024-04-04 214457](https://github.com/lakshanad1306/VLSI-LAB-EXP-1/assets/161121355/5c0ad9e4-b9ae-40e9-8036-98295a896dea)

<img width="631" alt="image" src="https://github.com/lakshanad1306/VLSI-LAB-EXP-1/assets/161121355/517604ec-80d3-406b-917b-37d8927487f1">


# RESULT

Thus the simulation and synthesis Logic Gates,Adders and Subtractor using VIVADO 2023.2 has been verified.







  












