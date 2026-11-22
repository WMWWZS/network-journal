# Labs · 实验

> **看懂 ≠ 会了。** 每个概念都要有一个能跑、能改、能自己验证的实验。

## 约定

每个实验一个目录，编号与 `docs/` 对应，至少包含：

```text
lab-name/
├── README.md      # 目的、原理、预期输出、自测题
├── run.ps1        # 一键运行（或 build.ps1）
└── *.py           # 源码：纯标准库，不依赖第三方包
```

三条硬规则：

1. **必须在本机真实跑通**，README 里贴的是真实输出，不是「预期大概是这样」；
2. **零第三方依赖**（Python 只用标准库），换一台装了 Python 3 的机器就能跑；
3. **不发送真实流量**：练习数据用 RFC 5737 文档专用地址（`192.0.2.0/24` 等）构造。

抓包文件（`.pcap`）体积大且可能含 Cookie/Token 等敏感信息，**默认不提交**，用脚本现场生成。

## 实验列表

| 编号 | 实验 | 对应笔记 | 状态 |
|:---:|---|---|:---:|
| 01 | 手工构造 IPv4/TCP/UDP/DNS 字节 | [01 · 分层与封装](../docs/01-layers-and-encapsulation.md)、[02 · 以太网/ARP/IPv4](../docs/02-ethernet-arp-ip.md) | ✅ 完成 |
| 02 | 解析 DNS 响应（含压缩指针） | [05 · UDP 与 DNS](../docs/05-udp-and-dns.md) | ⬜ 待做 |
| 03 | 观察 TCP 状态迁移 | [03 · TCP 三次握手](../docs/03-tcp-handshake.md) | ⬜ 待做 |
| 04 | 解析 HTTP/1.1 报文并处理 chunked | [06 · HTTP 与 TLS](../docs/06-http-and-tls.md) | ⬜ 待做 |
| 05 | 用 pcap 文件练过滤器 | [08 · 抓包与协议分析](../docs/08-capture-and-analysis.md) | 🟡 练习数据已生成 |
| 06 | 逆向一个自定义长度字段协议 | [09 · 自定义二进制协议](../docs/09-custom-binary-protocol.md) | 🟡 组帧/拆帧示例已就绪 |

## 工具

| 工具 | 状态 | 用途 |
|:---:|---|---|
| Python 3.11（`py`） | ✅ 已安装 | 所有 lab |
| curl 8.22.0 | ✅ 已安装 | 应用层验证、`-w` 计时 |
| Wireshark / tshark | ⬜ 未安装 | lab 05 需要；安装见 [resources.md](../resources.md) |
| MinGW-w64 gcc 14.2 | ✅ 已安装 | 需要时写小工具 |

> 本机 `python` 是 Microsoft Store 占位 stub，运行会失败（`EXIT=9009`）。统一用 `py`。

辅助脚本（不属于 lab，但会被引用）：

- [`tools/make-pcap.py`](../tools/make-pcap.py)：生成 `sample.pcap`（1 个 TCP SYN + 1 个 DNS 查询），装好 Wireshark 后练过滤器；
- [`tools/frame-demo.py`](../tools/frame-demo.py)：长度字段 + TLV 的组帧/拆帧与粘包处理演示。

## 运行环境检查

```powershell
py --version
curl.exe --version
```

两条都能输出，就能跑通 lab 01。Wireshark 相关实验等安装后再做。
