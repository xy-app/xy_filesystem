# 压缩/解压归档文件 (CompressFile)

## 1. 功能概述
对指定文件或文件夹进行高压缩率打包归档或一键解压。支持多种常用归档格式（`.zip`, `.tar.gz`, `.tar`, `.tar.zst`, `.7z`, `.gz`）。

## 2. 核心特性
- **多格式归档支持**：支持 Zip、Tar、Tar.gz、7z 等主流归档格式。
- **灵活压缩控制**：支持 0~9 压缩级别预设（平衡、极速、高压缩率与仅存储）。
- **安全密码加密**：可选设置归档加密密码保护敏感数据。
- **覆盖冲突保护**：支持覆盖已有同名文件的安全开关。

## 3. 参数说明

| 属性名称 | 参数类型 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- |
| `source` | `MixedType` | `""` | 待处理的源文件或源目录完整路径 |
| `destination` | `MixedType` | `""` | 解压输出目录或压缩包目标保存路径 |
| `filename` | `MixedType` | `"archive.zip"` | 归档文件名称（如 `backup.zip`） |
| `format` | `MixedType` | `"zip"` | 压缩格式（Auto / zip / tar / tar.gz / 7z / gz） |
| `level` | `MixedType` | `6` | 压缩级别（0~9，0 为仅存储，9 为最大压缩） |
| `password` | `MixedType` | `""` | 加密保护密码（可选） |
| `overwrite` | `MixedType` | `true` | 若目标位置已存在同名文件是否允许覆盖 |

## 4. 输出
- 返回操作是否成功布尔值（`bool`）。
