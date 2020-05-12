# 平均负载(Load Avg)
    简单来说，平均负载是指单位时间内，系统处于可运行状态和不可中断状态的平均进程数，也就是平均活跃进程数

# cpu 上下文切换
    - cs（context switch）是每秒上下文切换的次数。
    - in（interrupt）则是每秒中断的次数。
    - r（Running or Runnable）是就绪队列的长度，也就是正在运行和等待 CPU 的进程数。
    - b（Blocked）则是处于不可中断睡眠状态的进程数。

# pidstat

# perf

# pstree

# top

    - 用户态 CPU 使用率 （%usr）；
    - 内核态 CPU 使用率（%system）；
    - 运行虚拟机 CPU 使用率（%guest）；
    - 等待 CPU 使用率（%wait）；
    - 以及总的 CPU 使用率（%CPU);
    - 用户（%user）
    - Nice（%nice）
    - 系统（%system）
    - 等待 I/O（%iowait）
    - 中断（%irq）
    - 软中断（%softirq）

# execsnoop

