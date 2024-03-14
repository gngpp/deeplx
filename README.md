[![CI](https://github.com/gngpp/deeplx/actions/workflows/release.yml/badge.svg)](https://github.com/gngpp/deeplx/actions/workflows/release.yml)
 <a target="_blank" href="https://github.com/gngpp/deeplx/blob/main/LICENSE">
  <img src="https://img.shields.io/badge/license-MIT-blue.svg"/>
 </a>
  <a href="https://github.com/gngpp/deeplx/releases">
    <img src="https://img.shields.io/github/release/gngpp/deeplx.svg?style=flat">
  </a>
  </a><a href="https://github.com/gngpp/deeplx/releases">
    <img src="https://img.shields.io/github/downloads/gngpp/deeplx/total?style=flat">
  </a>
  [![](https://img.shields.io/docker/image-size/gngpp/deeplx)](https://registry.hub.docker.com/r/gngpp/deeplx)
  [![Docker Image](https://img.shields.io/docker/pulls/gngpp/deeplx.svg)](https://hub.docker.com/r/gngpp/deeplx/)

# deeplx

Rust封装的DeepL Free API服务

> 使用前提是你需要有一个DeepL Pro帐号

### Features

 - 仅支持DeepL Pro
 - 支持翻译文本
 - 支持帐号池
 - 支持代理池

### 安装

- Ubuntu(Other Linux)

GitHub Releases 中有预编译的二进制文件，以Ubuntu为例：

```bash
wget https://github.com/gngpp/deeplx/releases/download/v0.9.40/deeplx-0.1.0-x86_64-unknown-linux-musl.tar.gz
tar -xf deeplx-0.1.0-x86_64-unknown-linux-musl.tar.gz
mv ./deeplx /bin/deeplx

# 在线更新版本
deeplx update

# 前台运行进程
deeplx run

# 后台运行进程
deeplx start

# 停止后台进程
deeplx stop

# 重启后台进程
deeplx restart

# 查看后台进程状态
deeplx ps

# 查看后台进程日志
deeplx log
```

- Docker

> 镜像源支持`gngpp/deeplx:latest` / `ghcr.io/gngpp/deeplx:latest`

### 使用

1. 启动参数说明

- `-d`, `--debug` 日志开启DEBUG模式
- `-b`, `--bind` 服务监听Socket地址，默认`0.0.0.0:8000`
- `tls-cert` Https证书路径
- `tls-key` Https私钥路径
- `-A`, `--api-key` `deeplx`的翻译接口鉴权密钥
- `--dl-session` 可选的`dl_session`cookie值
- `-x`, `--proxies` 代理，支持协议`http`/`https`/`socks5`/`socks5h`，多个代理使用`,`分隔

2. 启动

第一次启动可以不设置`-dl-session`，那么就需要在浏览器打开: `http://localhost:8000/pool`，登录后，自动加入到帐号池中即可使用。

3. 命令参考
   
```bash
> deeplx -h
DeepL Free API

Usage: deeplx
       deeplx <COMMAND>

Commands:
  run      Run server
  start    Start server daemon
  restart  Restart server daemon
  stop     Stop server daemon
  log      Show the server daemon log
  ps       Show the server daemon process
  help     Print this message or the help of the given subcommand(s)

Options:
  -h, --help     Print help
  -V, --version  Print version


> deeplx run -h
Run server

Usage: deeplx run [OPTIONS]

Options:
  -d, --debug                    Debug mode
  -b, --bind <BIND>              Bind address [default: 0.0.0.0:8000]
      --tls-cert <TLS_CERT>      TLS certificate file
      --tls-key <TLS_KEY>        TLS private key file
  -A, --api-key <API_KEY>        API key
      --dl-session <DL_SESSION>  Deepl `dl_session`
  -x, --proxies <PROXIES>        Deepl client proxy [env: PROXIES=]
  -h, --help                     Print help
```

### 编译

Linux编译，Ubuntu机器为例:

```bash
apt install build-essential
apt install cmake
apt install libclang-dev

git clone https://github.com/gngpp/deeplx.git && cd deeplx
cargo build --release
```