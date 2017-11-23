`iptables`防火墙

搭建web服务器

1. 添加epel源

   ```shell
   yum -y install epel-release
   ```

2. 安装`nginx`

   ```shell
   yum install nginx -y
   ```

   ​

3. 启动`nginx`

   ```shell
   service nginx start
   ```

4. 自动启用`ngnix`

   ```shell
   systemctl enable nginx
   ```

5. 查看`nginx`状态

   ```shell
   service nginx status
   ```
