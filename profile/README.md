
你有没有遇到过这种情况：买了一台 VPS，用了几天发现速度很差，换机房又懒得折腾，最后续费的时候心里还隐隐不情愿？

其实这类问题大多数都可以在买之前解决掉，用一个叫 **Looking Glass（LG）** 的工具就行。搬瓦工（BandwagonHost）有好几个机房都提供了 Looking Glass 演示站点，你可以在下单之前，直接从目标机房向你的 IP 发起 traceroute 和 ping，看清楚走的是哪条线路，延迟大概是多少，有没有绕路，再做决定。

这篇文章把搬瓦工所有可用的 Looking Glass 地址整理出来，附带使用方法，最后再按不同使用场景给出套餐推荐——先测速，再下单，踏踏实实。

---

## 什么是 Looking Glass，它能告诉你什么

先说清楚 Looking Glass 是什么，因为确实有不少人把它和 SpeedTest 混淆了。

SpeedTest 测的是你**从本地到服务器**的速度，就是你实际下载、上传的速率。Looking Glass 测的是**从服务器到你**的路由路径，即 traceroute 和 ping。两件事，角度不同，意义也不同。

Looking Glass 更适合用来判断线路质量。买 VPS 的时候，"走不走 CN2 GIA""有没有绕路"这些问题，traceroute 一跑就清楚了。比如：

- 看到路由里出现 `59.43.x.x` 节点，说明走的是电信 CN2 线路
- 全程都是 `59.43.x.x` 直到进入国内，就是 CN2 GIA，不绕路
- 前半段 `59.43`、后半段掉回 `202.97.x.x`，是 CN2 GT，半程优化
- 看到 `AS9929` 或 `AS10099`，是联通精品线路
- 看到 `AS58807`，是移动 CMIN2

知道走什么线，心里才有谱。

---

## 场景一：电信用户，追求低延迟建站 → 用 DC6 / DC9 LG 测试

电信用户对 CN2 GIA 的感知最明显。搬瓦工 DC6 CN2 GIA-E 和 DC9 CN2 GIA 这两个洛杉矶机房，是电信用户公认性价比最高的选择。三网回程都接入 CN2 GIA，延迟通常在 150-180ms 左右，丢包率极低。

