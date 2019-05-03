# CPU 架构
下图是单个处理器了 **四个核**和**八个硬件线程**

<img src="../resources/systems.performance/c6-cpu.png" width = "80%" />  

## MMU

<img src="../resources/systems.performance/c6-mmu.png" width = "80%" />  
MMU负责虚拟地址到物理地址的转换，通过芯片上的TLB缓存地址转换。主存(DRAM)里的转换表，处理缓存未命中的情况。

## 调度器
Linux 2.6.23引入完全公平调度器，使用红黑树取代传统运行队列来管理任务，以任务的CPU时间作为key，这样使得CPU的少量消费者相对与CPU消费型负载均衡更容易被找到，提高了交互I/O消费负载的性能。

## 工具
命令|说明|
-|-|
uptime|检查负载均衡，确认CPU负载是随着时间上升还是下降
vmstat|每秒运行vmstat。检查空闲列|
mpstat|检查单个热点CPU|
top/prstat|查看哪个进程用户CPU消耗大|
pidstat/prestat|把CPU消耗大的分解成用户和系统时间|
perf/dtrace/stap/oprofile|从用户时间或者内核时间角度剖析CPU使用堆栈跟踪|
perf/cpustat|测量CPI|