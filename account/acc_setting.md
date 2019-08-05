# 账户维护

&emsp;&emsp;在日常使用过程中，用户可以根据实际需要，在账户模块对系统内的账户进行维护，用户可以修改已有的账户信息，或者删除不需要的账户。

<div align=center><img src="/images/acc_setting.png" width="640" height="376">

### 账户修改

&emsp;&emsp;用户可以对已有账户的信息（除账户名外）进行修改，具体的点击账户的设置按钮后会有该账户的信息表单，修改完成后保存；<font color = orange>如果账户的交易柜台连接处于开启状态，修改成功后，需要手动重启该账户的交易连接后，修改才能生效</font>。

<div align=center><img src="/images/acc_setting_1.png" width="640" height="376">

&emsp;&emsp;为了提高账户盈亏的计算精度，用户可以对账户的交易手续费率进行设置，点击账户右侧的手续费设置按钮，在手续费设置弹窗内修改手续费参数

<div align=center><img src="/images/fee_setting.png" width="640" height="376">

### 账户日志
&emsp;&emsp;用户可以点击账户后面的运行日志按钮，在新的窗口打开账户的实时运行日志，方便用户实时地监控账户的运行情况

<div align=center><img src="/images/acc_log.png" width="640" height="376">

### 账户删除

&emsp;&emsp;在交易账户列表，点击删除按钮可以删除不需要的交易账户，但是，在删除交易账户之前，需要保证：

​	a）：需要删除的交易账户的交易连接已经关闭

​	b）：如果被删除的交易账户是该柜台的行情接收账户，需要关闭该柜台的行情连接

&emsp;&emsp;如果被删除的账户时该柜台的行情账户，系统会自动选择该柜台的其他账户作为行情源账户。<font color = orange>需要注意的是，删除账户会把与该账户有关的所有信息都删除，其中包括账户资金、账户持仓、账户委托记录、账户成交记录，账户交易日志</font>。