
## CentOS 7 下安装Nginx服务器
步骤如下：

1. 添加epel源

   ```shell
   yum -y install epel-release
   ```

2. 安装`nginx`

   ```shell
   yum install nginx -y
   ```

3. 添加防火墙的例外规则

   ```shell
   sudo firewall-cmd --permanent --zone=public --add-service=http 
   sudo firewall-cmd --permanent --zone=public --add-service=https
   sudo firewall-cmd --reload
   ```
 
4. 启动`nginx`
   
   ```shell
    systemctl start nginx 
    systemctl enable nginx
   ```
   
5. 查看`nginx`状态

   ```shell
   systemctl status nginx
   ```
