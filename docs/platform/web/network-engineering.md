# Network Engineering

## 参考模型

OSI 参考模型：

- 物理层
- 数据链路层
- 网络层
- 传输层
- 会话层
- 表示层
- 应用层

TCP/IP 协议：

- 网络接口层（包含 OSI 的物理层、数据链路层）
- 网络层（IP）
- 传输层（TCP、UDP）
- 应用层（HTTP）

## IP

### 分类

- A 0 0~127
- B 10 128~191
- C 110 192~223
- D 1110
- E 1111

私有地址和保留地址：

- private `10.*.*.*`
- loopback `127.*.*.*`
- private `172.16.*.*` ~ `172.31.*.*`
- private `192.168.*.*`

网络地址和广播地址也是 IP 地址的形式。

- 网络地址 全0
- 广播地址 全1

## 应用层

- FTP（数据连接20 控制连接21）
- SSH（22）
- Telnet（23）
- SMTP（25）
- DNS（53）
- DHCP（服务器67 客户端68）
- TFTP（69）
- POP3（110）
- SNMP, Simple Network Management Protocol（服务器161 客户端162）

---

## 交换机

- Trunk PVID

### STP

- Disabled 无
- Blocking 接收配置BPDU
- Listening Blocking的所有动作，并发送配置BPDU
- Learning Listening的所有动作，并进行MAC地址学习
- Forwarding Learning的所有动作，并收发数据

BridgeID = 优先级值 + MAC地址，越小越优先。

STP => RSTP（缩短收敛时间） => MSTP（负载分担）

## 路由器

### OSPF

- IP:89
- 只与 BDR 和 DR 建立邻接关系。
- 先选举 BDR 再选举 DR。
- 只有 BDR 和 DR 都失效后再重新选举。

DR 选举细节：

- 优先级为 0 没有选举资格，选举优先级最高（相同时选举路由器 ID 最大）者。
