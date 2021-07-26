# OS Kernel


## OS interface

### Issue with the DRAM whole row getting recharged for Data retention
Only for Volation Memory.

Usually memory controller handles the recharging of the capacitors in the row cell of the DRAM bank. The cell are recharged every 64ms (depends on the DRAM ). This will consume  high amount of energy and create high performance overhead, as memory cant be used during the recharge process. The time it would spend recharging the cells is based on the capacity of the DRAM. As larger number of capacitor are needed to enable the higher capacity DRAM, the size of capacitor are reduced to fit in the DRAM, which means the amount of  energy that can be stored in the capactior significantly decreases. As a result, leaks occurs frequtly under short amount of time in the capacitor. DRAM manufacturing companies will usually  increase the the refresh rate(how often the capacitors are recharged), which again creates huge overhead in the perfomance of the  DRAM.

Failure to recharge the memory would create leaks on the capacitor of the cell. This will be issue while retaining the data from the DRAM memory (as data will lost). However, this is only for the volatile memory. In contrast, this wouldnt be an issue in new non-volatile DRAM memory.

The leak issue with the capacitor in the cell of the DRAM bank, as mentioned earlier, whole row cells are rehcarged instead of only the allocated cells. This is the current standard practices.

In the system software level, creating a OS interface for the memory controller so that we can assign memory controller to recharge only the regions (bank cells) that are allocated.



## References


