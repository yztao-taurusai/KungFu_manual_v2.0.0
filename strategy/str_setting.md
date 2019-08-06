# 策略维护

&emsp;&emsp;在KungFu交易系统中，策略模块相当于系统的策略池，用户可以根据实际需要，在策略模块中对已有策略进行编辑修改和删除，同时可以查看到每一个策略实时的持仓情况、委托情况、成交情况、盈亏情况以及交易日志

<div align=center><img src="/images/add_str.png" width="640" height="400" alt = "添加策略">

### 策略设置

&emsp;&emsp;在实际使用中，如果用户需要修改策略的本地文件路径，可以点击策略右侧相应的<font color = 'red'>```设置```</font>按钮，重新绑定新的策略文件


<div align=center><img src="/images/str_set.png" width="640" height="300" alt = "策略设置">


&emsp;&emsp;<font color = red>如果策略正在运行，需要重启策略后，策略新绑定的文件路径才能生效</font>

### 策略编辑

&emsp;&emsp;在KungFu交易系统中，内嵌了IDE，用户可以在KungFu系统中编写本地策略，点击策略右侧相应的<font color = 'red'>```编辑```</font>按钮，会有策略编辑IDE弹窗，在弹窗内，用户可以对策略绑定的本地文件进行编辑，在KungFu内嵌的IDE中，支持

- 创建新的文件
- 创建新的文件夹
- 编译已有文件内容
- 重命名已有文件

<div align=center><img src="/images/str_edit.png" width="640" height="400" alt = "策略编辑">

### 删除策略

&emsp;&emsp;在删除不需要的策略之前，需要保证策略处于关闭状态，需要注意的是，策略删除成功后，系统会将该策略的所有相关信息都删除，其中包括策略持仓信息、策略委托信息、策略成交信息、策略盈亏信息、策略交易日志信息。

