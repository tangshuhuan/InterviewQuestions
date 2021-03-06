# 什么是守护进程？Node 如何实现守护进程？

守护进程是不依赖终端（tty）的进程，不会因为用户退出终端而停止运行的进程。

Node 实现守护进程的思路：
  1. 创建一个进程 A；
  2. 在进程 A 中创建进程 B，可以使用 `child_process.fork` 或者其他方法；
  3. 启动子进程时，设置 `detached` 属性为 true，保证子进程在父进程退出后继续运行；
  4. 进程 A 退出，进程 B 由 init 进程接管。此时进程 B 为守护进程。