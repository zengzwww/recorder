# vscode打开服务器上的项目
* 在本地安装Remote Development插件  
* 打开左侧的“远程资源管理器”，在REMOTE->SSH下面，点击“+”新建一个远程，此时右侧弹出框框，往里面输入ssh登录命令，比如ssh blueberry@192.168.1.116，回车确定，在弹出的项目中选择“C:\Users\xxx\.ssh\config”，xxx是计算机用户名，一个新的远程建立好了  
* 单击vscode坐下角的两个背靠背的“L”构成的那个图标，在vscode顶上部弹出的东东里选择“Connect to Host ...”，在弹出的Host列表中选择刚才建立的远程，此时弹出新的vscode
* 弹出框框问“Are you sure you want to continue?”，选择“Continue”继续，然后输入密码，建立连接  
* 在左侧的资源管理器中“打开文件夹”，然后再弹出的框框中选择远程服务器上项目文件夹，点击“确定”，输入密码，完成打开项目

# vscode cmake编译
* 在服务器上安装C++，CMake和CMake Tools插件  
* vscode底部会出现CMake编译模式(Debug/Release/...)、编译工具、构建目标、运行目标等选择工具，选择对应的工具使用即可  

# vscode gdb调式
* 按下ctrl+shift+D打开“运行和调试”面板，点击“创建launch.json文件”创建launch.json文件，此时“configurations”为空.  
* 在打开的launch.json页面，点击“添加配置”，此时“configurations”后面弹出菜单，选择“C/C++： (gdb)启动”，自动填充“configurations”.  
* 更改“program”和“args”. ${workspaceFolder}是工程目录(.vscode所在目录).  

# vscode gdb无代码调式
* 将Debug版本的应用程序部署到服务器上.
* 更改“program”和“args”. ${workspaceFolder}是工程目录(.vscode所在目录).  
* 如果程序里有用到相对路径，相对路径对应的运行路径为.vscode目录. 比如对于   
```
deploy/bin/some_program
deploy/lib/some_library
deploy/.vscode/launch.json
```
运行路径是deploy/.vscode/，万分注意.   
* 如果需要设置环境变量，可在environment里设置，比如   
```
"environment": [{"name": "LD_LIBRARY_PATH", "value": "$LD_LIBRARY_PATH:${workspaceFolder}/lib"}],
```

# vscode设置python解释器

按下ctrl+shift+p，在下拉菜单中选择解释器. 前提是装了python插件.

# vscode调试过程中图像可视化神器
[simply-view-image-for-python-debugging](https://marketplace.visualstudio.com/items?itemName=elazarcoh.simply-view-image-for-python-debugging)
