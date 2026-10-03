# 📁 官方文件系统与归档压缩套件 (File System & Archive Suite)

[![Plugin Version](https://img.shields.io/badge/version-0.50.5-blue.svg)](manifest.json)
[![Group](https://img.shields.io/badge/group-Filesystem-yellow.svg)](#)
[![Platform](https://img.shields.io/badge/platform-All-green.svg)](#)
[![License](https://img.shields.io/badge/license-Freeware-brightgreen.svg)](#)

专为工业级自动化流程与 RPA 设计的文件系统读写、目录迭代、数据归档及图像存取套件。支持文本安全读写、大文件按行流式解析、文件夹递归/单层遍历、Zip/Tar/7z 压缩与解压、系统标准环境路径解析及专用内存图像对象存取。

---

## 📖 简介 (Overview)

`xy_filesystem` 提供了跨平台的底层文件系统操作能力：
- **流式与批量 IO 处理**：支持完整文件二进制/文本读取（`FileRead`）、追加与覆盖写入（`FileWrite`），以及对大体积文本按行高效解析（`ReadLines`）。
- **文件管理与元数据探测**：提供文件与目录的跨路径拷贝（`CopyFile`）、存在性与尺寸判断（`FileQuery`），以及跨平台的操作系统标准路径检索（`StandardPath`，如 Desktop、AppData、Temp 等）。
- **目录遍历引擎**：支持同步与异步后台迭代、深层递归遍历及多后缀通配符过滤（`DirectoryIterator`）。
- **工业级压缩归档**：集成 Zip、Tar、Tar.gz 多种主流压缩算法，支持 0~9 压缩级别设定与密码加密保护（`CompressFile`）。
- **视觉自动化生态集成**：专门为截图与机器视觉流水线提供内存图像对象的高速加载（`ImageLoad`）与本地持久化（`ImageSave`）。

---

## ✨ 核心特性 (Features)

- **高性能 IO 读写**：支持整文件读取与大文件按行流式解析为字符串列表，兼顾轻量操作与超大日志处理。
- **多格式归档压缩**：原生支持 `zip`、`tar`、`tar.gz` 格式的解压缩与打包，提供覆盖策略、压缩等级（0-9）及密码防护。
- **灵活目录遍历检索**：支持递归与非递归目录扫描，内置 `*`、`txt`、`png,jpg` 等多扩展名过滤规则，支持非阻塞异步模式。
- **跨平台环境抽象**：一键解析 Windows / macOS / Linux 下的 `Desktop`、`Documents`、`Downloads`、`AppData` 及 `Temp` 系统标准目录。
- **图像管线对接**：直接对接上游 CV/OCR 节点的 `Image` 内存对象，避免临时磁盘转存损耗。

---

## 🛠️ 动作指令全景速查 (Action Catalog)

| 动作标识 (Tag) | 功能名称 | 描述 | 输出类型 |
| :--- | :--- | :--- | :--- |
| `CompressFile` | 压缩/解压归档文件 | 执行 Zip/Tar/Tar.gz 格式的文件解压或打包归档，支持密码与等级 | `bool` |
| `CopyFile` | 复制文件/目录 | 跨目录拷贝单个文件或完整目录树，支持重命名 | `bool` |
| `DirectoryIterator` | 遍历目录文件 | 递归或单层遍历指定文件夹中的子文件与子目录，支持后缀过滤与异步 | `Array` |
| `FileQuery` | 查询文件属性/匹配 | 检测文件是否存在、查询大小、判断是否为目录或通配符匹配 | `string` |
| `FileRead` | 读取完整文件 | 读取文件全部内容为文本字符串或原始二进制字节流 | `string` |
| `FileWrite` | 写入文件内容 | 向指定路径覆盖或追加写入文本字符串或二进制内容 | `bool` |
| `ImageLoad` | 加载图像数据 | 从本地磁盘快速加载位图/PNG/JPEG 为内存 Image 对象 | `Image` |
| `ImageSave` | 保存图像文件 | 将当前内存中的 Image 对象编码并持久化保存至本地磁盘 | `bool` |
| `ReadLines` | 按行读取文本 | 将大型文本文件逐行解析为字符串数组列表，支持异步模式 | `Array` |
| `StandardPath` | 获取系统标准路径 | 获取系统桌面、用户文档、应用配置或临时文件夹的标准绝对路径 | `string` |

---

## 📚 详细参数说明与参考 (Detailed Reference)

### 1. `CompressFile` - 压缩/解压归档文件
支持文件/文件夹的打包归档与压缩包解压。

- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `source` | 源文件/源目录 | `string` | `""` | - | 待打包的文件/目录，或待解压的归档文件路径 |
  | `destination` | 目标路径 | `string` | `""` | - | 解压输出目录或打包输出的目标归档路径 |
  | `filename` | 归档文件名称 | `string` | `archive.zip` | `archive.zip`, `archive.tar.gz` | 生成压缩包的文件名 |
  | `format` | 归档格式 | `string` | `zip` | `zip`, `tar`, `tar.gz` | 压缩算法格式 |
  | `level` | 压缩等级 | `number` | `6` | `0`, `1`, `6`, `9` | 压缩级别（0 为存储，9 为最大压缩） |
  | `password` | 加密密码 | `string` | `""` | - | 压缩加密或解压保护密码（可选） |
  | `overwrite` | 覆盖已存在文件 | `bool` | `true` | `true`, `false` | 若目标已存在是否允许覆盖 |
- **输出类型：** `bool`（操作是否成功）

---

### 2. `CopyFile` - 复制文件/目录
跨路径复制单个文件或递归复制整个文件夹树。

- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- |
  | `from` | 源文件路径 | `string` | `""` | 要复制的源文件或源目录路径 |
  | `to` | 目标目录/文件 | `string` | `""` | 复制目标目的路径 |
  | `filename` | 重命名新文件名 | `string` | `""` | 目标文件名；若留空则自动保持原文件名 |
- **输出类型：** `bool`

---

### 3. `DirectoryIterator` - 遍历目录文件
列举指定目录下的所有文件项，输出文件路径数组列表。

- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `path` | 文件夹路径 | `string` | `""` | - | 目标被扫描的根目录路径 |
  | `recursive` | 递归查找子目录 | `bool` | `false` | `true`, `false` | 是否深度向下遍历多级子文件夹 |
  | `extensions` | 扩展名过滤 | `string` | `*` | `*`, `txt`, `png,jpg`, `csv` | 过滤指定后缀，多后缀用逗号隔开 |
  | `async` | 异步遍历模式 | `bool` | `false` | `true`, `false` | 是否在后台异步非阻塞执行遍历 |
- **输出类型：** `Array`（文件路径数组）

---

### 4. `FileQuery` - 查询文件属性/匹配
快速检查文件系统元数据与存在性。

- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `pattern` | 文件路径或匹配规则 | `string` | `""` | - | 目标路径或通配符规则 |
  | `option` | 查询类型 | `string` | `exists` | `exists`, `size`, `is_dir`, `is_file` | 查询模式：是否存在、文件大小、是否为目录/文件 |
- **输出类型：** `string`（根据选项返回布尔字符串、字节大小或匹配状态）

---

### 5. `FileRead` 与 `FileWrite` - 基础文件读写

#### `FileRead` - 读取完整文件
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- |
  | `file` | 文件路径 | `string` | `""` | 待读取的磁盘目标文件路径 |
- **输出类型：** `string`（文本内容或二进制数据表达）

#### `FileWrite` - 写入文件内容
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `folder` | 存储目录 | `string` | `""` | - | 输出存储的父文件夹路径 |
  | `filename` | 文件名称 | `string` | `output.txt` | `output.txt`, `log.txt` | 写入目标文件的文件名 |
  | `source` | 写入数据内容 | `string` | `""` | - | 待持久化写入的文本或数据内容 |
- **输出类型：** `bool`

---

### 6. `ReadLines` - 按行读取文本
专为日志解析、大文本流式处理设计。

- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设选项 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `file` | 文本文件路径 | `string` | `""` | - | 目标文本文件路径 |
  | `async` | 异步读取模式 | `bool` | `false` | `true`, `false` | 是否启用后台线程异步非阻塞分片读取 |
- **输出类型：** `Array`（按行分割的文本列表）

---

### 7. `ImageLoad` 与 `ImageSave` - 图像对象存取
专门服务于视觉处理、截屏持久化与 OCR 图像流水线。

#### `ImageLoad` - 加载图像数据
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- |
  | `file` | 图片文件路径 | `string` | `""` | 目标图像文件路径（支持 JPG、PNG、BMP 等） |
- **输出类型：** `Image`（内存图像对象句柄）

#### `ImageSave` - 保存图像文件
- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设推荐值 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `folder` | 存储目录 | `string` | `""` | - | 保存图像的目标目录 |
  | `filename` | 文件名称 | `string` | `screenshot.png` | `screenshot.png`, `capture.jpg` | 输出图像的文件名 |
  | `image` | 图像对象引用 | `string` | `""` | - | 上游动作节点传递的 Image 对象 |
- **输出类型：** `bool`

---

### 8. `StandardPath` - 获取系统标准路径
解决自动化脚本在不同操作系统环境下的路径适配难题。

- **输入参数：**
  | 参数名 (Field) | 显示名称 | 类型 | 默认值 | 预设选项 | 说明 |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | `value` | 标准目录类型 | `string` | `Desktop` | `Desktop`, `Documents`, `Downloads`, `AppData`, `Temp` | 目标标准环境目录类型 |
- **输出类型：** `string`（当前系统的绝对物理目录路径）

---

## 📦 插件清单定义 (Manifest Reference)

```json
{
  "plugin_id": "xy_filesystem",
  "name": "官方文件系统与归档压缩套件 (File System & Archive Suite)",
  "version": "0.50.5",
  "group": "Filesystem",
  "group_icon": "📁",
  "description": "提供安全文件读写、按行解析读取、文件与目录遍历迭代、压缩包打包与解压 (Zip/Tar/7z)、专用图像存取与系统标准路径获取能力",
  "actions": [...]
}
```

---

## 📄 许可证 (License)

本插件遵循免费专有许可协议 (Freeware)。供 xy-app 用户免费下载与使用，未经官方书面授权，严禁对二进制文件进行逆向工程、反编译或二次打包转售。
