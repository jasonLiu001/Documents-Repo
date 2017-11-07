## CentOS下安装`Shadowsocks`

> 可参考文档地址：
>
> 环境搭建：https://www.iwwenbo.com/0-1-shadowsocks-start/
>
> `shadowsocks`原理：http://blog.021xt.cc/archives/98

1. 申请虚拟主机

   `https://cloud.digitalocean.com`

   申请完成后，启用`Floating IP`

2. 配置编译环境

   ```shell
   yum groupinstall 'Development Tools'
   ```

3. 安装`git`(可选项)

   ```shell
   yum install git
   ```

4. 安装`pip`工具

   ```shell
   #首先安装epel扩展源
   sudo yum -y install epel-release
   #安装python-pip
   sudo yum -y install python-pip
   #升级pip
   sudo pip install --upgrade pip   
   ```

5. 安装`Shadowsockets`

   ```shell
   pip install shadowsocks
   ```

6. 在`/etc`目录下新建`shadowsocks`配置文件

   ```shell
   vi /etc/shadowsoks.json
   ```

   在文件中添加如下内容(**单用户**的配置信息示例)

   ```json
   {
       "server":"my_server_ip",  //内网ip地址
       "server_port":8381,
       "local_address":"127.0.0.1",
       "local_port":1080,
       "password":"foobar1",
       "timeout":300,
       "method":"aes-256-cfb",
       "fast_open":false
   }

   //Linux服务器可以设置fast_open为true
   ```

   **多用户**模式配置文件示例如下：

   ```json
   {
       "server":"my_server_ip",  #填入你的内网IP地址
       "local_address": "127.0.0.1",
       "local_port":1080,
       "port_password": {
           "8381": "foobar1",    #端口号，密码
           "8382": "foobar2",
           "8383": "foobar3",
           "8384": "foobar4"
       },
       "timeout":300,
       "method":"aes-256-cfb",
       "fast_open": false
   }
   ```
   附带：配置说明
   | Name          | 说明                                       |
   | ------------- | ---------------------------------------- |
   | server        | 服务器地址，填ip或域名                             |
   | local_address | 本地地址                                     |
   | local_port    | 本地端口，一般1080，可任意                          |
   | server_port   | 服务器对外开的端口                                |
   | password      | 密码，可以每个服务器端口设置不同密码                       |
   | port_password | server_port + password ，服务器端口加密码的组合      |
   | timeout       | 超时重连                                     |
   | method        | 默认: “aes-256-cfb”，见 [Encryption](https://github.com/shadowsocks/shadowsocks/wiki/Encryption) |
   | fast_open     | 开启或关闭 [TCP_FASTOPEN](https://github.com/shadowsocks/shadowsocks/wiki/TCP-Fast-Open), 填true / false，需要服务端支持 |

7. 防火墙配置

   ```shell
   iptables -A INPUT -p tcp –dport 443 -j ACCEPT。//443为示例端口，你可以改为你需要的。
   重启防火墙：service iptables restart
   ```

8. 启动`shadowsocks`

   - 前端启动：`ssserver -c /etc/shadowsocks.json`；
   - 后端启动：`ssserver -c /etc/shadowsocks.json -d start`；
   - 停止：`ssserver -c /etc/shadowsocks.json -d stop`；
   - 重启(修改配置要重启才生效)：`ssserver -c /etc/shadowsocks.json -d restart`

9. 设置开机启动 
     - 在终端输入`vi /etc/rc.local`，
     - 把里面最后的带有ssserver的一大段默认的代码删除掉，
     - 再把`ssserver -c /etc/shadowsocks.json -d start`加进去，
     - 按`wq`保存退出。

10. 优化`shadowsock`

    https://shadowsocks.org/en/config/advanced.html

11. 测试服务器是否正常工作

     在客户端所在的机器上运行以下命令

     ```shell
     telnet ip 端口

     telnet 45.55.108.80 22
     ```

12. 如果出现"拒绝连接"情况解决

      + 查看SSH对应的22端口的绑定IP是什么`netstat -anp | grep 22`

        ```
        [root@centos-512mb-sfo1-01 ~]# netstat -anp | grep 22
        tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      962/sshd            
        tcp        0      0 192.241.218.88:22       119.4.225.87:31798      SYN_RECV    -                   
        tcp        0    104 10.12.0.5:22            183.240.196.63:8514     ESTABLISHED 993/sshd: root@pts/ 
        tcp6       0      0 :::22                   :::*                    LISTEN      962/sshd            
        unix  2      [ ACC ]     STREAM     LISTENING     16322    9
        ```

        这里面出现了两个IP地址：`192.241.218.88`和`10.12.0.5`，这时可用把`shadowsocks.json`中的`server`节点替换成其中任意一个并测试，哪个可用正常使用，就用哪个。

13. 优化

      ## Optimize the shadowsocks server on Linux

      First of all, upgrade your Linux kernel to 3.5 or later.

      ### Step 1, increase the maximum number of open file descriptors

      To handle thousands of concurrent TCP connections, we should increase the limit of file descriptors opened.

      Edit the `limits.conf`

      ```
      vi /etc/security/limits.conf
      ```

      Add these two lines

      ```
      * soft nofile 51200
      * hard nofile 51200
      ```

      Then, before you start the shadowsocks server, set the ulimit first

      ```
      ulimit -n 51200
      ```

      ### Step 2, Tune the kernel parameters

      The priciples of tuning parameters for shadowsocks are

      1. Reuse ports and conections as soon as possible.
      2. Enlarge the queues and buffers as large as possible.
      3. Choose the TCP congestion algorithm for large latency and high throughput.

      Here is an example `/etc/sysctl.conf` of our production servers:

      ```
      fs.file-max = 51200

      net.core.rmem_max = 67108864
      net.core.wmem_max = 67108864
      net.core.netdev_max_backlog = 250000
      net.core.somaxconn = 4096

      net.ipv4.tcp_syncookies = 1
      net.ipv4.tcp_tw_reuse = 1
      net.ipv4.tcp_tw_recycle = 0
      net.ipv4.tcp_fin_timeout = 30
      net.ipv4.tcp_keepalive_time = 1200
      net.ipv4.ip_local_port_range = 10000 65000
      net.ipv4.tcp_max_syn_backlog = 8192
      net.ipv4.tcp_max_tw_buckets = 5000
      net.ipv4.tcp_fastopen = 3
      net.ipv4.tcp_mem = 25600 51200 102400
      net.ipv4.tcp_rmem = 4096 87380 67108864
      net.ipv4.tcp_wmem = 4096 65536 67108864
      net.ipv4.tcp_mtu_probing = 1
      net.ipv4.tcp_congestion_control = hybla
      ```

      Of course, remember to execute `sysctl -p` to reload the config at runtime.

