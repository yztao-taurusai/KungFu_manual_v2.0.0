
## 柜台下账户对应字段
##### 添加/设置<font size=6 color="red">```CTP```</font>柜台账户字段

| 字段       | 字段含义     |
| :--------- | :----------- |
| account_id | 账户名称     |
| password   | 账户密码     |
| broker_id  | 券商代码     |
| md_uri     | 行情柜台地址 |
| td_uri     | 交易柜台地址 |
<br/>

##### 添加/设置<font size=6 color="#FAAD14">```XTP```</font>柜台账户字段

| 字段         | 字段含义        |
| :----------- | :-------------- |
| user_id      | 账户名称        |
| password     | 账户密码        |
| td_ip        | 交易柜台IP地址  |
| td_port      | 交易柜台端口    |
| software_key | 用户开发软件KEY |
| md_ip        | 行情柜台IP地址  |
| md_port      | 行情柜台端口    |
<br/>


##交易进程连接状态对应表

| 字段     | 字段颜色                        | 说明                       |
| :------- | :------------------------------ | :------------------------- |
| 未启动   | <font color = grey>灰色</font>  | 交易连接进程未启动         |
| 断开     | <font color = grey>灰色</font>  | 交易连接进程还没和柜台连接 |
| 连接     | <font color = green>绿色</font> | 交易连接进程与柜台连接成功 |
| 登录就绪 | <font color = green>绿色</font> | 交易账户登录柜台成功       |
| 登录失败 | <font color = red>红色</font>   | 交易账户登录柜台失败       |
| 结算确认 | <font color = green>绿色</font> | 交易账户成交结算成功       |
| 结算失败 | <font color = red>红色</font>   | 交易账户成交结算失败       |
| 资金确认 | <font color = green>绿色</font> | 交易账户资金确认成功       |
| 资金错误 | <font color = red>红色</font>   | 交易账户资金确认失败       |
| 持仓确认 | <font color = green>绿色</font> | 交易账户持仓确认成功       |
| 持仓错误 | <font color = red>红色</font>   | 交易账户持仓确认失败       |
| 就绪     | <font color = green>绿色</font> | 交易通道建立成功           |


##行情进程连接状态对应表

| 字段     | 字段颜色                        | 说明                       |
| :------- | :------------------------------ | :------------------------- |
| 未启动   | <font color = grey>灰色</font>  | 行情连接进程未启动         |
| 断开     | <font color = grey>灰色</font>  | 行情连接进程还没和柜台连接 |
| 连接     | <font color = green>绿色</font> | 行情连接进程与柜台连接成功 |
| 登录就绪 | <font color = green>绿色</font> | 行情账户登录柜台成功       |
| 登录失败 | <font color = red>红色</font>   | 行情账户登录柜台失败       |
| 就绪     | <font color = green>绿色</font> | 行情通道建立成功           |

## 