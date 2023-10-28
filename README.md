# pes_elevator
Elevator controllers are sophisticated electronic systems designed to manage the movement, safety, and efficiency of elevators within buildings.They serve as the central intelligence behind vertical transportation systems, seamlessly integrating hardware and software to ensure smooth, safe, and efficient operation of elevators within buildings.It is designed to manage the movement and status of an elevator. 

Elevator controller has been designed for a 8 story building. It takes input signals for the requested floor, current floor, clock, reset, and conditions indicating prolonged door opening or excessive weight.The module determines the elevator's direction, current floor, and operational status based on these inputs. It features safety checks: if the elevator door is open for more than 3 minutes, a door alert is triggered, and if the elevator is overloaded, a weight alert is activated.The module outputs signals indicating the elevator's direction, operational status, door alert, weight alert, and the current floor. It provides a versatile and essential component for elevator control systems.

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/154a3bfb-7d16-4158-9be2-c5ca665e7e53)


## Iverilog simulation
Commands
```
iverilog pes_elevator.v pes_elevator_tb.v
./a.out
gtkwave pes_elevator_tb.vcd
```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/deb58f7a-ede0-41a1-9c10-ba6c871e550c)


WAVEFORM 

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/da83baa3-b6d5-4a15-8873-ab938ff4a069)


## GLS 

**yosys simulation**


Commands

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog pes_elevator.v
synth -top pes_elevator
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/67361018-03fd-48ac-af62-912d207355f4)


![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/8e5634f0-5e0d-4a81-acce-80dc4caf489e)


**design**

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/bd91b7fc-aa57-44a5-ab05-36fda0aeef81)



Generating the netlist

Commands
```
write_verilog -noattr pes_elevator_net.v
```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/7f140452-4277-4270-b7eb-757ff7524e05)


**Verification**


Commands
```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v pes_elevator_net.v pes_elevator_tb.v
./a.out
gtkwave pes_elevator_tb_net.v
```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/72c5fa8d-92ab-48d8-a57c-7f38181686b8)


**WAVEFORM**

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/49477b8e-42b3-441a-a524-742bf2907ce1)

The synthesis  and simulation waveforms are matching.



# Openlane 

First create a folder with the project name in the designs folder and add the congif.json file and the verilog file to the folder. Create a src folder within the design folder and add all the libraries required.

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/54fa3b88-bf6a-41be-b0f3-c9bff6a07863)

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/5c2c6e01-80bf-496f-a133-70fafdc6b9a7)


![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/523506b2-7c75-4790-b038-989622ce0a3d)



Contents of config.json file

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/60f2bf9c-1236-49eb-9ec5-a9d2d374ede9)


Now we navigate to the openlane directory in terminal and run the commands 

```
make mount
./flow.tcl -interactive
```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/67c057bb-b224-4c01-8a75-7b614c3d3f55)


To run the design we run the command
```
prep -design pes_elevator
```
For synthesis:```run_synthesis```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/11a1d586-5b85-4b97-80ff-88df450f01e1)


Results:

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/3e0124a9-583a-4ce8-95cb-00af8cfe9f23)


**Slack after synthesis**

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/a37a5089-c5f5-4393-ab80-1fa56878b22b)

