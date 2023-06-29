<div align="left">

<h1 align="left">cgminer项目解读</h1>

## 项目模块
cgminer程序的主要由以下几个模块组成：
- 驱动程序模块：该模块负责与硬件设备进行通信，包括与ASIC和GPU进行通信。该模块提供了一个抽象层，可以针对不同的硬件进行定制和优化。
- 挖掘模块：该模块负责执行实际的挖掘操作，包括计算哈希值、验证区块等。该模块可以根据挖掘算法类型进行优化，以提高挖掘效率。
- 网络模块：该模块负责与比特币网络进行通信，包括从网络中获取最新的区块、广播已发现的区块等。该模块还可以与其他挖掘者进行协作，以提高挖掘效率。
- 用户界面模块：该模块负责与用户进行交互，包括设置挖掘参数、显示挖掘状态等。该模块可以提供命令行界面和图形界面两种选择。
- 数据库模块：该模块负责存储挖掘相关的数据，包括已挖掘的区块、未支付的比特币等。该模块可以与比特币网络中的其他节点进行同步，以保证数据的一致性。

在cgminer程序的整个架构中，挖掘模块是最核心的部分，它负责执行实际的挖掘操作，从而获得比特币奖励。其他模块则负责提供支持和协助，以确保挖掘操作的顺利进行。

## 代码解读
- 主函数 main 在cgminer.c
  * 初始化全局变量和模块：首先，main函数会调用init_globals函数初始化全局变量，然后依次初始化各个模块，如设备模块、矿池模块、API模块等。
  * 解析命令行参数：main函数接着会调用parse_args函数解析命令行参数，包括矿池服务器地址、矿池用户名和密码、设备类型、线程数、采矿算法等。这些参数都是程序运行所必须的配置信息。
  * 连接矿池服务器：一旦解析出矿池服务器地址、用户名和密码等信息，main函数就会调用connect_to_pool函数连接矿池服务器。这个过程中，程序会向矿池服务器发送认证信息，以便获取工作任务。
  * 开启工作线程：连接成功后，main函数会调用start_threads函数启动工作线程。每个线程都会循环执行work_loop函数，不断尝试获取工作任务并进行采矿计算。如果有新的工作任务，线程会调用submit_work函数将计算     结果提交给矿池服务器。
  * 退出程序：当用户按下Ctrl-C等退出程序时，main函数会调用shutdown_threads函数关闭所有工作线程，并释放各个模块的资源。最后，程序退出并返回0。
  总之，cgminer.c文件中的main函数是整个程序的核心逻辑，它负责初始化和管理各个模块，启动工作线程，连接矿池服务器，处理命令行参数等重要任务。
- 几个用到的signal
  * SIGINT 程序终止(interrupt)信号, 在用户键入INTR字符(通常是Ctrl+C)时发出
  * SIGABRT 程序自己发现错误并调用abort时产生
  * SIGTERM 程序结束(terminate)信号, 与SIGKILL不同的是该信号可以被阻塞和处理. 通常用来要求程序自己正常退出. shell命令kill缺省产生这个信号.
- 工作队列
  * 创建获取工作队列tq_new()
- 初始化USB设备
- 当有benchmark 或者 benchfile 选项是
-

## 探测probe_pools
- 启动total_pools个线程，每个线程运行test_pool_thread函数
- pool_active
  * 若有has_stratum, initiate_stratum, init_stratum_threads
  * 若没有has_stratum, curl_easy_init,
    * Probe for GBT support on first pass, GBT?
    *  

## 有bitmain的?
- 宏USE_BITMAIN_SOC ? 10414

## 项目编译环境
- forked 源代码到我的github仓库
- git clone 代码到已有的开发环境是CentOS Linux release 8.4.2105
- 安装 yum install autoconf automake libtool libcurl-devel 由于运行./autogen.sh遇到错误 missing libcurl dev
- 运行./autogen.sh
- ./configure
- ./make
</div>
