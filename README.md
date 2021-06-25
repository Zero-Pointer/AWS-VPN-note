# AWS-VPN-note
## 一、拥有一个 AWS 账号

这一步需要一个 :credit_card: **外币信用卡**，大学生身份是比较好注册的。

不过申请下来的可能会没有额度，不过也**没有年费**，我就直接往里打钱当外币储蓄卡用了。

---

## 二、创建一个 EC2 实例

- [x] 进入 [EC2 Dashboard](https://ap-northeast-2.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-2#Home:)
- [x] 选择目标 VPN 节点
- [x] 点击 *实例* 选项
- [x] 点击 *启动新实例*
- [x] 选择操作系统，我这里选择的是 **Ubuntu18.04**
- [x] 选择实例类型，我选择的是唯一免费的那个
- [x] 点击*审核和启动*
- [x] 设置安全组，如下图（最后的 8388 端口是为后文做准备）
  ![image-20210524214618407](img/image-20210524214618407.png)
- [x] 设置密钥对，开始*启动*

---

## 三、配置 EC2

- [x] 安装 Shadowsocks 服务端

```shell
sudo apt-get -y update && sudo apt-get install python-pip python-setuptools m2crypto shadowsocks
```

- [x] 创建配置文件

```shell
cd ~
mkdir ss
cd ss
```

- [x] 打开 *ss.json*，输入配置信息

```shell
vim ss.json
```

```json
{
"server":"0.0.0.0",
"server_port":8388,
"local_address": "127.0.0.1",
"local_port":1080,
"password":"zpttest",
"timeout":600,
"method":"aes-256-cfb"
}
```

- [x] 前台启动服务（能看到 Log 信息，退出控制台就关闭服务）

```shell
ssserver -c ~/ss/ss.json
```

- [x] 后台启动服务（后台挂起，看不到提示信息，退出控制台能依旧运行）

```shell
nohup ssserver -c ~/ss/ss.json >/dev/null 2>&1 &
```

[参考资料](https://viencoding.com/article/90)

---

## 四、客户端测试

- [x] 安装 Shadowsocks，我的是 4.2.0.0
- [x] 配置 **服务器IP** 和**密码**
- [x] 开启服务
- [x] [打开 Google](https://www.google.com)

---

## End、怎么查看自己的免费资源使用量

- [x] 在搜索框中搜索 **billing**

