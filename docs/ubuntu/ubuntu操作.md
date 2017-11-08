####在`Ubuntu`下`ssh`通过`root`身份登录

1. 给`Root`设置登录密码

   ```shell
   sudo passwd
   ```

2. 修改`ssh`配置文件

   ```shell
   PermitRootLogin yes   ##允许Root登录
   ```

3. 重启`SSH`

   ```shell
   service ssh restart
   ```

   ​