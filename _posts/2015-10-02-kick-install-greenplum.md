##kick install greenplum cluster

从今天开始，作为晚上个人修炼项目，我将尝试执行一键安装包，其中greenplum是第一个。  

每个项目都会同步到我的github，这里只是记录遇到的一些问题。  

github url: [kick-install-greenplum](https://github.com/laixiong/kick-install-greenplum)


**环境**：  
centos 6.3

**节点分布**：  
192.168.19.71 ksgp1	 gploader	gpmaster  
192.168.19.72 ksgp2	gpseg1  
192.168.19.73 ksgp3	gpseg2  
192.168.19.74 ksgp4	gpseg3  

**依赖：**  
各节点已安装expect RPM包。

日志：  
2015-10-01 经过一天的努力，终于将各节点的ssh信任搞定了。  
目前只写了prepare.sh 和ssh_expect两个脚本，功能还不是很完善。  

