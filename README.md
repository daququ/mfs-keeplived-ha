# mfs-keeplived-ha

High Availability Of MooseFS Master


最简单的实现mfs高可用，2台机器都分别装（moosefs，keeplived），配置其中一台是master，另一个为shadow，
其他集群中的chunk，logger等节点中的mfsmaster ip 都为VI，由keeplived管理VIP，发生切换时，修改mfsmaste.cfg文件，
并重启mfsmaster进程，向网关发送arping尽量减少mfsmater切换时间。


存在问题
* 切换时间至少2秒以上
* 当在100并发写时，发生mfsmaster切换，发生锁现象，不能自动恢复，除非umount，重新启动2个real mfsmaster节点，
发生数据丢失。
