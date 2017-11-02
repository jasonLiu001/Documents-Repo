## Testcase

1. 多个`nightmare`实例

   > 多个`nightmare`测试成功，可以启动多个`nightmare`实例

2. ~~通过`electron`创建多个`browserwindow`，并指定`parent`和`child`关系~~

   > 这种方案行不通，原因：即使能创建新的`electron`实例，这个实例也无法和`nightmare`进程进行通信，这样就没有实际的意义了，这就意味着，创建的`BrowserWindow`实例完成的任务结果，当前的`nightmare`实例无法获取到

3. `node`模块的拆分，注册`nightmare`的自定义方法一个方法就独立成一个模块

>  解决方案一：通过`grunt`顺序打包