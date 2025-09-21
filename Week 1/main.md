# LAB 1


``` bash
$ sudo -i
$ mkdir VLSI
$ cd VLSI
$ git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
$ ls            # You should see a folder named 'sky130RTLDesignAndSynthesisWorkshop'
$ cd sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/

# To run the Iverilog simulator, use the following command:
$ iverilog good_mux.v tb_good_mux.v

# You should see './a.out' file after running 'ls' command.

$ ./a.out        # Gives the follwoing output: VCD info: dumpfile tb_good_mux.vcd opened for output.

# To view the waveform using GTKWave, use the following command:
$ gtkwave tb_good_mux.vcd
```
