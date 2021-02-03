https://mp.weixin.qq.com/s?__biz=MzAwMzc4MTExOA==&mid=2649798734&idx=1&sn=057c6137a17fcd1650eb2e744a0325c9&chksm=8331e0dfb44669c9c8f6c5a1adfeaccaf8ca4999f5262ba26cdd7ac541dee409bbc2d7f58acd&mpshare=1&scene=1&srcid=0129uc7hno0Q4seLXt2JWRCe&sharer_sharetime=1611916489458&sharer_shareid=0d5c82ce3c8b7c8f30cc9a686416d4a8#rd
安装方法
Ubuntu/Mint 和 Debin 系统：
本地软件库中有相关安装包，你可以用下面命令安装：
# sudo apt-get install dstat
RHEL/Centos 和 Fedora 系统:
你可以在 romforge 软件库中添加有相关安装包，参照指导，使用如下命令很简单就能进行安装：
# yum install dstat
ArchLinux 系统：
相关软件包在社区资源库中，你可以用这个命令来安装：
# pacman -S dstat
使用方法
dstat 的基本用法就是输入 dstat 命令，输出如下：
这是默认输出显示的信息：
CPU 状态：CPU 的使用率。这项报告更有趣的部分是显示了用户，系统和空闲部分，这更好地分析了 CPU 当前的使用状况。如果你看到 "wait" 一栏中，CPU 的状态是一个高使用率值，那说明系统存在一些其它问题。当 CPU 的状态处在 "waits" 时，那是因为它正在等待 I/O 设备（例如内存，磁盘或者网络）的响应而且还没有收到。
磁盘统计（dsk）：磁盘的读写操作，这一栏显示磁盘的读、写总数。
网络统计（net）：网络设备发送和接受的数据，这一栏显示的网络收、发数据总数。
分页统计（paging）：系统的分页活动。分页指的是一种内存管理技术用于查找系统场景，一个较大的分页表明系统正在使用大量的交换空间，或者说内存非常分散，大多数情况下你都希望看到 page in（换入）和 page out（换出）的值是 0 0。
系统统计（system）：这一项显示的是中断（int）和上下文切换（csw）。这项统计仅在有比较基线时才有意义。这一栏中较高的统计值通常表示大量的进程造成拥塞，需要对 CPU 进行关注。你的服务器一般情况下都会运行运行一些程序，所以这项总是显示一些数值。
默认情况下，dstat 每秒都会刷新数据。如果想退出 dstat，你可以按 "CTRL+C" 键。
需要注意的是报告的第一行，通常这里所有的统计都不显示数值的。
这是由于 dstat 会通过上一次的报告来给出一个总结，所以第一次运行时是没有平均值和总值的相关数据。
但是 dstat 可以通过传递 2 个参数运行来控制报告间隔和报告数量。例如，如果你想要 dstat 输出默认监控、报表输出的时间间隔为 3 秒钟，并且报表中输出 10 个结果，你可以运行如下命令：
# dstat 3 10

在 dstat 命令中有很多参数可选，你可以通过 man dstat 命令查看，大多数常用的参数有这些：
-c：显示 CPU 系统占用，用户占用，空闲，等待，中断，软件中断等信息。

-C：当有多个 CPU 时候，此参数可按需分别显示 cpu 状态，例：-C 0,1 是显示 cpu0 和 cpu1 的信息。

-d：显示磁盘读写数据大小。

-D hda,total：include hda and total。

-n：显示网络状态。

-N eth1,total：有多块网卡时，指定要显示的网卡。

-l：显示系统负载情况。

-m：显示内存使用情况（包括 used，buffer，cache，free 值）。

-g：显示页面使用情况。

-p：显示进程状态。

-s：显示交换分区使用情况。

-S：类似 D/N。

-r：I/O 请求情况。

-y：系统状态。
-t ：将当前时间显示在第一行

--ipc：显示 ipc 消息队列，信号等信息。

--socket：用来显示 tcp udp 端口状态。

-a：此为默认选项，等同于 - cdngy。

-v：等同于 -pmgdsc -D total。
–socket ：显示网络统计数据
–tcp ：显示常用的 TCP 统计
–udp ：显示监听的 UDP 接口及其当前用量的一些动态数据–fs ：显示文件系统统计数据（包括文件总数量和 inodes 值）
–nocolor ：不显示颜色（有时候有用）

--output 文件：此选项也比较有用，可以把状态信息以 csv 的格式重定向到指定的文件中，以便日后查看。例：dstat --output /root/dstat.csv & 此时让程序默默的在后台运行并把结果输出到 /root/dstat.csv 文件中。



当然不止这些用法，dstat 附带了一些插件很大程度地扩展了它的功能。你可以通过查看 /usr/share/dstat 目录来查看它们的一些使用方法，常用的有这些：

-–disk-util ：显示某一时间磁盘的忙碌状况

-–freespace ：显示当前磁盘空间使用率

-–proc-count ：显示正

在运行的程序数量
-–top-bio ：指出块 I/O 最大的进程
-–top-cpu ：图形化显示 CPU 占用最大的进程
-–top-io ：显示正常 I/O 最大的进程
-–top-mem ：显示占用最多内存的进程
举一些例子：
查看全部内存都有谁在占用：
# dstat -g -l -m -s --top-mem


显示一些关于 CPU 资源损耗的数据：
# dstat -c -y -l --proc-count --top-cpu

您可以将多个内部 dstat 插件与外部 dstat 插件一起使用，以查看所有可用插件的列表，请运行以下命令：

$ dstat --list
