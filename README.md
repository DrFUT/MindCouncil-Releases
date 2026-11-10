# 主脑议会 Mind Council — 官方发行仓库

这是 **主脑议会（Mind Council）** 的 Android 安装包与更新元数据仓库。

- 应用源码不在这里，存放在私有仓库。
- 这里只有安装包、校验文件、发行说明和更新清单。
- 每个版本都提供 SHA-256 与签名证书指纹，可以独立核验。

## 下载

| 版本 | 类型 | 安装包 | 大小 | SHA-256 |
|---|---|---|---|---|
| — | 等待首次发布 | — | — | — |

> 也可以直接在 App 内走「档案 → 关于主脑议会 → 软件更新」检查和安装。

## 校验方法

### 1. 文件完整性

```bash
sha256sum -c SHA256SUMS.txt
```

或者手动比对：

```bash
sha256sum MindCouncil-vX.Y.Z.apk
```

### 2. 签名证书

```bash
apksigner verify --print-certs MindCouncil-vX.Y.Z.apk
```

每个版本期望的证书指纹写在同版本 `update-manifest.json` 的 `signingCertificateSha256` 字段。

> SHA-256 只证明文件没被改动，**不等于**发布者身份认证。签名证书指纹才是身份依据。

## 更新机制

App 读取本仓库的 `update-manifest.json` 检查新版本，只接受：

- 本仓库 Release 下的 APK 资产；
- `packageName` 为 `com.mindcouncil.mind_council`；
- `versionCode` 严格大于当前版本；
- SHA-256 与签名证书指纹完全一致；
- 非 Draft、非 Pre-release 的正式稳定版。

任何一项不通过，App 都会拒绝安装——不降级、不跳过校验、不接受其它来源的 APK。

## 版本与资产约定

- Tag：`vX.Y.Z`
- 资产：
  - `MindCouncil-vX.Y.Z.apk`
  - `SHA256SUMS.txt`
  - `update-manifest.json`
  - `release-notes.md`
- `latest` 只指向最新正式稳定版，预发布版本不进入稳定更新通道。

## 隐私

本仓库不包含应用源码、用户数据、API Key 或签名密钥。
