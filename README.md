# visual-first

`visual-first` 是一个面向 AI coding agent 的图优先协作 Skill。

它的目标不是把每个回答都做成网页，而是让复杂的工作结果先被看懂，再提供可核验的文字、文件路径和下一步。Skill 会根据任务复杂度，在简短结论、说明页和专用图之间选择合适的交付方式。

## 它能做什么

- 用行动优先的结构汇报实现结果、验证证据和待办事项
- 将复杂的架构、流程、时序、数据流和状态关系转成易读的可视化说明
- 在需要时协调以下类型的能力
  - `humanizer-zh`：去除空话、重复和模板化表达，同时保留事实与限定条件
  - `answer-me-with-html`：生成一页式 HTML 说明页
  - `archify`：生成架构图、流程图、时序图和状态图
  - `human-writing`：处理需要完整中文叙述的长文
- 区分“已实现”“建议方案”“未验证项”，避免把设计建议说成已完成事实
- 完成实际代码修改、测试或调查后，再组织可读的结果说明
- 对失败、阻塞、权限问题和外部依赖给出明确诊断

## 适用场景

适合在以下任务中使用：

- 解释系统架构、代码结构、请求链路或状态机
- 汇报重构、功能开发、Bug 修复和代码审查结果
- 比较多个技术方案并展示取舍
- 需要少读长文、先看图或快速掌握工作成果
- 需要把多个工具调用、验证结果和后续动作组织成一份清晰交付物

简单问答、单个命令或很小的改动不会强制生成 HTML 页面。

## 安装到 Pi

### 方式一：安装到全局 Skill 目录

```bash
mkdir -p ~/.pi/agent/skills/visual-first
curl -fsSL https://raw.githubusercontent.com/QianHuixun/visual-skill/main/SKILL.md \\
  -o ~/.pi/agent/skills/visual-first/SKILL.md
```

也可以直接克隆仓库：

```bash
mkdir -p ~/.pi/agent/skills
git clone https://github.com/QianHuixun/visual-skill.git \\
  ~/.pi/agent/skills/visual-first
```

如果目录已经存在，使用：

```bash
git -C ~/.pi/agent/skills/visual-first pull
```

安装后重启 Pi，或在交互模式中执行：

```text
/reload
```

### 方式二：安装到当前项目

在项目根目录执行：

```bash
mkdir -p .pi/skills/visual-first
curl -fsSL https://raw.githubusercontent.com/QianHuixun/visual-skill/main/SKILL.md \\
  -o .pi/skills/visual-first/SKILL.md
```

项目级 Skill 只会在该项目受信任后加载。

### 方式三：临时加载

只对当前 Pi 进程加载：

```bash
pi --skill /path/to/visual-first/SKILL.md
```

## 使用方式

Skill 会根据任务自动匹配。也可以在 Pi 中显式加载：

```text
/skill:visual-first
```

或者在请求中直接说明：

```text
启用图优先模式，帮我解释这个系统的请求链路。
```

启用后，如果不再需要 ADHD/行动优先层，可以说：

```text
关闭 ADHD 模式
```

如果要完全停止本 Skill 的持续使用，可以说：

```text
关闭图优先模式
```

## 依赖与配合

本仓库只包含 `SKILL.md`，不捆绑渲染器或其他 Skill。是否能生成 HTML 或专用图，取决于当前 agent 环境是否安装了对应能力：

- 没有可视化依赖时，仍会提供简洁的文字说明和证据
- 不会因为缺少依赖而执行来源不明的安装脚本
- `answer-me-with-html` 和 `archify` 等能力需要分别安装后才能使用其完整交付流程

## 目录结构

```text
visual-skill/
└── SKILL.md
```

## 安全说明

Skill 文件会影响 AI agent 的工作方式，使用前请审阅内容。不要把密钥、Token、私有业务数据或其他敏感信息写入公开仓库。

## License

当前仓库未声明独立许可证。使用、修改或再分发前，请根据仓库维护者的要求确认许可范围。
