# Docker Compose 项目使用指南

本项目使用 Docker Compose 配置了 Caddy 和 Dozzle，让你能够通过 HTTPS 安全地访问 Dozzle 来查看和管理 Docker 容器。

## 项目结构

- `docker-compose.yaml`: Docker Compose 配置文件
- `Caddyfile`: Caddy 服务器配置文件
- `caddy/`: Caddy 数据目录

## 使用步骤

### 1. 启动项目

使用以下命令启动项目：

```bash
docker compose up -d
```

这将启动 Caddy 和 Dozzle 服务。

### 2. 添加 Caddy 根证书到系统并信任

Caddy 生成的根证书位于以下路径：

```
./caddy/data/caddy/pki/authorities/local/root.crt
```

#### macOS 系统操作步骤

1. 打开终端并运行以下命令：

```bash
sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain ./caddy/data/caddy/pki/authorities/local/root.crt
```

2. 输入您的管理员密码

#### Linux 系统操作步骤

Debian/Ubuntu：
```bash
sudo cp ./caddy/data/caddy/pki/authorities/local/root.crt /usr/local/share/ca-certificates/
sudo update-ca-certificates
```

CentOS/RHEL：
```bash
sudo cp ./caddy/data/caddy/pki/authorities/local/root.crt /etc/pki/ca-trust/source/anchors/
sudo update-ca-trust
```

#### Windows 系统操作步骤

1. 双击证书文件
2. 选择"安装证书"
3. 选择"本地计算机"并点击"下一步"
4. 选择"将所有证书放入下列存储"，点击"浏览"
5. 选择"受信任的根证书颁发机构"，点击"确定"
6. 点击"下一步"然后"完成"

### 3. 访问 Dozzle

在浏览器中访问以下地址：

```
https://dozzle.localhost
```

现在您可以通过安全的 HTTPS 连接查看和管理您的 Docker 容器。

## 停止项目

使用以下命令停止项目：

```bash
docker compose down
```

## 故障排除

如果浏览器仍然显示证书不信任，请尝试：

1. 确保您正确导入了根证书
2. 重启浏览器
3. 在某些情况下，您可能需要重启计算机
