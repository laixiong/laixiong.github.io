
## 11g建库遇到/dev/shm太小的告警  

今天尝试手动建库，设置了memory_target，然后启动后提示/dev/shm，查了下资料，从11g开始，引入了一个自动内存管理(AMM)特性，该特性需更多的共享内存(/dev/shm)，必须确保共享内存大于MEMORY_MAX_TARGET 和MEMORY_TARGET(这俩即自动内存管理对应的初始化参数)。   

解决办法以增大共享内存为例，减小memory_target就不举例了。  
df -h  
cat /etc/fstab|grep shm  
tmpfs  /dev/shm   tmpfs   defaults     0 0
在defaults后面加上,size=2g，保存退出。  
重新挂载，使生效。  
mount -o remount /dev/shm  
