## nvm常用命令
```bash
nvm version
nvm npm_mirror https://npm.taobao.org/mirrors/npm/
nvm list available
nvm ls
nvm install latest 
nvm install 12.4.0
nvm uninstall 12.4.0
```
## nvm安装注意事项
1.如果之前安装过nodejs需要删除已存在的node,如何从Windows中删除Node.js：
~~~~
删除步骤
1.从卸载程序卸载程序和功能。

2.重新启动（或者您可能会从任务管理器中杀死所有与节点相关的进程）。

3.寻找这些文件夹并删除它们（及其内容）（如果还有）。根据您安装的版本，UAC设置和CPU架构，这些可能或可能不存在：

C:\Program Files (x86)\Nodejs
C:\Program Files\Nodejs
C:\Users\{User}\AppData\Roaming\npm（或%appdata%\npm）
C:\Users\{User}\AppData\Roaming\npm-cache（或%appdata%\npm-cache）

4.检查您的%PATH%环境变量以确保没有引用Nodejs或npm存在。

5.如果仍然没有卸载，请where node在命令提示符下键入，您将看到它所在的位置 - 删除（也可能是父目录）。

6.重新启动，很好的措施。
~~~~

2.windows下安装目录不能是中文，如果是英文不能出现空格

3.编辑setting文件,设置淘宝下载源
```bash
node_mirror: https://npm.taobao.org/mirrors/node/
npm_mirror: https://npm.taobao.org/mirrors/npm/
```