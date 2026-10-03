# 获取系统标准路径 (StandardPath)

## 1. 功能概述
快速获取当前操作系统约定俗成的标准物理绝对路径，解决跨平台自动化脚本中的路径适配问题。

## 2. 核心特性
- **跨平台路径抽象**：统一支持 Windows / macOS / Linux 系统环境下的用户标准目录检索。
- **常用已知目录**：覆盖 Desktop（桌面）、Documents（文档）、Downloads（下载）、AppData（应用配置）、Temp（临时目录）等。

## 3. 参数说明

| 属性名称 | 参数类型 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- |
| `value` | `MixedType` | `"Desktop"` | 标准目录类型（如 `Desktop`, `Documents`, `Downloads`, `AppData`, `Temp` 等） |

## 4. 输出
- 返回对应系统标准目录的物理绝对路径字符串（`string`）。
