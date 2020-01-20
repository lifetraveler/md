# command

1. 查看占用端口

   lsof -i tcp:5055

   Centos查看端口占用情况命令，比如查看80端口占用情况使用如下命令：

   lsof -i tcp:80

   列出所有端口

   netstat -ntlp

   1、开启端口（以80端口为例）

   ​      方法一：

   ​         /sbin/iptables -I INPUT -p tcp --dport 80 -j ACCEPT   写入修改

   ​         /etc/init.d/iptables save   保存修改

   ​        service iptables restart    重启防火墙，修改生效

   ​       方法二：

   ​       vi /etc/sysconfig/iptables  打开配置文件加入如下语句:

   ​       -A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT   重启防火墙，修改完成

   2、关闭端口

   ​     方法一：

   ​         /sbin/iptables -I INPUT -p tcp --dport 80 -j DROP   写入修改

   ​         /etc/init.d/iptables save   保存修改

    	        service iptables restart    重启防火墙，修改生效 

   ​       方法二：

   ​       vi /etc/sysconfig/iptables  打开配置文件加入如下语句:

   ​       -A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j DROP   重启防火墙，修改完成

   3、查看端口状态

   ​      /etc/init.d/iptables status

   有时启动应用时会发现端口已经被占用，或者是感觉有些端口自己没有使用却发现是打开的。这时我们希望知道是哪个应用/进程在使用该端口。

    	CentOS下可以用netstat或者lsof查看，Windows下也可以用netstat查看，不过参数会不同 

   Linux:

   netstat -nap #会列出所有正在使用的端口及关联的进程/应用

   lsof -i :portnumber #portnumber要用具体的端口号代替，可以直接列出该端口听使用进程/应用

    	一、检查端口被哪个进程占用 

    	 netstat -lnp|grep 88   #88请换为你的apache需要的端口，如：80 

    	SSH执行以上命令，可以查看到88端口正在被哪个进程使用。如进程号为 1777 。 

    	二、查看进程的详细信息   ps 1777   SSH执行以上命令。查看相应进程号的程序详细路径。 

    	三、杀掉进程，重新启动apache   kill -9 1777        #杀掉编号为1777的进程（请根据实际情况输入）   service httpd start #启动apache 

    	SSH执行以上命令，如果没有问题，apache将可以正常启动。 

      Windows系统:  netstat -nao #会列出端口关联的的进程号，可以通过任务管理器查看是哪个任务  最后一列为程序PID，再通过tasklist命令：tasklist | findstr 2724  再通过任务管理结束掉这个程序就可以了 

   

2. 查看文件编码

   - vim中 用 

     ```bash
     :set fileencoding
     ```

   - 安装enca命令

     ```bash
     sudu yum install -y enca
     enca file
     ```

3. 

