BGP 高防 IP 提供面向 DDoS 攻击的高级防护策略功能，用户可针对自身业务防护需求对 DDoS 防护策略进行调整和优化。通过黑白名单、禁用协议、禁用端口、报文特征过滤策略以及空连接防护，为业务提供针对性防护。

## 配置项简介

| 配置项       | 功能简介                                                     | 生效时间                                 |
| ------------ | ------------------------------------------------------------ | ---------------------------------------- |
| 黑白名单     | 基于 IP 地址级别的防护。<br/><ul><li>白名单中的 IP，访问时将被直接放行，不经过任何防护策略过滤。</li><li>黑名单中的 IP，访问时将会被直接阻断。</li></ul> | 保存配置后即刻生效。                     |
| 禁用协议     | 可禁用业务不使用的协议。<br/>当检测到攻击行为时，大禹高防集群会清洗掉该协议的流量。 | 保存配置后即刻生效。                     |
| 禁用端口     | 可禁用业务不使用的端口。<br/>当检测到攻击行为时，大禹高防集群会清洗掉该端口的流量 | 保存配置后即刻生效。                     |
| 报文过滤特征 | 可以针对业务报文特征或攻击报文特征，将协议、端口范围、包长范围、是否检测载荷、偏移量、检查深度、是否包括特征字符串等条件进行组合，设定策略动作。<br/>当检测到报文匹配到策略条件时，可以执行丢弃、拉黑源 IP 或断开连接等操作。 | 保存配置后即刻生效。                     |
| 拒绝海外流量 | 可拒绝来自中国（大陆地区及港澳台）以外的 TCP 流量请求。      | 提供防护的高防 IP 处于被攻击状态时生效。 |
| 空连接防护   | 应对空连接攻击。                                             | 提供防护的高防 IP 处于被攻击状态时生效。 |

## 添加新策略

> !高级安全防护策略功能具有一定专业性，建议有相关经验的用户在阅读以下操作指南后根据实际情况进行配置。

登录 [DDoS 防护（大禹）管理控制台](https://console.cloud.tencent.com/dayu/overview)，选择【BGP高防IP】>【防护配置】。在【DDoS高级防护策略】页签，单击【添加新策略】。根据实际业务需求设置以下参数，单击【确定】。
![](https://main.qcloudimg.com/raw/c392ecfccfb97d7533cf406d8ab92e81.png)

- **策略名称**
  输入策略名称，长度为1 - 32个字符，不限制字符类型。
- **黑白名单**
 - 若需设置黑名单：单击【添加】，填写需要拦截的 IP，选择【黑名单】，单击【确定】，即刻生效。
 - 若需设置白名单：单击【添加】，填写需要放行的 IP，选择【白名单】，单击【确定】，即刻生效。

  ![](https://main.qcloudimg.com/raw/8970c1f29d9ee00ecbb86bb7465899a9.png)

- **禁用协议**
  选择需要禁用的协议。
- **禁用端口**
  选择协议，然后填写对应需要禁用的端口。若某条记录中仅需禁用一个端口，则开始端口号和结束端口号填写相同值即可。单击列表下方的【增加】可新增多条记录。
- **报文过滤特征**
  支持将协议、端口范围、包长范围、是否检测载荷、偏移量、检查深度、是否包括特征字符串等条件进行组合，设定策略动作且即刻生效。 

 > ?
 >
 > - 偏移量：表示报文内容中开始匹配的特征的位置。
 > - 检查深度：配合偏移量使用，表示从偏移量设定的位置开始向后匹配的报文内容长度。
 > - 策略：
 >   - “丢弃报文”表示丢弃匹配该报文过滤特征的数据包。
 >   - “丢弃且拉黑源 IP”表示丢弃匹配该报文过滤特征的数据包并将源 IP 临时拉黑一段时间。
 >   - “丢弃且断开连接”表示丢弃匹配该报文过滤特征的数据包并断开 TCP 连接。
 >   - “丢弃，断开连接且拉黑源 IP”表示丢弃匹配该报文过滤特征的数据包，同时断开 TCP 连接并将源 IP 临时拉黑一段时间。

- **拒绝海外流量**
  勾选开启或关闭。BGP 高防 IP 的防护引擎内置海外 IP 库，开启拒绝海外流量后将基于该 IP 库对来源进行判断并执行阻断。处于被攻击状态时生效。
- **空连接防护**
  勾选开启或关闭。处于被攻击状态时生效。

## 绑定与解绑资源

登录 [DDoS 防护（大禹）管理控制台](https://console.cloud.tencent.com/dayu/overview)，选择【BGP高防IP】>【防护配置】。在【DDoS 攻击防护】页签，单击目标策略所在行的【绑定资源】。

- 绑定资源：在弹出的【绑定资源】对话框中，根据实际业务需求勾选一个或多个资源，单击【确定】。
- 解绑资源：在弹出的【绑定资源】对话框中，根据实际业务需求单击【已选择】区域中已选资源右侧的<img src="https://main.qcloudimg.com/raw/f452deeefbca4c66f34b7db71ec0daca.png"  style="margin:0;">，单击【确定】。

## 配置策略

登录 [DDoS 防护（大禹）管理控制台](https://console.cloud.tencent.com/dayu/overview)，选择【BGP高防IP】>【防护配置】。在【DDoS攻击防护】页签，单击目标策略所在行的【配置】。根据实际业务需求更新以下参数，单击【确定】保存修改。

- 策略名称
- 黑白名单
- 禁用协议
- 禁用端口
- 报文过滤特征
- 拒绝海外流量
- 空连接防护

## 删除策略

> ?未绑定资源的策略可直接删除。已绑定资源的策略需要先将所有资源解绑再执行删除操作。

登录 [DDoS 防护（大禹）管理控制台](https://console.cloud.tencent.com/dayu/overview)，选择【BGP高防IP】>【防护配置】。在【DDoS攻击防护】页签，单击目标策略所在行的【删除】。在弹出的对话框中，单击【确定】。
