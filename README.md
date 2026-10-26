# 📁 官方文件系统与归档压缩套件 (File System & Archive Suite)

[![Plugin Version](https://img.shields.io/badge/version-0.53.0-blue.svg)](manifest.json)
[![Group](https://img.shields.io/badge/group-Filesystem-yellow.svg)](#)
[![Platform](https://img.shields.io/badge/platform-All-green.svg)](#)
[![License](https://img.shields.io/badge/license-Freeware-brightgreen.svg)](#)

专为工业级自动化流程与 RPA 设计的文件系统读写、目录迭代、安全回收站删除、移动与重命名、文件占用检测、临时文件创建、文件夹事件监视、数据归档及图像存取套件。

---

## 📖 简介 (Overview)

`xy_filesystem` 提供了跨平台的底层文件系统操作能力：
- **流式与批量 IO 处理**：支持完整文件二进制/文本读取（`FileRead`）、覆盖与追加写入（`FileWrite`），以及对大体积文本按行高效解析（`ReadLines`）。
- **完整文件管理与安全机制**：支持跨目录文件/目录拷贝（`CopyFile`）、移动与重命名（`MoveFile`）、新建多级目录（`CreateFolder`）、安全回收站删除与强制粉碎（`DeleteFile`）、属性探测（`FileQuery`）及系统标准路径解析（`StandardPath`）。
- **高级 RPA 自动化集成**：支持进程独占文件占用检测与超时解锁等待（`FileLock`）、高安全临时文件与目录生成（`TempFile`）、实时文件夹文件变动事件监视（`WatchFolder`）。
- **目录遍历引擎**：支持同步与异步后台迭代、深层递归遍历及多后缀通配符过滤（`DirectoryIterator`）。
- **工业级压缩归档**：集成 Zip、7z、Tar、Tar.gz、Tar.zst 多种主流压缩算法，支持 0~9 压缩级别与密码保护（`CompressFile`）。
- **视觉自动化生态集成**：专门为截图与机器视觉流水线提供内存图像对象的高速加载（`ImageLoad`）与本地持久化/无缝导出 PDF（`ImageSave`）。

---

## 🛠️ 动作指令全景速查 (Action Catalog)

| 动作标识 (Tag) | 功能名称 | 描述 | 输出类型 |
| :--- | :--- | :--- | :--- |
| `CompressFile` | 压缩/解压归档文件 | 执行 Zip/7z/Tar 格式的文件解压或打包归档，支持密码与等级 | `bool` |
| `CopyFile` | 复制文件/目录 | 跨目录拷贝单个文件或完整目录树，支持重命名 | `bool` |
| `CreateFolder` | 创建文件夹 | 递归新建指定的文件夹路径，支持已存在时自动清空内部文件选项 | `string` |
| `DeleteFile` | 删除文件/目录 | 安全删除指定文件或文件夹，默认移入系统回收站（支持强力彻底粉碎） | `bool` |
| `DirectoryIterator` | 遍历目录文件 | 递归或单层遍历指定文件夹中的子文件与子目录，支持后缀过滤与异步 | `Array` |
| `FileLock` | 文件占用检测 | 检测文件是否正被 Excel、Word 或其他外部进程独占锁定，支持超时等待解锁 | `bool` |
| `FileQuery` | 查询文件属性/匹配 | 检测文件是否存在、查询大小、判断是否为目录或最后修改时间 | `string` |
| `FileRead` | 读取完整文件 | 读取文件全部内容为文本字符串或原始二进制字节流 | `string` |
| `FileWrite` | 写入文件内容 | 向指定路径覆盖或追加写入文本字符串或二进制内容 | `bool` |
| `ImageLoad` | 加载图像数据 | 从本地磁盘快速加载位图/PNG/JPEG 为内存 Image 对象 | `Image` |
| `ImageSave` | 保存图像文件 | 将当前内存中的 Image 对象编码并持久化保存至本地磁盘或 PDF | `bool` |
| `MoveFile` | 移动/重命名文件 | 将文件或文件夹移动到新目录或重命名，支持跨盘/跨卷移动 | `bool` |
| `ReadLines` | 按行读取文本 | 将大型文本文件逐行解析为字符串数组列表，支持异步模式 | `Array` |
| `StandardPath` | 获取系统标准路径 | 获取系统桌面、用户文档、应用配置或临时文件夹的标准绝对路径 | `string` |
| `TempFile` | 创建临时文件/目录 | 在系统临时目录下自动生成具备唯一名的临时文件或文件夹 | `string` |
| `WatchFolder` | 监视文件夹变动 | 实时监视文件夹中的文件新建、修改、删除等事件，支持超时阻断等待 | `string` |

---

## 📄 许可证 (License)

本插件遵循免费专有许可协议 (Freeware)。供 xy-app 用户免费下载与使用。
