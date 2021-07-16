Windows家庭版Docker下载
#一、环境要求

​        Windows 版 Docker 的环境需要启用 Windows 操作系统中的 Hyper-V 和容器特性，而Windows 10家庭版并没有这两个选项。

![image-20210716110519525](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210716110519525.png)

​       所以我们必须自行下载，再确定电脑支持虚拟化技术后，在桌面创建记事本，将下列代码复制到记事本中：

    pushd “%~dp0”
    dir /b %SystemRoot%\servicing\Packages*Hyper-V*.mum >hyper-v.txt
    for /f %%i in (‘findstr /i . hyper-v.txt 2^>nul’) do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages%%i"
    del hyper-v.txt
    Dism /online /enable-feature /featurename:Microsoft-Hyper-V-All /LimitAccess /ALL
​       再将记事本文件名改为 Hyper-V.cmd，以管理员身份打开这个文件，重启完成就能使用Hyper-V。

​       其次还要安装WSL2(针对于x64系统):

​              1.在管理员身份打开 PowerShell 并运行，在命令行输入：

​             dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

​              2.安装 WSL 2 之前，必须启用“虚拟机平台”可选功能。以管理员身份打开 PowerShell 并运行：

​             dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

​             3.下载Linux内核更新包(x64)：

​                    https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi

​                 运行并安装。

​             4.将 WSL 2 设置为默认版本，在PowerShell下输入：

​                   wsl --set-default-version 2

​             5.打开 [Microsoft Store](https://aka.ms/wslstore)，并选择你偏好的 Linux 分发版并直接获取，如我选择 Ubuntu                                          18.04LTS，首次启动Linux分发版需要为新的 Linux 分发版创建用户帐户和密码。

#二、 下载Docker

​         访问 Docker 的下载（https://www.docker.com/products/docker-desktop）页面，并单击其中的 Download for Windows 按钮进行下载。

​         此后按安装向导，并按照提示一步一步完成整个安装过程，即可完成 Windows 版 Docker 的安装。

​                   

 
