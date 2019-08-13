

















<font size = 10>KungFu    V2.0</font>

<font size = 10>产品使用手册</font>

























[TOC]

























# 1.功夫交易系统简介

------

##1.1 功夫介绍

功夫是 [Taurus.ai](http://taurus.ai) 团队专为量化交易者设计的开源交易执行系统。功夫想要解决以下问题：

- 低延迟交易 - 量化交易者对系统内响应速度有极高要求，功夫提供微秒级别的系统响应，支持带纳秒级时间戳的交易数据实时存储和盘后分析。
- 开放的策略编写方式 - 功夫支持 Python 3 及 C++ 形式的策略编写，策略师可以不受限的自由使用第三方计算库，放飞创意。
- 友好的使用方式 - 告别 Linux shell 小黑屋，功夫提供图形化操作界面，简化策略运维流程。而进阶用户仍然具备通过底层 API 以无界面形式使用系统的能力。
- 跨平台运行 - 三大主流平台（Windows、MacOSX、Linux）皆可编译运行。
- 灵活的扩展接口 - 功夫提供几种不同的数据交互接口（易筋经、SQLite、nanomsg），支持用户自行开发各种功能模块。

功夫系统架构如下：

- 后台核心（C++）

  - 易筋经（yijinjing） - 专为金融交易设计的超低延迟时间序列内存数据库，提供纳秒级时间精度，可落地交易相关的全部数据。
  - 咏春（wingchun） - 策略执行引擎，提供策略开发接口，利用易筋经特性，咏春还提供一系列交易数据分析工具。

- 中台交互（C++/Python/nodejs）

  - [SQLite](https://www.sqlite.org/index.html) - 功夫使用内嵌式数据库 SQLite 存储配置信息及中间数据
  - [nanomsg](https://nanomsg.org) - 功夫使用 nanomsg 作为前后台通信机制，系统内对延迟不敏感的指令（例如手动下单等）可通过 nanomsg 信道传达。

  前端UI（Node.js）

  - [Electron](https://electronjs.org) - 跨平台的桌面应用开发框架
  - [Vue.js](https://vuejs.org) - UI开发框架

  打包机制

  - [pyinstaller](https://pyinstaller.readthedocs.io/en/stable/) - 封装完整的 Python 环境及所有二进制依赖，使得功夫的安装部署绿色化，无需依赖其他软件。
  - [pipenv](https://pipenv.readthedocs.io) - Python 依赖管理工具，开发过程无需额外安装 Python 包。
  - [pm2](https://pm2.io) - 基于 nodejs 的进程管理工具
  - [electron-builder](https://www.electron.build) - 借助 Electron 技术，功夫可以提供本地化应用程序的安装使用体验。

  功夫在系统设计上支持任意柜台的对接（涵盖中国所有股票、期货市场），目前功夫开源版仅提供 CTP 和 XTP 柜台对接的实现；如果需要接入更多柜台请通过 [Taurus.ai](http://taurus.ai) 官网联系我们；开发者也可根据长拳标准自行开发新的柜台接口。

  初次使用请参考 [功夫交易系统用户手册](https://app.gitbook.com/@taurusai/s/kungfu-userdoc/)；更多介绍请关注知乎专栏 [硅商冲击](https://zhuanlan.zhihu.com/silicontrader)。

##1.2 License

功夫采用 Apache License 2.0 发布。

##1.3 Setup 编译及运行环境

功夫的编译依赖以下工具：

- 支持 C++17 的编译器
- Node.js (>=8 <11)
- yarn
- Python 3
- pipenv
- cmake (>3.12)

功夫编译依赖 [Node.js](https://nodejs.org)，建议预先进行如下设置加速依赖包的下载：

```$ npm config set registry https://registry.npm.taobao.org
$ npm config set registry https://registry.npm.taobao.org
$ npm config set puppeteer_download_host https://npm.taobao.org/mirrors
$ npm config set electron_mirror https://npm.taobao.org/mirrors/electron/
$ npm config set sass-binary-site https://npm.taobao.org/mirrors/node-sass
```

###1.3.1MacOSX

```$ brew install git cmake node@10
$ brew install git cmake node@10
$ npm install -g yarn electron-builder
$ pip install pipenv
```

###1.3.2 Windows

开发组在 Visual Studio 2017 15.9.14 环境下进行工作，安装时需要勾选 VC140（Visual Studio 2015) toolset。

下载并安装 [git](https://git-scm.com/download/win)，[Python 3](https://www.python.org/downloads/windows/)，[CMake](https://cmake.org/install/)，[Node.js LTS 10.15.3](https://nodejs.org/en/download/) 并添加相应路径至 %PATH% 环境变量。

```C:\> npm install -g yarn electron-builder
C:\> npm install -g yarn electron-builder
C:\> pip install pipenv
```

###1.3.3 Linux

确保编译器支持 C++ 17，例如对于 CentOS，升级 gcc 到 5.0 以上：

```yum -y install centos-release-scl
yum -y install centos-release-scl
yum -y install devtoolset-8-gcc devtoolset-8-gcc-c++ devtoolset-8-binutils
echo "source /opt/rh/devtoolset-8/enable" >> /etc/profile
source /etc/profile
```

```$ # install cmake3 node.js
$ # install cmake3 node.js
$ node-v10.15.3-linux-x64/bin/npm install -g yarn electron-builder
$ pip install pipenv
```

##1.4 Compile 编译

###1.4.1 常规操作

获取代码并编译：

```$ git clone https://github.com/taurusai/kungfu
$ cd kungfu
$ yarn
$ yarn build
```

编译结果输出在 app/build 目录下，例如在 MacOSX 系统上，最终的可执行文件输出在 app/build/mac/Kungfu.Trader.app。

遇到编译问题需要完整的重新编译时，执行以下命令清理临时文件：

``` $ yarn clean 
$ yarn clean
```

###1.4.2 选择编译模式

功夫默认编译为 Release 模式（-D[CMAKE_BUILD_TYPE](https://cmake.org/cmake/help/v3.12/variable/CMAKE_BUILD_TYPE.html)="Release")，如果希望以 Debug 模式编译，需要执行以下命令：

```$ npm config set kungfu-core:buildtype "Debug"
$ npm config set kungfu-core:buildtype "Debug"
```

执行以下命令恢复 Release 模式：

```
$ npm config set kungfu-core:buildtype "Release"
```

切换编译模式后，需要执行以下命令重新生成配置文件：

```
$ yarn workspace kungfu-core run configure
```

###1.4.3 编译过程产生的临时文件

编译过程会在代码所在目录下生成如下临时文件：

```node_modules
node_modules
build
dist
```

通常情况下可通过执行如下命令对 build 和 dist 进行清理：

```
$ yarn clean
```

需要注意 node_modules 目录为 npm 产生的包目录，一般情况下无需清除，如有特殊需要可手动删除。

另外，编译过程中会在系统的以下路径产生输出:

```
$HOME/.cmake-js                     # cmake.js 存储的 C++ 依赖包
$HOME/.virtualenvs                  # pipenv(windows) 存储的 Python 依赖
$HOME/.local/share/virtualenvs      # pipenv(unix) 存储的 Python 依赖
```

如果需要清理这些文件，都需要手动删除。

##1.5 Version 版本

- 2.0.0:
  - 跨平台支持
  - 支持 Python 3
  - 提供基于 Electron 的图形化操作界面
- 1.0.0:
  - 以 Docker/rpm 方式运行的最后稳定版本
- 0.0.5:
  - 增加对股票交易柜台 xtp 的支持
  - 在系统 docker 中增加了 numa（xtp 的依赖），不希望更新 docker 的用户可以通过 yum install numactl 来手动安装
- 0.0.4:
  - 增加 FeeHandler 模块，增加策略中的 Pnl 实时计算支持
- 0.0.3:
  - 增强 wingchun report 中的延迟统计工具，新增调用API前的系统内耗时 (TTT before API)
- 0.0.2:
  - 修正了 PosHandler 的一个 update 情况的潜在风险
  - 修正没有 close 的 file 句柄
  - 修正了 memcpy 的潜在越界问题
  - 编译选项优化为 O3
- 0.0.1: 初始化版本

##1.6 Contribute 开发

开发文档即将上线，请关注 [Taurus.ai](http://taurus.ai) 官网。 QQ 交流群 312745666，入群问题答案：taurus.ai





#2.运行第一个策略

##2.1 账户设置

​		KungFu是一款支持跨柜台多账户交易的量化交易系统，系统目前支持的柜台有：`XTP`（股票），`CTP`（期货），后续会不断添加对其他柜台的支持。

​		为了方便用户对账户进行管理，我们在系统内提供了账户模块，在账户模块中，用户可以对账户进行添加、编辑以及删除，也可以查看每一个账户的实时运行状态、运行日志、持仓情况、委托情况、成交情况以及盈亏情况。



<div align=center><img src="/Users/yztao/Desktop/images/acc_setting.png" width="640" height="376">

​		添加一个 `账户` 在kungfu交易系统中，一个账户由一个`行情进程（md）`以及一个`交易进程（td）`组成，`行情进程`用来接受行情，`交易进程`用来下撤单。当我们添加了一个账户，实际上是根据新增账户的信息建立了一个`交易进程`，于此同时，也建立了一个`行情进程`。

```
备注：
1. 行情进程在添加交易进程后会自动添加，一个柜台下只有一行情进程
2. 可以通过切换行情源绑定的账号来实现更换行情进程所绑定的信息
3. ctp柜台只支持windows系统与linux系统，xtp柜台对于mac，windows，linux三个系统都支持
```

###2.1.1 添加账户步骤

- 点击账户模块交易账户列表左上角的`添加`按钮
- 选择账户对应的柜台
- 填写账户信息表单，点击确定
- 操作成功后，交易账户列表中会新增刚添加账户的交易进程，**如果该账户所属柜台从未被其他账户使用**，在行情源列表中会新增一条行情进程

<div align=center><img src="/Users/yztao/Desktop/images/add_acc.png" width="640" height="376">

[柜台下账户对应字段](/account/acc_setting_key.md/#柜台下账户对应字段)

###2.1.2 启动<font color="red">````交易进程````</font>

------

​		添加完账户后，交易账户列表会出现一条新的`交易进程`，需要保证其正常运行，才能正常进行交易，点击交易账户列表内的`连接`按钮。

<div align=center><img src="/Users/yztao/Desktop/images/TD_start.png"  width="640" height="376">

​		启动交易进程后，交易进程会与交易柜台进行连接，从交易柜台中获取该账户最新的资金与持仓信息，并同步到KungFu系统的数据库中。

[交易进程连接状态对应表]()





###2.1.3 启动`行情进程`

---

​		交易进程被添加后，如果该交易进程的柜台**没有被系统内其他账户使用**，行情源列表中会自动出现一条`行情进程`。行情进程的运行用来保证策略能够接收到行情，也需要先启动后才能运行交易，点击行情源列表内的`连接`按钮，如果行情进程出现异常，可以点击`行情日志`按钮，查看对应的运行日志。

<div align=center><img src="/Users/yztao/Desktop/images/MD_start.png" width="640" height="376">

​		行情进程的原理是**绑定柜台下账户，从账户信息的的行情地址中获取行情**，每个柜台只需绑定一个账户，可以通过切换不同的账户来作为行情源，从而接收期望的行情信息。

<div align=center><img src="/Users/yztao/Desktop/images/md_change.png" width="640" height="376">

[行情进程连接状态对应表](/account/acc_setting_key.md/#行情进程连接状态对应表)

```
备注：
1. 交易/行情进程需处于就绪状态，才能算是连接成功，才能够进行交易
2. 交易/行情进程若出现登录失败，请不要担心，系统会每隔一时间自动去重新连接
3. 在当前版本中，因为要首先保正交易系统执行性能，暂不对交易系统进程消耗资源做限制
```



##2.2 设置策略

​		Kungfu本质上是为策略程序提供了一个运行环境。在Kungfu中，每一个策略都是运行在一个单独的进程里，通过策略列表的开关进行管理，策略运行时打印的log，交易的实时数据都会呈现在系统中。

<div align=center><img src = "/Users/yztao/Desktop/images/add_str.png" width="640" height="376" alt="策略模块">

###2.2.1 添加策略步骤

- 进入策略模块，点击策略列表的添加按钮
- 输入策略的名称 **添加成功后，策略名称不能修改**，选择策略绑定的本地文件
- 添加成功后，点击运行按钮

<div align=center><img src = "/Users/yztao/Desktop/images/add_str.png" width="640" height="376" alt="添加策略">

```备注：
备注：
1. 在启动策略之前，需要保证策略使用的行情/交易进程连接处于就绪状态
2. 在运行策略时，需要关注右下角的账户状态
3. 如果账户状态不为绿色，需要确认策略运行所需的交易/行情进程是否开启
```





# 3.功能介绍

## 3.1 账户维护

​		在日常使用过程中，用户可以根据实际需要，在账户模块对系统内的账户进行维护，用户可以修改已有的账户信息，或者删除不需要的账户。

<div align=center><img src="/Users/yztao/Desktop/images/acc_setting.png" width="640" height="376">

### 3.1.1 账户修改

​		用户可以对已有账户的信息（除账户名外）进行修改，具体的点击账户的设置按钮后会有该账户的信息表单，修改完成后保存；如果账户的交易柜台连接处于开启状态，修改成功后，需要手动重启该账户的交易连接后，修改才能生效。

<div align=center><img src="/Users/yztao/Desktop/images/acc_setting_1.png" width="640" height="376">

​		为了提高账户盈亏的计算精度，用户可以对账户的交易手续费率进行设置，点击账户右侧的手续费设置按钮，在手续费设置弹窗内修改手续费参数

<div align=center><img src="/Users/yztao/Desktop/images/acc_setting_1.png" width="640" height="376">

### 3.1.2账户删除

​		在交易账户列表，点击删除按钮可以删除不需要的交易账户，但是，在删除交易账户之前，需要保证：

​	a）：需要删除的交易账户的交易连接已经关闭

​	b）：如果被删除的交易账户是该柜台的行情接收账户，需要关闭该柜台的行情连接

​		如果被删除的账户时该柜台的行情账户，系统会自动选择该柜台的其他账户作为行情源账户。需要注意的是，删除账户会把与该账户有关的所有信息都删除，其中包括账户资金、账户持仓、账户委托记录、账户成交记录，账户交易日志。



##3.2 账户信息

###3.2.1 账户日志

​		用户可以点击账户后面的运行日志按钮，在新的窗口打开账户的实时运行日志，方便用户实时地监控账户的运行情况

<div align=center><img src="/Users/yztao/Desktop/images/acc_log.png" width="640" height="376">

### 3.2.2 账户持仓

​		在交易账户列表中，选中需要查看持仓的账户后，在持仓模块就会显示该账户的持仓信息，其中包括：

- 代码：持仓标的的代码

- 多空：持仓的方向

- 昨：该标的的昨仓

- 今：该标的的今仓

- 总：该标的的总持仓

  用户可以通过搜索标的代码来定位自己需要查看的标的持仓，可以通过点击`导出按钮`，导出账户的持仓明细；

<div align=center><img src="/Users/yztao/Desktop/images/acc_holding.png" width="640" height="376">

​		功夫交易系统支持用户进行手动下单，点击持仓模块的`下单`按钮，可以用在交易账户列表中选中的账户对自选的标的进行手动下单，下单类型支持市价单和限价单；

<div align=center><img src="/Users/yztao/Desktop/images/acc_holding_order.png" width="640" height="376">

```
说明：账户的持仓信息会在启动账户的交易进程的时候，与该账户在交易柜台的持仓信息进行同步，同步完成以后，系统内会维护该账户的持仓信息，如果该账户在系统外进行了交易，则账户在系统内的持仓与账户在交易柜台的真实持仓会不一样。
```





### 3.2.3 账户委托

​		在交易账户列表中，选中需要查看委托记录的账户后，在委托模块就可以看到该账户的委托记录。

​		在委托模块中，默认显示的是该账户的未完成委托；点击`当日委托` 按钮后，会显示该账户当日所有的委托记录; 用户可以通过点击`导出`按钮，导出该账户某一时间段内的历史委托记录;



<div align=center><img src="/Users/yztao/Desktop/images/acc_entrust.png" width="640" height="376">

<div align=center><img src="/Users/yztao/Desktop/images/acc_entrust_1.png" width="640" height="376">

- 下单时间：触发该笔委托的时间
- 代码：该笔委托的标的代码
- 买卖：该笔委托的买卖方向
- 开平：该笔委托对应的仓位开平方向
- 委托价：该笔委托对应的委托价格
- 已成交/全部：该笔委托已成交的数量与该笔委托的委托总量的比
- 订单状态：该笔委托当前的状态
- 策略：触发该笔委托的策略名称

用户也可以通过搜索关键字的方式定位自己需要的委托记录，搜索的对象为委托记录里面的：

- 代码名称
- 策略名称
- OrderID(系统维护的订单编号，在列表中没显示)

功夫量化交易系统支持用户对未完成委托进行撤单操作，点击`全部撤单`按钮后，系统会对当前该账户的所有未完成订单进行撤单操作；



<font color = red>委托订单状态对应表</font>

| 字段             | 字段颜色                                         |
| :--------------- | :----------------------------------------------- |
| 等待             | 委托订单请求已发送，等待柜台返回信息，非最终状态 |
| 错误             | 委托订单请求失败，最终状态                       |
| 全部成交         | 委托订单请求已全部成交，最终状态                 |
| 全部撤销         | 委托订单请求已全部撤销，最终状态                 |
| 部分撤销部分成交 | 委托订单部分撤销部分成交，最终状态               |



### 3.2.4 账户成交

在交易账户列表中，选中需要查看当日成交记录的账户后，页面右下方就会显示该账户的当日成交记录。

在当日成交记录中，我们展示了每一笔成交记录的：

- 成交时间：该笔交易完成的时间
- 代码：该笔交易的标的代码
- 买卖：该笔交易的买卖方向
- 开平：该笔交易对应的仓位开平方向
- 成交价：该笔交易标的的成交价格
- 成交量：该笔交易标的的成交数量
- 策略：触发该笔交易的策略名称

用户可以通过点击`导出`按钮，导出某一时间段内的该账户的成交记录；

用户也可以通过搜索关键字的方式定位自己需要的成交记录，搜索的对象为成交记录里面的：

- 标的代码
- 策略

<div align=center><img src="/Users/yztao/Desktop/images/acc_deal.png" width="640" height="376">

### 3.2.5 账户盈亏

​		在交易账户列表中，选中需要查看盈亏的账户后，收益曲线就显示该账户的实时盈亏情况

​		收益曲线有两种表现形式：日线、分钟线

- 日线会显示该账户添加到系统后的整体盈亏走势、累计收益率以及累计收益
- 分钟线显示该账户当天的整体盈亏走势、当日收益率以及当日收益

<div align=center><img src="/Users/yztao/Desktop/images/acc_PNL.png" width="640" height="376">

### 3.2.6 柜台下账户对应字段

添加/设置<font color = gray  size = 5>`CTP`</font>柜台账户字段

| 字段       | 字段含义     |
| :--------- | :----------- |
| account_id | 账户名称     |
| password   | 账户密码     |
| broker_id  | 券商代码     |
| md_uri     | 行情柜台地址 |
| td_uri     | 交易柜台地址 |

添加/设置<font color = gray size = 5>`XTP`</font>柜台账户字段

| 字段         | 字段含义        |
| :----------- | :-------------- |
| user_id      | 账户名称        |
| password     | 账户密码        |
| td_ip        | 交易柜台IP地址  |
| td_port      | 交易柜台端口    |
| software_key | 用户开发软件KEY |
| md_ip        | 行情柜台IP地址  |
| md_port      | 行情柜台端口    |

## 3.3 策略维护

​		在KungFu交易系统中，策略模块相当于系统的策略池，用户可以根据实际需要，在策略模块中对已有策略进行编辑修改和删除，同时可以查看到每一个策略实时的持仓情况、委托情况、成交情况、盈亏情况以及交易日志

<div align=center><img src="/Users/yztao/Desktop/images/add_str.png" width="640" height="376" >



### 3.3.1 策略设置

​		在实际使用中，如果用户需要修改策略的本地文件路径，可以点击策略右侧相应的`设置`按钮，重新绑定新的策略文件

<div align=center><img src="/Users/yztao/Desktop/images/str_set.png" width="640" height="376">





如果策略正在运行，需要重启策略后，策略新绑定的文件路径才能生效

### 3.3.2 策略编辑

​		在KungFu交易系统中，内嵌了IDE，用户可以在KungFu系统中编写本地策略，点击策略右侧相应的`编辑`按钮，会有策略编辑IDE弹窗，在弹窗内，用户可以对策略绑定的本地文件进行编辑，在KungFu内嵌的IDE中，支持

- 创建新的文件
- 创建新的文件夹
- 编译已有文件内容
- 重命名已有文件

<div align=center><img src="/Users/yztao/Desktop/images/str_edit.png" width="640" height="376">



### 3.3.3 删除策略

​		在删除不需要的策略之前，需要保证策略处于关闭状态，需要注意的是，策略删除成功后，系统会将该策略的所有相关信息都删除，其中包括策略持仓信息、策略委托信息、策略成交信息、策略盈亏信息、策略交易日志信息。



## 3.4 策略信息

### 3.4.1 策略持仓

​	在策略列表中，选中需要查看持仓的策略后，在持仓模块就会显示该策略的持仓信息，其中包括：

- 代码：持仓标的的代码
- 多空：持仓的方向
- 昨：该标的的昨仓
- 今：该标的的今仓
- 总：该标的的总持仓

​      用户可以通过搜索标的代码来定位自己需要查看的标的持仓，可以通过点击`导出按钮`，导出策略的持仓明细；

​      功夫交易系统支持用户进行手动下单，点击持仓模块的`下单`按钮，可以将自选的标的通过指定的账户进行下单，下单类型支持市价单和限价单；

​      用户可以通过搜索标的代码来定位自己需要查看的的标的持仓：

<div align=center><img src="/Users/yztao/Desktop/images/str_holding.png" width="640" height="376" alt = "策略下单">

<div align=center><img src="/Users/yztao/Desktop/images/str_order.png" width="640" height="376" alt = "策略下单">



### 3.4.2 策略委托

​		在策略列表中，选中需要查看委托记录的策略后，在委托板块会显示该策略的委托记录。

​		在委托模块中，默认显示的是该策略的未完成委托；点击`当日委托` 按钮后，会显示该策略当日所有的委托记录; 用户可以通过点击`导出`按钮，导出该策略某一时间段内的历史委托记录;

<div align=center><img src="/Users/yztao/Desktop/images/str_entrust.png" width="640" height="376" alt = "未完成委托">

<div align=center><img src="/Users/yztao/Desktop/images/str_entrust_1.png" width="640" height="376" alt = "当日委托">

​		在委托记录列表中，我们展示了每一笔委托记录的：

- 下单时间：触发该笔委托的时间
- 代码：该笔委托的标的代码
- 买卖：该笔委托的买卖方向
- 开平：该笔委托对应的仓位开平方向
- 委托价：该笔委托对应的委托价格
- 已成交/全部：该笔委托已成交的数量与该笔委托的委托总量的比
- 订单状态：该笔委托当前的状态
- 账户：显示执行该委托的交易账户名称

​        用户也可以通过搜索关键字的方式定位自己需要的委托记录，搜索的对象为委托记录里面的：

- 代码名称
- 账户名称
- OrderID(系统维护的订单编号，在列表中没显示)

​         功夫量化交易系统支持用户对未完成委托进行撤单操作，点击`全部撤单`按钮后，系统会对当前该策略的所有未完成订单进行撤单操作；



<font color = red >委托订单状态对应表</font>

| 字段             | 字段说明                                         |
| :--------------- | :----------------------------------------------- |
| 等待             | 委托订单请求已发送，等待柜台返回信息，非最终状态 |
| 错误             | 委托订单请求失败，最终状态                       |
| 全部成交         | 委托订单请求已全部成交，最终状态                 |
| 全部撤销         | 委托订单请求已全部撤销，最终状态                 |
| 部分撤销部分成交 | 委托订单部分撤销部分成交，最终状态               |



### 3.4.3 策略成交

​		在策略列表中，选中需要查看当日成交记录的策略后，页面右下方就会显示该策略的当日成交记录。

​		在当日成交记录中，我们展示了每一笔成交记录的：

<div align=center><img src="/Users/yztao/Desktop/images/str_deal.png" width="640" height="376" alt = "当日成交">

​		在成交记录列表中，我们展示了每一笔成交记录的：

- 成交时间：该笔交易完成的时间
- 代码：该笔交易的标的代码
- 买卖：该笔交易的买卖方向
- 开平：该笔交易对应的仓位开平方向
- 成交价：该笔交易的标的成交价格
- 成交量：该笔交易的标的成交量
- 账户：执行该笔成交的交易账户名

​        用户也可以通过搜索关键字的方式定位自己需要的成交记录，搜索的对象为成交记录里面的：

- 标的代码
- 账户



### 3.4.4 策略盈亏

​		在策略列表中，选中需要查看盈亏的策略后，收益曲线就会显示该策略的实时盈亏情况

​		收益曲线有两种表现形式：日线、分钟线

- 日线会显示该策略添加到系统后的整体盈亏走势、累计收益率以及累计收益
- 分钟线显示该策略当天的整体盈亏走势、当日收益率以及当日收益

<div align=center><img src="/Users/yztao/Desktop/images/str_PNL.png"  width="640" height="376">



### 3.4.5 交易日志

​		交易日志模块会显示策略列表中选中的策略的交易日志详情，如果该策略正在运行，交易日志也会实时更新，用户勾选`跟踪至底部`后，交易日志会一直滚动显示最新的日志信息;

​		用户可以根据`搜索关键字`的方式来筛选需要查看的交易日志，如果策略的交易日志过多，用户也可以点击`清空`按钮，清空前端显示的交易日志;

<div align=center><img src="/Users/yztao/Desktop/images/str_log.png" width="640" height="376" alt = "策略日志">

​			点击`打开日志文件`按钮，会在新窗口打开当前策略对应的日志文件；

<div align=center><img src="/Users/yztao/Desktop/images/str_log_1.png" width="640" height="376" alt = "策略日志窗口">

## 3.5 状态监控

### 3.5.1  账户监控

​		为了方便用户实时监控系统内账户的交易连接状态以及柜台的行情连接状态，在系统页面的右下角设置了账户状态监控浮窗，用户可以通过浮窗按钮的字体颜色来判别当前系统的状态，具体规则如下：

- 当所有连接都就绪时，按钮文字为绿色
- 当有连接未打开，其他连接都为就绪时，按钮文字为灰色
-  当有连接状态处于异常时，按钮文字会显示为橙色或者红色

​        用户还可以在状态浮窗中启停账户的交易连接以及柜台的行情连接



<div align=center><img src = "/Users/yztao/Desktop/images/acc_status.png" width="640" height="376" alt="账户状态监控">

### 3.5.2  进程监控

​		为了方便用户可以实时地监控功夫交易系统的<font color="FF9900">```主控进程(master)```</font>以及<font color="FFCC00">```数据进程(watcher)```</font>的状态，在系统页面的右下角有主进程状态监控浮窗，点击展开浮窗后，可以看到主控进程和数据进程的实时状态，让用户更加全面掌握系统的状态；



<div align=center><img src = "/Users/yztao/Desktop/images/master_status.png" width="640" height="376" alt="主进程状态监控">

​		如果发现进程出现报错，用户可以打开进程的运行日志，通过详细的运行日志，定位进程报错的原因；



<div align=center><img src = "/Users/yztao/Desktop/images/master_status_log.png" width="640" height="376" alt="主进程日志">