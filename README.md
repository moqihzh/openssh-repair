 OpenSSH 漏洞修复包

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

本仓库提供预编译的 OpenSSH 漏洞修复包，用于快速修复 OpenSSH 相关安全漏洞。

## 📦 支持的操作系统

### RPM 包（适用于 RHEL/CentOS/AlmaLinux/Rocky Linux/Kylin Linux Advanced Server V10）

### DEB 包（适用于 Debian/Ubuntu）

> 开发中，敬请期待

## 🚀 快速开始

### RPM 包安装

#### 方法一：直接安装（推荐）

```bash
# 1. 下载 RPM 包
git clone https://github.com/moqihzh/openssh-repair.git

# 2. 安装
cd openssh-repair/rpm/V_10_2_P1
sudo rpm -Uvh openssh-*.rpm

# 3. 重启 SSH 服务
sudo systemctl restart sshd

# 4. 验证版本
ssh -V
```

#### 方法二：使用 yum/dnf 安装

```bash
# 1. 下载所有 RPM 包到当前目录
git clone https://github.com/moqihzh/openssh-repair.git
cd openssh-repair/rpm/V_10_2_P1

# 2. 使用 yum 本地安装
sudo yum localinstall openssh-*.rpm -y

# 3. 重启服务并验证
sudo systemctl restart sshd
ssh -V
```

### ⚠️ 安装注意事项

1. **保持现有连接**：升级前请保持至少一个 SSH 会话连接，以防配置问题导致无法登录
2. **备份配置**：
   ```bash
   sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
   ```
3. **测试配置**：升级后先测试配置是否正确
   ```bash
   sudo sshd -t
   ```
4. **防火墙规则**：确保防火墙允许 SSH 端口（默认 22）
5. **旧版本升级权限问题**：如果从 OpenSSH 8.0 以下版本升级，SSH 相关文件和目录可能会发生权限变化，导致服务无法启动。需要手动修复权限：
   ```bash
   # 修复密钥文件权限
   chmod 600 /etc/ssh/ssh_host_ed25519_key
   chmod 600 /etc/ssh/ssh_host_ecdsa_key
   chmod 600 /etc/ssh/ssh_host_rsa_key
   
   # 修复 SSH 目录权限
   chmod 755 /etc/ssh
   
   # 重启并检查服务状态
   systemctl restart sshd
   systemctl status sshd
   ```


## 🛠️ 自行编译

如果你需要自行编译 OpenSSH 包，可以参考以下项目：

### 编译 RPM 包

参考项目：[boypt/openssh-rpms](https://github.com/boypt/openssh-rpms)

```bash
git clone https://github.com/boypt/openssh-rpms.git
cd openssh-rpms
# 按照项目说明进行编译
```

### 编译 DEB 包

参考项目：[boypt/openssh-deb](https://github.com/boypt/openssh-deb)

```bash
git clone https://github.com/boypt/openssh-deb.git
cd openssh-deb
# 按照项目说明进行编译
```

## 📋 卸载与回滚

如果需要回滚到系统原版本：

```bash
# 1. 卸载当前版本
sudo rpm -e openssh-server openssh-clients openssh

# 2. 重新安装系统版本
sudo yum reinstall openssh openssh-server openssh-clients -y

# 3. 恢复配置（如果需要）
sudo cp /etc/ssh/sshd_config.bak /etc/ssh/sshd_config

# 4. 重启服务
sudo systemctl restart sshd
```

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

本项目采用 [MIT 许可证](LICENSE)。

## ⚠️ 免责声明

使用本软件时，请：

- 在生产环境使用前，请先在测试环境验证
- 做好数据备份和配置备份
- 了解相关安全风险

## 📞 联系方式

- 提交问题：[GitHub Issues](https://github.com/moqihzh/openssh-repair/issues)
- 项目主页：[openssh-repair](https://github.com/moqihzh/openssh-repair)

---

**注意**：升级 OpenSSH 是一项重要的系统操作，请务必谨慎操作并做好备份。