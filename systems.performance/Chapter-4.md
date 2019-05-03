# Observability Tools
## Counters
- vmstat: virtual and physical memory statistics, system-wide
- mpstat: per-CPU usage
- iostat: per-disk I/O usage, reported from the block device interface
- netstat: network interface statistics, TCP/IP stack statistics, and some per- connection statistics
- sar: various statistics; can also archive them for historical reporting

```shell
$ vmstat 1 3
procs -----------memory---------- ---swap-- -----io---- -system-- ----cpu----
    r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa
   40 0 34455620 111396 13438564 0
40 0 34458684 111396 13438588 0 0 0 0 2223 15198 13 11 76 0 40 0 34456468 111396 13438588 0 0 0 0 1940 15142 15 11 74 0
```
These tools typically read statistics from the /proc file system.

## Tracing

- tcpdump: network packet tracing (uses libpcap)
- snoop: network packet tracing for Solaris-based systems
- blktrace: block I/O tracing (Linux)
- iosnoop: block I/O tracing (DTrace-based)
- execsnoop: tracing of new processes (DTrace-based)
- dtruss: system-wide buffered syscall tracing (DTrace-based)
- DTrace: tracing of kernel internals and the usage of any resource (not just network or block I/O), using static and dynamic tracing
- SystemTap: tracing of kernel internals and the usage of any resource, using static and dynamic tracing
- perf: Linux Performance Events, tracing static and dynamic probes

## Observability Sources
Type|Linux|
-|-|
Per-process counters|/proc|
System-wide counters|/proc, /sys|
Device driver and debug info|/sys|
Per-process tracing|ptrace, uprobes|
CPU performance counters|perf_event|
Network tracing|libpcap|
Per-thread latency metrics|delay accounting|
System-wide tracing|tracepoints, kprobes, ftrace|

### /proc
```shell
[root@host~]# ls -F /proc/19954/
attr/      auxv    clear_refs  comm             cpuset  environ  fd/      gid_map  limits    map_files/  mem        mounts      net/  numa_maps  oom_score      pagemap      projid_map  sched      sessionid  smaps  stat   status   task/   uid_map
autogroup  cgroup  cmdline     coredump_filter  cwd@    exe@     fdinfo/  io       loginuid  maps        mountinfo  mountstats  ns/   oom_adj    oom_score_adj  personality  root@       schedstat  setgroups  stack  statm  syscall  timers  wchan
```
- limits: in-effect resource limits  
- maps: mapped memory regions  
- sched: various CPU scheduler statistics  
- schedstat: CPU runtime, latency, and time slices  
- smaps: mapped memory regions with usage statistics  
- stat: process status and statistics, including total CPU and memory usage  
- statm: memory usage summary in units of pages  
- status: stat and statm information, human-readable  
- task: directory of per-task statistics  