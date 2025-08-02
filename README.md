# Port-Mapping-Manage

[![Version](https://img.shields.io/badge/version-3.1-blue)](https://github.com/pjy02/Port-Mapping-Manage/blob/main/port_mapping_manager.sh)
[![License](https://img.shields.io/badge/license-MIT-green)](https://github.com/pjy02/Port-Mapping-Manage/blob/main/LICENSE)

> 强大且易用的 iptables 端口映射管理脚本，支持 **TCP / UDP** 协议、批量操作、规则持久化、实时流量监控、备份管理等高级特性。

---

## 📑 项目简介

本脚本旨在简化 Linux 服务器上的大范围端口转发配置与管理，特别适用于 **Hysteria 2 / Xray / iperf** 等需要映射大量端口的应用场景。

* **交互友好**：提供多级菜单，无需记忆复杂命令
* **协议灵活**：支持 TCP / UDP，并可通过数字快速选择
* **批量配置**：支持读取配置文件一次性导入多条规则
* **实时监控**：内置流量统计与速率监控
* **安全可靠**：自动备份规则，支持选择性恢复 / 清理
* **可移植性**：兼容 Debian / Ubuntu / CentOS / Rocky / AlmaLinux 等常见发行版

---

## 🚀 快速开始

> 需 **root** 权限执行，确保系统已安装 `iptables` / `iptables-save` / `iptables-restore`。

```bash
# 一键下载并运行（示例）
bash <(curl -fsSL https://raw.githubusercontent.com/pjy02/Port-Mapping-Manage/refs/heads/main/install_pmm.sh)
```

### 可选启动参数

| 参数 | 说明 |
| ---- | ---- |
| `-v, --verbose` | 显示更多调试信息 |
| `--no-backup` | 禁用自动备份 |
| `-h, --help` | 查看帮助 |
| `--version` | 显示脚本版本 |

---

## 🖥️ 主菜单一览

| 序号 | 功能 |
| ---- | ---- |
| 1 | 新增端口映射 |
| 2 | 查看预设映射范围 |
| 3 | 查看当前映射规则 (Enhanced View) |
| 4 | 规则管理：批量删除 / 端口修改 / 启用禁用 |
| 5 | 系统诊断 |
| 6 | 批量操作：导入 / 导出 / 示例配置 |
| 7 | 备份管理：创建 / 恢复 / 选择性清理 |
| 8 | 实时监控流量 |
| 9 | 恢复默认设置 |
| 10 | 永久保存当前规则 |
| 11 | 帮助信息 |
| 12 | 版本信息 |
| 13 | 退出脚本 |

---

## 🔧 新增映射示例

1. 选择 **1. 新增端口映射**
2. 按提示依次输入：
   * 起始端口：`6000`
   * 终止端口：`7000`
   * 本地服务端口：`3000`
   * 协议：`1`（TCP）或 `2`（UDP）
3. 确认后即刻生效，可在 **3. 查看当前映射规则** 中验证。

---

## 📂 批量导入示例文件

脚本可读取以下格式的配置文件批量导入规则：

```text:sample_rules.conf
# 格式: start_port:end_port:service_port
6000:7000:3000
8000:9000:4000
10000:12000:5000
```

---

## 🛡️ 备份与恢复

* **自动备份**：每次更改 iptables 前自动备份到 `backups/` 目录，默认保留 10 份
* **选择性清理**：在备份管理菜单输入序号（支持空格/逗号等任意分隔）或输入 `all` 一键清空
* **恢复备份**：按序号选择需要恢复的备份文件，支持覆盖当前全部规则

---

## 📊 实时监控

在 **8. 实时监控** 中，可每秒查看累计数据包、字节数与实时速率，方便排查流量瓶颈。

---

## 🆘 故障排查

1. 确认脚本以 **root** 身份执行
2. 检查 `iptables` 是否正常工作：`iptables -L -n`
3. 若规则未生效，尝试重启相关服务并确保本地端口监听
4. 查看日志：`logs/udp_mapping_*.log`

---

## 📜 License

本项目遵循 **MIT License** 发表，可自由使用、修改、分发。详情参见 [LICENSE](./LICENSE)。

---

## 🔄 升级指南

使用最新安装脚本可自动检测并替换到最新版本：

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/pjy02/Port-Mapping-Manage/main/install_pmm.sh)
```

脚本会在保留现有配置的前提下完成升级。

---

## 🗑️ 卸载脚本

```bash
pmm --uninstall
```

或在主菜单输入 `99` 按提示卸载，并选择是否保留备份文件。

---

## 🤝 贡献指南

欢迎提交 PR 或 Issue！

1. Fork 本仓库并创建分支
2. 提交代码前请运行 `shellcheck` 保证脚本质量
3. 详细描述变更内容和测试结果

---

## 📰 更新日志

| 版本 | 变更 | 日期 |
| ---- | ---- | ---- |
| 3.1  | 增加安装脚本依赖自动检测 | 2025-08-02 |
| 3.0  | 全面重构，增加诊断与监控 | 2025-08-02 |
| 2.0  | 初始发布 | 2025-08-01 |

感谢所有贡献者！
