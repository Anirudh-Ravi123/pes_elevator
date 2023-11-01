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

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/db0c7b68-d391-42c4-8e24-cddd247eaeac)



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

**SYNTHESIS**
To run synthesis:```run_synthesis```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/4f1231e0-75b9-4883-a7f7-67e8bb856810)


Results:

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/994bcf26-f951-4bc7-9a18-6a178cc18fa1)


**Slack after synthesis**

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/bf01cdee-fce0-4511-bd76-092a03aec2bd)


**FLOORPLAN**
Command to run floorplan:```run_floorplan```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/0fcd7177-06cd-4bfe-9a3c-703ad95ef374)


Results:

Core and Die area

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/ce350044-13ff-4efa-87f5-eb6a150cd297)


To view the design we type 

```
magic -T /home/anirudhravi/OpenLane/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def pes_elevator.def &
```
![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/494e750f-0fdf-4245-8c30-770b74fed303)


![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/680ce772-8214-4ad5-ab15-34fb6c5b7115)


**PLACEMENT**
Command to run placement:```run_placement```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/8f1c5adf-6803-4cd8-9707-40c2fe1e1d8d)


Results

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/b9dc5ee4-0aa1-4b0d-b899-bdc78998c895)


To view the design we type 

```
magic -T /home/anirudhravi/OpenLane/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def pes_elevator.def &
```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/86564e99-da74-49ad-905c-a35474e4e26a)


**CTS(CLOCK TREE SYNTHESIS)**
Command to cts:```run_cts```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/f214277f-8c96-43d8-922f-d55f184af199)


Results

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/be1a6f7e-ec58-4cd0-b9da-170d4fdab444)


![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/2ff42620-ee0d-4bcf-8d87-e8f061db927e)


![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/a2d0336c-8f21-44d4-93fd-abcdeb32b737)



**ROUTING**
Command to run routing:```run_routing```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/c1d5c7a5-19ff-41d2-8967-cefdf7af9861)


Results


![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/692e1278-8e43-4bff-a1b1-0f8f566c9418)


![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/08ae2e72-e882-4898-a2df-dddee590fbfe)


![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/3622cdb7-c22f-4188-aed1-329d95b5af3c)


To view the design we type 

```
magic -T /home/anirudhravi/OpenLane/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def pes_elevator.def &
```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/7b9ac352-3db2-4104-a05c-592ce96eac59)


![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/46085d73-72ad-40d0-b465-ed23031dade6)


![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/c8def5d2-f0d0-427a-8930-d89d57cd916a)


![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/004d2de2-0abf-4131-a37b-7055f08ff07b)


**STATISTICS**

- Internal Power = 1.38e-05  W
- Switching Power = 6.58e-06 
- Leakage Power =  6.46e-10
- Total Power =  2.04e-05
