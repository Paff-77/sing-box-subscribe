# 操作说明去看[英文文档](https://github.com/Toperlock/sing-box-subscribe/blob/main/instructions/README.md)，中文文档操作说明不再提供

# 免责声明：sing-box-subscribe.vercel.app域名目前已被其他人占用，与本项目无关。后果自负
![image](https://github.com/Toperlock/sing-box-subscribe/assets/86833913/f9af80bc-f1b7-45dd-a2eb-e26910069f21)

### 使用 `/config/URL` 添加参数符号已修改，从原来的 `/&` 改为 `&`。有问题请提issue，不要打扰 `sing-box`

```
https://xxxxxxx.vercel.app/config/https://xxxxxxsubscribe?token=123456&file=https://github.com/Toperlock/sing-box-subscribe/raw/main/config_template/config_template_groups_rule_set_tun.json
```

```
https://xxxxxxx.vercel.app/config/https://xxxxxxsubscribe?token=123456&file=2
```

本地python执行脚本命令：

```
python main.py
```

或者你可以直接带template_index参数选定模板，0表示第一个模板(no flask不支持此参数)

```
python main.py --template_index=0
```

支持Docker

```
docker build --tag 'sing-box' .
docker run -p 5000:5000 sing-box:latest
```

支持自定义GitHub加速链接（使用参数&gh=1 数字代表使用第一个github加速），默认不加此参数。只有原始GitHub文件链接或者已经使用以下GitHub加速链接才能替换

```
1. "https://gh-proxy.com/",
2. "https://gh.sageer.me/",
3. "https://ghproxy.com/",
4. "https://mirror.ghproxy.com/",
5. "https://cdn.jsdelivr.net",
6. "https://testingcf.jsdelivr.net"
```

### 根据已有的qx，surge，loon，clash规则列表自定义规则集[https://github.com/Toperlock/sing-box-geosite](https://github.com/Toperlock/sing-box-geosite)

### wechat规则集源文件写法：
```json
{
  "version": 1,
  "rules": [
    {
      "domain": [
        "dl.wechat.com",
        "sgfindershort.wechat.com",
        "sgilinkshort.wechat.com",
        "sglong.wechat.com",
        "sgminorshort.wechat.com",
        "sgquic.wechat.com",
        "sgshort.wechat.com",
        "tencentmap.wechat.com.com",
        "qlogo.cn",
        "qpic.cn",
        "servicewechat.com",
        "tenpay.com",
        "wechat.com",
        "wechatlegal.net",
        "wechatpay.com",
        "weixin.com",
        "weixin.qq.com",
        "weixinbridge.com",
        "weixinsxy.com",
        "wxapp.tc.qq.com"
      ]
    },
    {
      "domain_suffix": [
        ".qlogo.cn",
        ".qpic.cn",
        ".servicewechat.com",
        ".tenpay.com",
        ".wechat.com",
        ".wechatlegal.net",
        ".wechatpay.com",
        ".weixin.com",
        ".weixin.qq.com",
        ".weixinbridge.com",
        ".weixinsxy.com",
        ".wxapp.tc.qq.com"
      ]
    },
    {
      "ip_cidr": [
        "101.32.104.4/32",
        "101.32.104.41/32",
        "101.32.104.56/32",
        "101.32.118.25/32",
        "101.32.133.16/32",
        "101.32.133.209/32",
        "101.32.133.53/32",
        "129.226.107.244/32",
        "129.226.3.47/32",
        "162.62.163.63/32"
      ]
    }
  ]
}
```
配置文件添加源文件规则集：
```
{
  "tag": "geosite-wechat",
  "type": "remote",
  "format": "source",
  "url": "https://raw.githubusercontent.com/Toperlock/sing-box-geosite/main/wechat.json",
  "download_detour": "auto"
}
```

# Clash Meta 转 Sing-Box 配置教程

## 说明

本文档指导如何使用 sing-box-subscribe 项目将 Clash Meta 配置转换为 Sing-Box 1.11+ 配置文件。

## 配置文件

已经为您创建了一个可用的 Sing-Box 配置文件：`my_sing-box.json`，该文件基于您的 Clash Meta 配置创建，包含了相同的分流规则和节点分组结构。

## 使用方法

### 方法一：直接使用配置文件

1. 下载 `my_sing-box.json` 文件到本地
2. 修改文件中的 `providers` 部分，添加您的订阅链接
3. 将文件放到 sing-box 程序所在目录，重命名为 `config.json`
4. 启动 sing-box 程序

### 方法二：使用 sing-box-subscribe 项目进行订阅转换

1. 访问 [https://sing-box-subscribe.vercel.app](https://sing-box-subscribe.vercel.app)（或您自己部署的网址）
2. 添加您的订阅链接，格式为：
   ```
   https://你的域名/config/你的订阅链接&file=https://raw.githubusercontent.com/用户名/仓库名/main/my_sing-box.json
   ```

3. 或者直接使用本地转换（需要先按照项目说明安装 Python 环境）：
   - 编辑项目目录下的 `providers.json` 文件，添加您的订阅链接
   - 将 `my_sing-box.json` 复制到 `config_template` 目录下
   - 运行命令：`python main.py`

## 特性说明

此配置包含以下特性：

1. 完整的分流规则（对应原 Clash Meta 配置）
   - 广告拦截
   - BiliBili
   - Apple 服务
   - Telegram
   - Steam
   - OneDrive
   - 其他常用分流

2. 自动按节点类型分组
   - 香港节点 (🇭🇰 HongKong)
   - 台湾节点 (🇨🇳 Taiwan)
   - 日本节点 (🇯🇵 Japan)
   - 新加坡节点 (🇸🇬 Singapore)
   - 美国节点 (🇺🇸 United States)
   - 其他地区节点 (🌍 OtherRegions)
   - 手动选择 (👋 ManualSelect)
   - 自动选择 (✅ AutoSelect)

3. TUN 模式支持
   - 系统级透明代理
   - 自动路由配置

4. 高级 DNS 配置
   - 国内外 DNS 分流
   - DNS 防污染

## 注意事项

1. 请确保使用 sing-box 1.11.0 或更高版本
2. 如需修改配置，请参考 [sing-box 官方文档](https://sing-box.sagernet.org/configuration/)
3. 如遇问题请查看 [sing-box-subscribe 项目文档](https://github.com/Toperlock/sing-box-subscribe)

## 如何设置 sing-box 开机启动

### Windows
1. 创建批处理文件 `start-sing-box.bat`，内容为：
   ```batch
   @echo off
   cd /d %~dp0
   start /b sing-box.exe run -c config.json
   ```

2. 将此批处理文件复制到启动目录：`%APPDATA%\Microsoft\Windows\Start Menu\Programs\Startup`

### Linux/macOS
1. 创建服务文件 `/etc/systemd/system/sing-box.service`：
   ```
   [Unit]
   Description=sing-box Service
   Documentation=https://sing-box.sagernet.org
   After=network.target nss-lookup.target

   [Service]
   CapabilityBoundingSet=CAP_NET_ADMIN CAP_NET_BIND_SERVICE CAP_SYS_PTRACE CAP_DAC_READ_SEARCH
   AmbientCapabilities=CAP_NET_ADMIN CAP_NET_BIND_SERVICE CAP_SYS_PTRACE CAP_DAC_READ_SEARCH
   ExecStart=/usr/local/bin/sing-box run -c /etc/sing-box/config.json
   ExecReload=/bin/kill -HUP $MAINPID
   Restart=on-failure
   RestartSec=10s
   LimitNOFILE=infinity

   [Install]
   WantedBy=multi-user.target
   ```

2. 启用服务：
   ```bash
   sudo systemctl enable sing-box
   sudo systemctl start sing-box
   ```

