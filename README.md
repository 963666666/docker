# docker

## 基础技术
### Linux Namespace
  Namespace的API主要使用3个系统调用
  <ul>
    <li>clone()创建新进程。根据系统调用参数来判断哪些类型的Namespace被创建，而且它们的子进程也会被包含到这些Namespace中。</li>
    <li>unshare()将进程移出某个Namespace</li>
    <li>setns()将进程加入到Namespace</li>
  </ul>
  <br/>
  <ul>
    <li>UTS Namespace 主要是用来隔离nodename和domainname两个系统标识。在UTS Namespace里面，每个Namespace允许有自己的hostname</li>
    <li>IPC Namespace用来隔离System V IPC和POSIX message queues。每一个IPC Namespace都有自己的System V IPC和POSIX message queue</li>
    <li>PID Namespace是用来隔离进程ID的。同样一个进程在不同的PID Namespace里可以拥有不同的PID。这样就可以理解，在docker container里面，
    ，使用ps -ef经常会发现，在容器内，前台运行的那个进程PID是1，但是在容器外，使用ps -ef会发现同样的进程却有不同的PID。</li>
    <li>Mount Namespace用来隔离各个进程看到的挂载点视图。在不同的Namespace的进程中，看到的文件系统层次是不一样的。在Mount Namespace中
    调用mount()和umount()仅仅只会影响当前Namespace内的文件系统，而对全局的文件系统是没有影响的。</li>
    <li>User Namespace主要是隔离用户的用户组ID。也就是说，一个进程的User ID和Group ID在User Namespace内外可以是不同的。比较常用的是，
    在宿主机上以一个非root用户运行创建一个User Namespace，然后在User Namespace里面却映射成root用户。</li>
    <li>Network Namespace是用来隔离网络设备、IP地址端口等网络栈的Namespace。Network Namespace可以让每个容器拥有自己独立的（虚拟的）
    网络设备，而且容器内的应用可以绑定到自己的端口，每个Namespace内的端口都不会互相冲突。在宿主机上搭建网桥后，就能很方便地实现容器之间
    的通信，而且不同容器上的应用可以使用相同的端口。</li>
  </ul>