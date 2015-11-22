
## 11g建库遇到/dev/shm太小的告警  

今天尝试手动建库，设置了memory\_target，然后启动后提示/dev/shm，  
查了下资料，从11g开始，引入了一个自动内存管理(AMM)特性，  
该特性需更多的共享内存(/dev/shm)，必须确保共享内存大于MEMORY\_MAX\_TARGET 和MEMORY\_TARGET(这俩即自动内存管理对应的初始化参数)。   

解决办法以增大共享内存为例，减小memory\_target就不举例了。  
df -h  
cat /etc/fstab|grep shm  
tmpfs  /dev/shm   tmpfs   defaults     0 0
在defaults后面加上,size=2g，保存退出。  
重新挂载，使生效。  
mount -o remount /dev/shm  

再查一下看起来是生效了，怪就怪在重启后竟然失效了。   
再百度一下，原来，这个问题应该是系统的一个bug，    
在redhat的bugzilla中可查（ https://bugzilla.redhat.com/show_bug.cgi?id=669700 ），  
针对这个也有一个解决办法，如下：  

编辑/etc/rc.d/rc.sysinit  

#vim /etc/rc.d/rc.sysinit  

修改前： mount -f /dev/shm >/dev/null 2>&1  

修改后：mount /dev/shm >/dev/null 2>&1  
