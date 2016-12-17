#Custom Settings to restart nginx command
=============
##常用的 bat 命令

    1.Echo 命令
　　打开回显或关闭请求回显功能，或显示消息。如果没有任何参数，echo 命令将显示当前回显设置。

    语法
    ```
　　echo [{on　off}] [message]
　　Sample：@echo off / echo hello world
    ```
    2.@ 命令
　　表示不显示@后面的命令，在入侵过程中（例如使用批处理来格式化敌人的硬盘）自然不能让对方看到你使用的命令啦。
    ```
    Sample：@echo off
　　@echo Now initializing the program,please wait a minite...
    ```    
    3.Rem 命令
　　注释命令，在C语言中相当与/*--------*/,它并不会被执行，只是起一个注释的作用，便于别人阅读和你自己日后修改。
    ```
　　Rem Message
　　Sample：@Rem Here is the description.
    ```
　　4.Pause 命令
　　运行 Pause 命令时，将显示下面的消息：
    Press any key to continue . . .
    ```
　　Sample：
　　@echo off
　　:begin
　　copy a:*.* d：\back
　　echo Please put a new disk into driver A
　　pause
　　goto begin
    ```
　　在这个例子中，驱动器 A 中磁盘上的所有文件均复制到d:\back中。
    显示的注释提示您将另一张磁盘放入驱动器 A 时，pause 命令会使程序挂起，以便您更换磁盘，然后按任意键继续处理。
    
    5.start 命令
　　调用外部程序，所有的DOS命令和命令行程序都可以由start命令来调用。
　　入侵常用参数：
    
    6.Goto 命令
　　指定跳转到标签，找到标签后，程序将处理从下一行开始的命令。
　　语法：
    ```
    goto label （label是参数，指定所要转向的批处理程序中的行。）
　　Sample：
　　if {%1}=={} goto noparms
    ```
    如果对此命令有兴趣可以从网上搜索相关的其他命令。

##代码
    
    复制下面的代码，并注意注释，换好 cd 后的应用路径，保存为 .bat 文件。双击即可运行。

    @echo off
    rem 通过任务列表查找该应用是否运行;
    tasklist|find "nginx.exe"
    rem 如果正在运行跳转到 A 其他跳转 B ;
    if %errorlevel% EQU 0 (goto A) else (goto B)

    :A
    echo "nginx.exe"存在！
    echo 正在关闭...
    rem 终止该应用;
    TASKKILL /F /IM nginx.exe /T
    echo 正在运行重启命令...
    rem 在此需要换你文件的路径。
    cd "C:\nginx-1.11.6"
    start nginx.exe

    echo nginx重启成功
    pause
    exit

    :B
    echo 正在打开...nginx.exe
    rem 在此需要换你文件的路径。
    cd "C:\nginx-1.11.6"
    start nginx.exe
    echo nginx运行成功！
    pause
    exit
