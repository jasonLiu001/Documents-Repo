##启用POWERSHELL远程连接

服务器端配置

1. 管理员身份运行PowerShell ISE后，运行以下命令

   ```powershell
   Enable-PSRemoting -Force
   ```

   >This command starts the WinRM service, sets it to start automatically with your system, and creates a firewall rule that allows incoming connections. The `-Force` part of the cmdlet tells PowerShell to perform these actions without prompting you for each step

2. 添加客户端到信任列表

   ```powershell
   Set-Item wsman:\localhost\client\trustedhosts *
   ```

   >The asterisk is a wildcard symbol for all PCs. If instead you want to restrict computers that can connect, you can replace the asterisk with a comma-separated list of IP addresses or computer names for approved PCs.
   >
   >查看信任列表命令：
   >
   >```powershell
   >Get-Item WSMan:\localhost\Client\TrustedHosts
   >```

3. 禁用`Powershell`远程连接

   ```powershell
   Disable-PSRemoting -force
   ```

4. 重启`WinRM`服务

   ```powershell
   Restart-Service WinRM
   ```

客户端测试连接

1. 测试连接

   ```powershell
   Test-WsMan COMPUTER
   ```

   > This simple command tests whether the WinRM service is running on the remote PC. If it completes successfully, you’ll see information about the remote computer’s WinRM service in the window—signifying that WinRM is enabled and your PC can communicate. If the command fails, you’ll see an error message instead.

2. 执行远程命令

   ```powershell
   Invoke-Command -ComputerName COMPUTER -ScriptBlock { COMMAND } -credential USERNAME
   ```

3. 会话的方式执行远程命令

   ```powershell
   Enter-PSSession -ComputerName COMPUTER -Credential USER
   ```



## 网络文章

>https://www.thomasmaurer.ch/2011/01/quick-powershell-remoting-guide/