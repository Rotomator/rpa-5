#UiPath Robots概述
UiPath Robots其实是UiPath的执行者，它执行你在Studio中录制好的脚本。
Robots默认是作为windows服务来安装的。因此Robots可以打开windows的进程，它有windows服务的所有权限。当然Roboot
Robots can also be installed in a user mode. For your Robot, this means that it has the exact same rights as the user under which it has been installed.

Regardless of the mode in which you installed the Robot, it can still be connected to Orchestrator, with an Attended or Unattended license.

