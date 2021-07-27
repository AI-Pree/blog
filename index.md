# OS Kernel
This OS is created to run on the RISC-V ISA computers.

## OS interface

### Issue in the DRAM, no optimisation for Data retention
Only for volatile Memory.

Usually memory controller handles the recharging of the capacitors in the row cell of the DRAM bank. The cell are recharged every 64ms (depends on the DRAM ). This will consume  high amount of energy and create high performance overhead, as memory cant be used during the recharge process. The time it would spend recharging the cells is based on the capacity of the DRAM. As larger number of capacitor are needed to enable the higher capacity DRAM, the size of capacitor are reduced to fit in the DRAM, which means the amount of  energy that can be stored in the capactior significantly decreases. As a result, leaks(when cells starting losing the data stored in it) occurs frequtly under short amount of time in the capacitor. DRAM manufacturing companies will usually  increase the the refresh rate(how often the capacitors are recharged), which again creates huge overhead in the perfomance of the  DRAM.

Failure to recharge the memory would create leaks on the capacitor of the cell. This will be issue while retaining the data from the DRAM memory (as data will lost). However, this is only for the volatile memory. In contrast, this wouldnt be an issue in new non-volatile DRAM memory.

The leak issue with the capacitor in the cell of the DRAM bank, as mentioned earlier, whole row cells are rehcarged instead of only the allocated cells. This is the current standard practices.

In the system software level, creating a OS interface for the memory controller so that we can assign memory controller to recharge only the regions (bank cells) that are allocated.

Although this approach, will solve the issue to some extent, it would'nt be optimal when all the cells in the memory bank are allocated.

Another solution, to tackle this problem is by time profiliing the retention of the DRAM bank cells. So, we can profile each of the individual cells and decide time interval for recharging individual row. The reason that we will not be recharging based on indiviual cell is that not every cells has same capacity, while one's capacitor can have lower leak life span than its correspondng cells in the row. This will provide us with a better insight on when to recharge each individual row in the memory bank.

However, you need to be careful while analysing the profiling of the rentention time and understanding the tradeoffs while trying to implement the solution. For instance, the power consumption, performance, accuarcy of the refresh time for each row based on the analysed profile metrics. One of the downside would be conjectural analysis causing leaks in the capacitor.

### Retriving object life time from the compiler
OS Kernel can also retrive the object life time of the application from the compiler (most of the compiler that has garbage collector already implements it) and tell the memory controller to refresh particular row in the memory bank based on the life span of the data object used by the application. Also, the memory controller can skip refreshing the particular row that has data object life span shorter than the refresh time of the DRAM cells capacitor itself.

## References


