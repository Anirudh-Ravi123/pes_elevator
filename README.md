# pes_elevator
## Iverilog simulation
Commands
```
iverilog pes_elevator.v pes_elevator_tb.v
./a.out
gtkwave pes_elevator_tb.vcd
```
![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/1491d594-0fb4-4d98-b512-d22ec937c68e)

WAVEFORM 

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/53675f81-056f-4475-825e-b9da7692f501)


**yosys simulation**


Commands

```
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog pes_elevator.v
synth -top pes_elevator
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/c4556d32-9afd-4bda-b636-dd1a187eb9af)


![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/91bf1d31-bed7-4e36-8993-3d748544990d)


**design**
![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/b51e85b3-ac9b-475a-8de8-182fd30c6e8e)



Generating the netlist

Commands
```
write_verilog -noattr pes_elevator_net.v
```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/e00d30d5-3db7-46f2-9387-27cce8550b4e)

## GLS 

Commands
```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v pes_elevator_net.v pes_elevator_tb.v
./a.out
gtkwave pes_elevator_tb_net.v
```

![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/08ad123a-6796-4583-a945-dd6ee2f42e6e)


**WAVEFORM**
![image](https://github.com/Anirudh-Ravi123/pes_elevator/assets/142154804/2df22afb-ba31-4fd7-b29b-87b81d044011)


