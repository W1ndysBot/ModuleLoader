# W1ndys-bot

对接 OneBot 的 Python 模块加载器

# 本项目已不再更新，仅供参考开发，新仓库请看 https://github.com/W1ndysBot/W1ndysBot

## 介绍及背景

Python 编写的模块加载器，使用 WebSocket 客户端模式对接上游服务，支持 OneBot 协议，如遇到问题请提 issue

本加载器不以插件的形式进行加载，而是以模块的形式进行加载。

这也就意味着，本加载器的功能增加，直接写代码即可，无需配置相关插件信息。

> 写这个加载器的原因是，了解到了 mf 师傅的插件式加载器，但我本人并不习惯这种方法，于是就写了这个模块式加载器，整个加载器的配置全部采用 Python 模块化编程，功能的开发模式完全基于原生 Onebot11。
>
> 有关插件式加载器的文档请参考：[School-Robot/Plugin-Loader: 用于对接 OneBot 的 Python 插件加载器 (github.com)](https://github.com/School-Robot/Plugin-Loader)

## 加载器特色

- 模块化编程，易于维护
- 支持断线重连，无需手动重启
- 支持上线提醒（QQ），掉线提醒（钉钉）
- 支持 OneBot 11 标准，采用原生的 OneBot 11 标准进行开发

### API 文档

Napcat 开发文档 [开发文档 | NapCatQQ ](https://napneko.github.io/develop/api)

OneBot 11 标准 [botuniverse /onebot-11: OneBot 11 标准 (github.com)](https://github.com/botuniverse/onebot-11#/)

go-cqhttp [API | go-cqhttp 帮助中心](https://docs.go-cqhttp.org/api/)

> 备注：本机器人实现基于 **Python** 做核心开发，使用 **NapCatQQ** 或 **LLOnebot** 作为消息平台，**OneBot 11** 作为 QQ 机器人 API 实现。

## 使用方法

### 安装依赖

```bash
pip install -r requirements.txt
```

### 配置基本信息

#### 配置 ws 连接和管理员

打开`app/config.py`

```python
owner_id = [123]  # 机器人root管理员 QQ 号

ws_url = "xxx"  # 协议端（一般是NapCatQQ、LLOnebot或其他支持ws正向通信监听的客户端）监听的 WebSocket API 地址

token = "xxx"  # 如果需要认证，请填写认证 token
```

#### 配置钉钉通知

打开`app/secret.py`

```python
# 这里替换为你自己的TOKEN，不要直接用我的，我的有IP验证，用我的也没用
DD_BOT_TOKEN = "xxx"
# 这里替换为你自己的SECRET，不要直接用我的，我的有IP验证，用我的也没用
DD_BOT_SECRET = "xxx"
```

## 开发文档

开发功能请参考：[dev.md](dev.md)

## 更新日志

### 2025-01-02

重大更新：重构了回应消息的捕捉逻辑，由原来的 websocke.recv 改成了发送只管发，不具有返回值，由另一个函数捕捉回应消息日志，再进行分析，防止由于多线程导致消息捕捉失败

### 2024-09-09

- feat: 貌似更新了很多，但是我自己用的更新的最及时，参考代码：https://github.com/W1ndys-bot/W1ndys-bot ， 这里是我平时用的，一些代码变动是最早更新的

- feat: 在`api.py`里，其实你也可以根据自己的需求，添加一些常用函数

- feat: 数据存储类型基本以 SQLite 为主

### 2024-08-26

更新了一些细节，默认存储还是 json 文件，后续会更新为 sqlite 数据库

## 友链

[School-Robot/Plugin-Loader: 用于对接 OneBot 的 Python 插件加载器 (github.com)](https://github.com/School-Robot/Plugin-Loader)
