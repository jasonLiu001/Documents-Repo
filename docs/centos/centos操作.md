`iptables`防火墙

搭建web服务器

1. 安装`nginx`

   ```shell
   yum install nginx -y
   ```

   ​

2. 启动`nginx`

   ```shell
   service nginx start
   ```

3. 自动启用`ngnix`

   ```shell
   systemctl enable nginx
   ```

4. 查看`nginx`状态

   ```shell
   service nginx status
   ```

   ​

epel包安装

   ```shell
   yum -y install epel-release
   ```
