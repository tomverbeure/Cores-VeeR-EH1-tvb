

* Compile `veer_sim.cpp` with g++ 11.3:

	`time g++ -I `yosys-config --datdir`/include veer_sim.cpp -o veer_sim.o`

	Aborted after 3 hours. Used 15GB at the time.

* After reading into Yosys

   ```
   Number of wires:              69893
   Number of wire bits:         366723
   Number of public wires:       26592
   Number of public wire bits:  182483
   Number of memories:              36
   Number of memory bits:       5895424
   Number of processes:           1569
   Number of cells:              39878
     $add                          583
     $and                        15570
     $eq                          6847
     $ge                             7
     $gt                             6
     $logic_not                   2154
     $lt                            15
     $memrd                         36
     $mul                          198
     $mux                         2742
     $ne                           133
     $not                         3491
     $or                          6030
     $reduce_and                   401
     $reduce_or                    344
     $reduce_xor                    31
     $shiftx                       237
     $shl                           36
     $shr                           15
     $sshr                           4
     $sub                           90
     $xnor                           8
     $xor                          900
   ```

* synth_ecp5

    Default configuration

    ```
=== veer_wrapper ===

   Number of wires:              76281
   Number of wire bits:         277359
   Number of public wires:       76281
   Number of public wire bits:  277359
   Number of memories:               0
   Number of memory bits:            0
   Number of processes:              0
   Number of cells:              97534
     CCU2C                         868
     DP16KD                        372
     L6MUX21                      4034
     LUT4                        64311
     MULT18X18D                      7
     PFUMX                       13716
     TRELLIS_FF                  14226
    ```