**DC6 CN2 GIA-E Looking Glass：**
👉 [https://dc6.bwg.net/lg/en.php](https://bwh81.net/aff.php?aff=80238)（访问页面后输入你的本地 IP，选择 traceroute 测试）

- 机房编号：USCA_6，美国洛杉矶
- 测试 IPv4：162.244.241.102

**DC9 CN2 GIA Looking Glass：**
👉 [https://dc9.bwg.net/lg/](https://bwh81.net/aff.php?aff=80238)（同上操作）

- 机房编号：USCA_9，美国洛杉矶
- 测试 IPv4：65.49.131.102

打开页面之后，找到输入框，把你自己的本地 IP 填进去（不知道自己 IP 可以先百度"我的 IP"），然后在测试类型里选 **traceroute**，点击测试。结果输出会显示每一跳的节点、AS 号、地理位置和延迟。

如果你是电信用户，看到回程路由里出现 `59.43` 开头的节点并且全程没有掉落到 `202.97`，那就说明走的是 CN2 GIA，可以放心买。

这两个机房对应的是搬瓦工 CN2 GIA-E 套餐。进入 LG 页面之后，你也可以直接打开 SpeedTest 那一侧测试下载速度。👉 [点击查看 CN2 GIA-E 套餐详情](https://bwh81.net/aff.php?aff=80238&pid=87)

---

## 场景二：联通用户，跑欧洲线路 → 用荷兰 EUNL_9 LG 测试

搬瓦工有一个比较特殊的机房：荷兰阿姆斯特丹 EUNL_9，走的是联通 AS9929 + AS10099 精品线路。这条线路对联通用户来说体验非常好——联通骨干到荷兰直连，基本不绕路。

荷兰机房没有独立 LG 页面，但它属于 CN2 GIA-E 套餐的可选机房，你可以先用 DC9 的 LG 测个大方向，再购入后迁机房到 EUNL_9 看实际效果。或者直接 ping 荷兰机房测试 IP：`185.212.170.234`，看一下延迟。

对于联通用户来说，CN2 GIA-E 套餐购买后可以一键迁移到荷兰 EUNL_9，不需要多花钱。

👉 [CN2 GIA-E 套餐 1G 版，$49.99/季，12 个机房任意切换](https://bwh81.net/aff.php?aff=80238&pid=87)

---

## 场景三：移动用户，追求日本方向 → 用 JPOS 软银 LG 测试

移动用户走日本方向，感觉是最好的，尤其是日本软银（JPOS_1）这个机房，三网对软银线路都很友好。

**日本大阪软银 Looking Glass：**
👉 [https://jpos.bwg.net/lg/](https://bwh81.net/aff.php?aff=80238)

- 机房编号：JPOS_1，日本大阪
- 测试 IPv4：185.212.59.222

用法和前面一样：输入本地 IP，选 traceroute，看回程路由里有没有 SoftBank 的节点标识（BBTec/BBTEC），有就说明走的是软银线路，移动用户体验不会差。

这个机房同样属于 CN2 GIA-E 套餐可选机房，一套买了可以在多个机房之间随意切换。

---

## 场景四：入门用户，预算有限 → 用 DC3 / FMT LG 测个底

搬瓦工最便宜的入门套餐，默认机房是 DC2，可以迁移到 DC3（CN2 GT）、DC8、弗里蒙特（FMT）等机房。

对于没有特别高速要求的用户，比如只是学习 Linux 或者搭个博客，这些机房完全够用。

**DC3 CN2 Looking Glass：**
👉 [https://dc3.bwg.net/lg/](https://bwh81.net/aff.php?aff=80238)

- 机房编号：USCA_3，美国洛杉矶
- 测试 IPv4：23.252.103.101

**弗里蒙特 Fremont Looking Glass：**
👉 [https://fmt.bwg.net/lg/en.php](https://bwh81.net/aff.php?aff=80238)

- 机房编号：USCA_FMT，美国弗里蒙特
- 测试 IPv4：184.105.138.67

DC3 走的是 CN2 GT，下午两三点延迟还好，但晚高峰可能有波动。弗里蒙特机房走的是 HE（Hurricane Electric）国际线路，适合对国内速度要求不高的国际业务。

如果预算实在有限，入门套餐年付 $49.99，用优惠码 **BWHCGLUKKB** 打折之后约 $46.6，一天不到一块三，够折腾好一阵了。

👉 [点击查看入门套餐，1G/20G SSD/1T 月流量，$49.99/年](https://bwh81.net/aff.php?aff=80238&pid=44)

---

## 场景五：企业/电商用户，要求稳定性 → 电商 SLA 套餐 + DC5 机房

2025 年底搬瓦工推出了一个专门面向电商/高稳定性需求的套餐系列：**E-Commerce SLA VPS**，对应的机房是 DC5（USCA_5），承诺 99.99% 在线时间，线路走三网高端路线（电信 CN2 GIA + 联通 9929 + 移动 CMIN2），还有每两周可免费换一次 IP 的特权。

这个套餐没有单独的 LG 站点，但它和 DC9 同在洛杉矶，路由方向相似。可以用 DC9 的 LG 先测一下大方向，实际购入之后效果只会更好不会更差。

---

## 搬瓦工全套餐价格对比表

下面整理了搬瓦工目前官网在售的所有主要套餐系列，方便一眼看完做决策：

| 套餐系列 | 内存 | CPU | 硬盘 | 月流量 | 带宽 | 价格 | 可选高速机房 | 购买 |
|---|---|---|---|---|---|---|---|---|
| **KVM / CN2 GT 入门** | 1G | 2核 | 20G SSD | 1T | 1Gbps | $49.99/年 | DC3 CN2 GT、DC8、FMT等9个 |  [立即购买](https://bwh81.net/aff.php?aff=80238&pid=44) |
| **KVM / CN2 GT** | 2G | 3核 | 40G SSD | 2T | 1Gbps | $52.99/半年 | 同上 |  [立即购买](https://bwh81.net/aff.php?aff=80238&pid=45) |
| **KVM / CN2 GT** | 4G | 4核 | 80G SSD | 3T | 1Gbps | $19.99/月 | 同上 |  [立即购买](https://bwh81.net/aff.php?aff=80238&pid=46) |
| **CN2 GIA-E 推荐** | 1G | 2核 | 20G SSD | 1T | 2.5Gbps | $49.99/季 | DC6、DC9、日本软银、荷兰9929、加拿大 等12个 |  [立即购买](https://bwh81.net/aff.php?aff=80238&pid=87) |
| **CN2 GIA-E** | 2G | 3核 | 40G SSD | 2T | 2.5Gbps | $89.99/季 | 同上 |  [立即购买](https://bwh81.net/aff.php?aff=80238&pid=88) |
| **CN2 GIA-E** | 4G | 4核 | 80G SSD | 3T | 2.5Gbps | $56.99/月 | 同上 |  [立即购买](https://bwh81.net/aff.php?aff=80238&pid=89) |
| **E-Commerce SLA** | 1G | 2核(AMD独享) | 20G NVMe | 1T | 2.5Gbps | $65.89/季 | DC5 SLA（CN2 GIA+9929+CMIN2） |  [立即购买](https://bwh81.net/aff.php?aff=80238&pid=164) |
| **E-Commerce SLA** | 2G | 3核 | 40G NVMe | 2T | 2.5Gbps | $116.99/季 | 同上 |  [立即购买](https://bwh81.net/aff.php?aff=80238&pid=165) |
| **香港 CN2 GIA 高端** | 2G | 2核 | 40G SSD | 500G | 1Gbps | $89.99/月 | 香港 HKHK_8（最快，延迟30-60ms） |  [立即购买](https://bwh81.net/aff.php?aff=80238&pid=95) |
| **香港 CN2 GIA** | 4G | 4核 | 80G SSD | 1T | 1Gbps | $155.99/月 | 同上 |  [立即购买](https://bwh81.net/aff.php?aff=80238&pid=96) |
| **日本大阪 CN2 GIA** | 2G | 2核 | 40G SSD | 0.5T | 1.5Gbps | $49.99/月 | 日本大阪 JPOS_6 |  [立即购买](https://bwh81.net/aff.php?aff=80238&pid=134) |
| **日本东京 CN2 GIA** | 2G | 2核 | 40G SSD | 0.5T | 1.2Gbps | $89.99/月 | 日本东京 JPTYO_8 |  [立即购买](https://bwh81.net/aff.php?aff=80238&pid=108) |
| **阿联酋迪拜** | 1G | 2核 | 20G SSD | 500G | 1Gbps | $19.99/月 | 迪拜+CN2 GIA+日本软银等14个 |  [立即购买](https://bwh81.net/aff.php?aff=80238&pid=114) |

> **优惠码**：购买时在 Promotional Code 处填入 **BWHCGLUKKB**，全场常规套餐循环折扣约 6.77%，续费同样有效。

---

## Looking Glass 使用方法：三步搞定

买 VPS 之前用 LG 测试的流程很简单，我把步骤拆细一点：

**第一步：找到你的本地 IP**

打开浏览器搜索"我的 IP"或者访问 `ip.sb`，记下你的公网 IP 地址。

**第二步：打开对应机房的 LG 页面**

根据你感兴趣的机房选对应的地址（上面各场景里都列出来了），打开页面。

**第三步：选测试类型，输入 IP 开始测**

LG 页面里通常有四个测试选项：
- **ping**：从服务器 ping 你的 IP，看往返延迟
- **traceroute**：路由追踪，看每一跳经过哪些节点，适合判断走什么线路
- **mtr**：综合测试，兼具 ping 和 traceroute，还能看丢包率
- **host**：域名解析，一般用不到

建议把 **traceroute** 和 **mtr** 都跑一遍，结合着看，更全面。

---

## 各场景推荐小结

| 使用场景 | 推荐机房 | 推荐套餐 | 参考价格 |
|---|---|---|---|
| 电信用户建站 | DC6 CN2 GIA-E / DC9 CN2 GIA | CN2 GIA-E | $49.99/季起 |
| 联通用户 | 荷兰 EUNL_9（AS9929） | CN2 GIA-E | $49.99/季起 |
| 移动用户 | 日本软银 JPOS_1 | CN2 GIA-E | $49.99/季起 |
| 极低预算学习用 | DC3 / DC8 / FMT | KVM/CN2 GT入门 | $49.99/年起 |
| 电商/高稳定业务 | DC5 SLA | E-Commerce SLA | $65.89/季起 |
| 对延迟极度敏感 | 香港 HKHK_8 | 香港CN2 GIA | $89.99/月起 |
| 日本区用户/AI服务 | 日本大阪 JPOS_6 | 日本大阪CN2 GIA | $49.99/月起 |

---

## 几个实用的测试 IP，备用

不想用 LG 网页，也可以直接在本地 ping 或者 mtr 跑这些官方测试 IP：

| 机房 | 测试 IP |
|---|---|
| DC3 CN2（USCA_3） | 23.252.103.101 |
| DC6 CN2 GIA-E（USCA_6） | 162.244.241.102 |
| DC9 CN2 GIA（USCA_9） | 65.49.131.102 |
| DC2 QNET（USCA_2） | 23.252.96.201 |
| 日本大阪软银（JPOS_1） | 185.212.59.222 |
| 弗里蒙特（USCA_FMT） | 184.105.138.67 |

本地 Windows 用户直接打开命令提示符运行 `ping 上面某个IP` 就行。想看路由就 `tracert IP`。Linux / macOS 用户用 `mtr IP` 更方便。

---

## 最后说两句

Looking Glass 不是万能的，它能告诉你路由走向和瞬时延迟，但跑出来的结果只是一个参考——你自己的网络环境（运营商、地区、时段）才是最终决定因素。建议至少在晚高峰（20:00-23:00）测一次，平峰期和晚高峰差别有时候很大，特别是便宜套餐。

搬瓦工 30 天内支持退款，实在买了不满意还可以退。但与其买了再退，不如买前多跑几次 LG，心里有底再下单。

👉 [查看所有搬瓦工套餐，按需选购](https://bwh81.net/aff.php?aff=80238)
