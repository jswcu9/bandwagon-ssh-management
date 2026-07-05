# 搬瓦工 SSH 密码怎么查、怎么改、改完忘了怎么办：三种情况全解析，附套餐选购指南

买完搬瓦工，SSH 连不上——这几乎是每个新手都会卡的第一关。

有时候是密码压根没记，有时候是邮件找不到了，有时候是改了密码但忘了改哪儿。还有一种情况：KiwiVM 面板里点了 Generate 按钮，结果提示 "Failed to reset root password (739102)"，不知道哪出了问题。

这篇文章把搬瓦工 SSH 密码相关的问题一次性说清楚，包括初始密码在哪找、KiwiVM 怎么重置、SSH 登录进去后怎么改成自己能记住的密码，以及常见报错的解法。

---

## 搬瓦工 SSH 密码是什么

先把概念搞清楚。

搬瓦工 VPS 的 **SSH 密码 = root 密码**，就是你用 Xshell、FinalShell、Termius 这类工具远程连 VPS 时填的那个密码。用户名默认是 `root`（全小写），端口是一个随机生成的四五位数字（不是 22，这是搬瓦工和大多数 VPS 厂商不一样的地方）。

搬瓦工的密码和端口都是系统随机生成的，初始的 root 密码是一串大小写字母加数字混合的随机字符串，记起来确实麻烦。

---

## 方法一：从邮件里找初始密码

买完搬瓦工之后，系统会发一封邮件，标题一般是类似 "KiwiVM: OS Reload on localhost.localdomain [IP地址]" 的格式，里面包含：

- VPS 的 IP 地址
- SSH 端口号
- 初始 root 密码

**问题是这封邮件很容易进垃圾箱。** 特别是用 Gmail 以外邮箱注册的朋友，大概率要去垃圾邮件里翻一翻。

找不到也没关系，还有 KiwiVM 这条路。

---

## 方法二：通过 KiwiVM 面板重置 SSH 密码

这是最常用的方法，适合密码忘了或者邮件找不到的情况。步骤如下：

1. 登录搬瓦工官网账户，进入 **Services → My Services**
2. 找到你的 VPS 实例，点击 **KiwiVM Control Panel** 按钮
3. 确认 VPS 状态是 **Running**（这一步很关键，下面会说为什么）
4. 点击左侧菜单的 **Root password modification**
5. 点击 **Generate and set new root password** 按钮
6. 页面会刷新，用绿色背景显示出新密码

**注意：这个密码只会显示这一次，页面关闭或刷新后就再也看不到了。立刻复制保存。**

没记下来也没关系，再点一次 Generate 就行，多重置几次不影响 VPS 运行。

