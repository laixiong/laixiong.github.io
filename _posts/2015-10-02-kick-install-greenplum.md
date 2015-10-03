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
2015-10-01   
经过一天的努力，终于将各节点的ssh信任搞定了。  
目前只写了prepare.sh 和ssh_expect两个脚本，功能还不是很完善。  
2个比较难搞的问题：  
a.单行数据去重，比如"hosta hostb hostc hostb hostd hosta"，搞了变天还是要借助于awk的数组
    awk 'BEGIN {RS=ORS=" "}!a[$0]++',要注意的是要在行后手动追加个空格，最后一个会有问题。  
b.expect问题，听说最后要多加一个无关紧要的expect，否则最后一个expect不执行，不知道真假啊，反正加一个吧，
但我怀疑是以为说这话的是没有加exp_continue,我就遇到过脚本里没加，怎么都跑不通，最后这个timeout之后怎么捕获error code还是没学会。

2015-10-03
判断集群中的系统版本是否一致，提示too many arguments,原来下面的命令有空格，要加""或者将[]改成[[]]
	osVersion=`cat /etc/redhat-release`

