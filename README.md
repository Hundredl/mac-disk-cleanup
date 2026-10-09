# Mac 磁盘排查与清理助手

简体中文 | [English](README.en.md)

一个用于 Codex 等本机 AI 助手的 skill：盘点磁盘与应用残留，让用户审核，再按批准范围清理，保存可追溯的维护记录。

适合“电脑有点慢，磁盘是不是太满了”“有哪些旧应用和文件可以清”“清理后某个功能异常，查查改了哪里”。可只排查，也可接着执行已经批准的项目。

## 直接复制这段 Prompt

不安装 skill 时，也可以把下面这段发给能访问你电脑的 AI 助手：

```text
请帮我排查这台 Mac 的磁盘占用和旧应用残留。先只读检查，列出候选的具体路径、大小、用途、恢复条件和推荐处理方式，让我审核。记录我明确保留的内容；仅清理我批准的具体项目，已有授权不重复询问。不要为了凑空间扩大范围，区分缓存、账号/聊天数据库、文档、存档和运行依赖，备份按我的要求做。执行前复核路径与占用，先保存记录再操作，失败也留痕；完成后核验并测量真实可用空间变化。把删除、保留、错误、备份当前状态及可能影响哪些功能，整理到我指定的“系统维护”位置，方便以后参考和归因。没有本机工具或权限时，请说明限制。
```

普通聊天网页中的模型未必能访问本机，复制 Prompt 不会自动获得终端、文件或管理员权限。

## 安装为 Codex skill

在本机终端运行（需要 Git；目标目录应尚不存在）：

```sh
git clone https://github.com/Hundredl/mac-disk-cleanup.git "${CODEX_HOME:-$HOME/.codex}/skills/mac-disk-cleanup"
```

在新的 Codex 会话中调用：

```text
使用 $mac-disk-cleanup，先看看磁盘和旧应用占用，不要删除，列候选让我审核。
```

你也可以直接让助手读取仓库里的 [SKILL.md](SKILL.md)。其他支持 SKILL.md 的助手可按各自安装方式使用。

英文使用者可看 [English README](README.en.md) 和 [English skill guide](SKILL.en.md)。`SKILL.md` 保持统一入口，会按用户语言选择指南，无需安装两份 skill。

## 文件

- [SKILL.md](SKILL.md)：主流程与范围规则。
- [SKILL.en.md](SKILL.en.md)：完整英文指南。
- [盘点注意事项](references/inspection.md)：空间口径、候选证据和权限边界。
- [执行与记录](references/execution-record.md)：逐项日志、核验、备份状态与故障归因。
- `agents/openai.yaml`：Codex 的名称、简介和示例调用。

本仓库提供通用方法，不包含个人清理报告、自动删除脚本或一键清理命令。释放空间与改善卡顿需要分别验证；某些内容删除后需要重新下载、构建或重装，恢复能力取决于实际备份与原始来源。

License: [MIT](LICENSE).