👉 [进入搬瓦工官网，开始操作](https://bit.ly/BanWaGon)

---

## 常见报错：Failed to reset root password (739102)

这是很多人卡住的地方。

报错的完整提示通常是：

> Failed to reset root password (739102)  
> Additional information: 992800002 VPS is currently stopped. Please make sure VPS is fully booted before attempting to modify root password.

翻译过来就一句话：**VPS 没开机，不能重置密码。**

之前的旧教程说重置密码要先关机，那是以前的逻辑，现在已经完全反过来了——必须在 VPS **开机状态（Running）** 下才能重置密码。

解决方法很简单：回到 KiwiVM 面板首页，点 **Start** 把 VPS 开机，等状态变成 Running，再去点密码重置。

---

## 方法三：SSH 登录后直接改成自己能记住的密码

KiwiVM 的 Generate 功能生成的是随机密码，每次都是一串没规律的字符串，用起来要复制粘贴，有时候在手机上操作还很麻烦。

如果想改成自己设定的密码，有两种方法：

### 方法 3A：通过 KiwiVM 的 Root Shell 修改

不需要额外的 SSH 客户端，在 KiwiVM 面板里就能操作。

1. 进入 KiwiVM 面板，点左侧的 **Root shell - interactive**
2. 输入命令：
   
   passwd
   
3. 按提示输入新密码两次（输入时屏幕不显示字符，这是正常的）
4. 出现 `passwd: all authentication tokens updated successfully.` 说明修改成功

### 方法 3B：通过 SSH 客户端修改

先用旧密码登进 VPS，然后执行：

bash
passwd


接着按提示输入新密码两次确认就好。

**密码建议设置大写字母 + 小写字母 + 数字的组合，纯数字或者太短的密码容易被暴力扫描。**

---

## 登录 SSH 需要的三样东西

趁这个机会把完整的登录信息整理一下，缺一不可：

| 信息 | 说明 | 在哪找 |
|------|------|--------|
| IP 地址 | 服务器的公网 IP | KiwiVM 面板首页 |
| SSH 端口 | 搬瓦工不是默认的 22，是随机分配的 | KiwiVM 面板首页 |
| 用户名 | 固定是 `root` | 不需要查 |
| 密码 | root 密码 | 开通邮件 / KiwiVM 重置 |

Windows 上比较好用的 SSH 客户端是 **Termius** 或 **FinalShell**，macOS 和 Linux 直接用系统自带终端就行：

bash
ssh root@你的IP -p 你的端口


---

## 搬瓦工目前在售套餐一览

既然到这里了，顺手把现在搬瓦工的主要套餐整理一下，方便还没买或者想升级的朋友参考。

| 套餐系列 | 月流量 | 内存 | 硬盘 | 价格 | 适合场景 | 购买 |
|----------|--------|------|------|------|----------|------|
| KVM 入门款 | 1TB | 1GB | 20G SSD | $49.99/年 | 学 Linux、跑脚本 |  [选择此方案](https://bit.ly/BanWaGon) |
| CN2 GIA-E（性价比款） | 1TB | 1GB | 20G SSD | $169.99/年 / $49.99/季 | 建站、日常使用 |  [选择此方案](https://bit.ly/BanWaGon) |
| CN2 GIA-E（大流量款） | 2TB | 2GB | 40G SSD | $299.99/年 / $89.99/季 | 流量需求较大 |  [选择此方案](https://bit.ly/BanWaGon) |
| 日本大阪 CN2 GIA | 1TB | 2GB | 40G SSD | $499.99/年 / $49.99/月 | 低延迟需求 |  [选择此方案](https://bit.ly/BanWaGon) |
| 香港 CN2 GIA（小流量） | 500GB | 2GB | 40G SSD | $899.99/年 / $89.99/月 | 追求极低延迟 |  [选择此方案](https://bit.ly/BanWaGon) |
| 香港 CN2 GIA（大流量） | 1TB | 4GB | 80G SSD | $1559.99/年 / $155.99/月 | 高端需求 |  [选择此方案](https://bit.ly/BanWaGon) |

说实话，大多数人买搬瓦工的理由就是线路质量好，如果只是入门玩玩，KVM 套餐 $49.99/年足够，算下来一天一毛多。

有正经建站或者对速度有要求的，CN2 GIA-E 是性价比最高的档——$49.99 季付，12 个机房可以随时切换，遇到某个机房抽风可以直接换，这个灵活性很好用。

香港套餐价格不低，但三网延迟真的很低，广东方向延迟个位数。预算够的当然可以考虑。

👉 [查看搬瓦工当前所有套餐与折扣](https://bit.ly/BanWaGon)

---

## 关于付款方式

搬瓦工支持支付宝、银联、PayPal、信用卡。国内用户用支付宝最方便，不用考虑汇率问题，结账时选 Alipay 直接扫码就行。

---

## FAQ：搬瓦工 SSH 密码常见问题

**Q：搬瓦工的 SSH 用户名是什么？**  
A：固定是 `root`，小写，所有套餐都一样。

**Q：SSH 端口是 22 吗？**  
A：不是，搬瓦工的 SSH 端口是随机生成的，一般是一个四五位数字。在 KiwiVM 面板首页可以看到，字段名是 SSH Port。

**Q：重置密码之后 VPS 里的数据会不会丢失？**  
A：不会。重置 root 密码只修改登录凭据，不影响 VPS 里的文件和配置。

**Q：可以把 root 密码改成自己指定的密码吗？**  
A：KiwiVM 面板的 Generate 功能只能生成随机密码。想设置自定义密码，要通过 Root Shell 或者 SSH 登录后执行 `passwd` 命令来改。

**Q：重置密码后新密码只显示一次是什么意思？**  
A：点击 Generate 后，新密码会出现在页面顶部，但关闭页面或刷新之后就看不到了。如果没记下来，再点一次 Generate 重置就行。

**Q：搬瓦工退款政策是怎么样的？**  
A：搬瓦工支持 30 天内退款，不满意可以申请全额退款。

---

遇到 SSH 连不上的情况，九成九是这几个原因：密码错了、端口写错了、VPS 没开机。按上面的步骤一项一项确认，基本都能解决。

👉 [前往搬瓦工官网，获取最新套餐优惠](https://bit.ly/BanWaGon)
