# 账户设置

&emsp;&emsp;KungFu是一款支持跨柜台多账户交易的量化交易系统，系统目前支持的柜台有：<font color="#FAAD14">```XTP```</font>（股票），<font color="red">```CTP```</font>（期货），后续会不断添加对其他柜台的支持。<br/>
&emsp;&emsp;为了方便用户对账户进行管理，我们在系统内提供了账户模块，在账户模块中，用户可以对账户进行添加、编辑以及删除，也可以查看每一个账户的实时运行状态、持仓情况、委托情况、成交情况以及盈亏情况。

<div align=center><img src="/images/acc_setting.png" width="640" height="376">

#### 添加一个 <font color="#FAAD14">```账户```</font> 
---

&emsp;&emsp;在kungfu交易系统中，账户有两个概念：<font color="#FAAD14">```行情进程（md）```</font>和<font color="red">```交易进程（td）```</font>，<font color="#FAAD14">```行情进程```</font>用来接受行情，<font color="red">```交易进程```</font>用来下撤单。当我们添加了一条账户，实际上是用添加账户的信息建立了一条<font color="red">```交易进程```</font>，于此同时，也建立了一条<font color="#FAAD14">```行情进程```</font>。

    备注：
    1. 行情进程在添加交易进程后会自动添加，在一个柜台下只有一条
    2. 可以通过切换行情源绑定的账号来实现更换行情进程所绑定的信息
    3. ctp柜台只支持windows系统与linux系统，xtp柜台对于mac，windows，linux三个系统都支持

###### 添加账户步骤

- 点击账户模块交易账户列表左上角的<font color=#FAAD14>```添加```</font>按钮
- 选择账户对应的柜台
- 填写账户信息表单，点击确定
- 操作成功后，交易账户列表中会新增刚添加账户的交易进程，**如果该账户所属柜台从未被其他账户使用**，在行情源列表中会新增一条行情进程

<div align=center><img src="/images/add_acc.gif" width="640" height="376">

[柜台下账户对应字段](/account/acc_setting_key.md/#柜台下账户对应字段)

#### 启动<font color="red">```交易进程```</font>
---

&emsp;&emsp;添加完账户后，交易账户列表会出现一条新的<font color="red">```交易进程```</font>，需要使其正常运行，才能正常进行交易，点击交易账户列表内的<font color="#17b07f">```连接```</font>按钮。

<div align=center><img src="/images/TD_start.png"  width="640" height="376">

&emsp;&emsp;启动交易进程后，交易进程会与交易柜台进行连接，从交易柜台中获取该账户最新的资金与持仓信息，并同步到KungFu系统的数据库中。

[交易进程连接状态对应表](/account/acc_setting_key.md/#交易进程连接状态对应表)

### 启动<font color="#FAAD14">```行情进程```</font>
---

&emsp;&emsp;交易进程被添加后，如果该交易进程的柜台**没有被系统内其他账户使用**，行情源列表中会自动出现一条<font color="#FAAD14">```行情进程```</font>。行情进程的运行用来保证策略能够接收到行情，也需要先启动后才能运行交易，点击行情源列表内的<font color="#17b07f">```连接```</font>按钮，如果行情进程出现异常，可以点击<font color = "red">```行情日志```</font>按钮，查看对应的运行日志。

<div align=center><img src="/images/MD_start.png" width="640" height="376">

&emsp;&emsp;行情进程的原理是**绑定柜台下账户，从账户信息的的行情地址中获取行情**，每个柜台只需绑定一个账户，可以通过切换不同的账户来作为行情源，从而接收期望的行情信息。

<div align=center><img src="/images/md_change.gif" width="640" height="376">

[行情进程连接状态对应表](/account/acc_setting_key.md/#行情进程连接状态对应表)


    备注：
    1. 交易/行情进程需处于就绪状态，才能算是连接成功，才能够进行交易
    2. 交易/行情进程若出现登录失败，请不要担心，系统会每隔一时间自动去重新连接
    3. 在当前版本中，因为要首先保正交易系统执行性能，暂不对交易系统进程消耗资源做限制



​	