# pes_elevator
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

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/fd8711f8-028c-456e-bfba-9244ac58acd6)


