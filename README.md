# skill-dev-driver - 开发驾驶元技能

**版本**: 1.0.0  
**作者**: YYCLink  
**协议**: MIT License

## 概述

skill-dev-driver 是一个**元技能（Meta-Skill）**，专注于：
- 🎯 **理解项目目标** - 知道用户要做什么
- 📜 **记录项目历史** - 记住已完成和待办事项
- 💡 **积累解决方案** - 从问题中学习并复用
- 🔗 **调度领域技能** - 调用其他技能协同工作

## 核心特性

| 特性 | 说明 | Token 效率 |
|------|------|-----------|
| 轻量索引 | skill-index.json (~500 token) | ⭐⭐⭐⭐⭐ |
| 项目上下文 | current-state.md (~200 token) | ⭐⭐⭐⭐⭐ |
| 按需加载 | 仅加载匹配的技能 (~2000 token) | ⭐⭐⭐⭐⭐ |
| 技能调度 | 可调用其他 YYCLink 技能 | ⭐⭐⭐⭐ |

## 触发词

当用户输入包含以下关键词时，skill-dev-driver 会自动激活：

| 场景 | 触发词示例 | 调用的子技能 |
|------|-----------|-------------|
| 继续工作 | "继续"、"下一步"、"接着做"、"历史"、"进度"、"之前"、"昨天"、"上次" | project-memory |
| 规划架构 | "架构"、"设计"、"规划"、"路线"、"怎么做"、"如何开始" | core-driving |
| 解决问题 | "bug"、"错误"、"问题"、"解决"、"失败"、"报错"、"异常" | solution-library |
| 调用技能 | "用 XX 技能"、"调用 XX" | skill-router |

## 快速开始

### 方式一：通过 YYCLink-Skills 一键下载

```bash
# 在 YYCLink-Skills 目录双击 run.bat
# 或手动克隆
git clone https://github.com/wanddream/skill-dev-driver.git
```

### 方式二：直接在项目中使用

```bash
# 在你的项目目录
mkdir skills
cd skills
git clone https://github.com/wanddream/skill-dev-driver.git
```

### 方式三：在编译器中导入

**CodeBuddy/Qoder**：
1. 设置 → 技能 → 导入 Skill
2. 选择 `skill-dev-driver/SKILL.md`
3. 完成！

**Cline/Cursor**：
1. 项目里放 `skills/skill-dev-driver/`
2. 使用时说："使用 skill-dev-driver 技能"

## 目录结构

```
skill-dev-driver/
├── SKILL.md                    # 核心技能文件（入口）
├── README.md                   # 使用说明
├── skill-index.json            # 技能索引配置（Token 优化）
├── skills/                     # 子技能目录
│   ├── core-driving/           # 核心驾驶 - 理解项目目标，规划开发路线
│   │   └── SKILL.md
│   ├── project-memory/         # 项目记忆 - 记录项目历史进度，支持上下文感知
│   │   └── SKILL.md
│   └── solution-library/       # 解决方案库 - 积累问题 - 解决方案对照表
│       └── SKILL.md
└── templates/                  # 上下文模板
    ├── project-goal.template.md    # 项目目标模板
    ├── current-state.template.md   # 当前状态模板
    └── solutions.template.md       # 解决方案库模板
```

## 使用示例

### 示例 1：继续之前的工作

```
用户：继续做昨天的功能

skill-dev-driver:
📖 读取项目上下文...
当前任务：实现语音识别模块
上次进度：完成了 HTTP API 通信部分
待办：添加 VAD 语音活动检测

正在加载 project-memory 技能...

好的，我们继续实现语音识别模块。上次完成了 HTTP API 通信，
今天我们来添加 VAD 语音活动检测功能...
```

### 示例 2：调用其他技能

```
用户：用小程序技能做登录功能

skill-dev-driver:
🔗 检测到需要小程序开发技能...
正在加载 skill-miniprogram-ecosystem...

已加载小程序生态开发技能。
为了设计登录功能，请告诉我：
1. 目标平台？（微信/抖音/支付宝）
2. 登录方式？（微信登录/手机号/自定义）
```

### 示例 3：记录解决方案

```
用户：这个 bug 终于解决了！是 numpy 版本冲突

skill-dev-driver:
💡 检测到新问题解决方案！
正在记录到 solution-library...

已记录：
问题：numpy 版本冲突导致语音识别失败
解决：锁定 numpy==1.24.3

下次遇到类似问题会自动推荐这个方案。
```

## 项目上下文管理

### 初始化（首次使用）

在项目根目录创建 `.yyclink/context/` 目录：

```bash
mkdir -p .yyclink/context
```

创建项目目标文件：

```bash
.yyclink/
└── context/
    ├── project-goal.md      # 项目目标（用户填写）
    └── current-state.md     # 当前状态（AI 更新）
```

### 项目目标模板

```markdown
# 项目目标

## 项目名称
[填写项目名称]

## 项目描述
[用一句话描述项目是做什么的]

## 核心功能
1. [功能 1]
2. [功能 2]
3. [功能 3]

## 技术栈
- 前端：
- 后端：
- 数据库：

## 目标用户
[描述目标用户群体]
```

### 当前状态模板

```markdown
# 当前状态

## 当前任务
[当前正在进行的任务]

## 完成进度
- [x] 已完成的功能
- [ ] 待办事项

## 最近修改
- [日期] 修改内容

## 遇到的问题
- 问题描述 → 解决方案
```

### 如何让 AI 自动更新

完成任务后，告诉 AI：
```
更新 current-state.md，记录今天完成了 XXX
```

或者：
```
记录到项目历史：实现了 XX 功能，遇到了 XX 问题已解决
```

## 与其他技能的配合

skill-dev-driver 可以与其他 YYCLink 技能配合使用：

| 场景 | 配合的技能 | 调用方式 |
|------|-----------|---------|
| 小程序开发 | skill-miniprogram-ecosystem | 自动调度 |
| 论文写作 | skill-thesis-writer | 自动调度 |
| 产品评审 | skill-product-manager | 自动调度 |
| Web 开发 | skill-web-dev | 自动调度 |

### 技能调度机制

当用户说"用 XX 技能"或检测到相关领域关键词时，skill-dev-driver 会：
1. 自动识别需要的技能
2. 读取目标技能的 SKILL.md
3. 按照目标技能的指令执行
4. 完成任务后返回 skill-dev-driver 继续上下文管理

## 常见问题

### Q: skill-dev-driver 和其他技能有什么区别？

**A**: skill-dev-driver 是**元技能（Meta-Skill）**，它本身不专注于某个具体领域，而是：
- 管理项目上下文（目标、历史、解决方案）
- 调度其他领域技能（小程序、论文、产品等）
- 让你在任何项目中都能"继续之前的工作"

### Q: 必须使用 .yyclink/context/目录吗？

**A**: 这是推荐的目录结构，但你可以自定义。关键是：
- skill-dev-driver 需要知道项目目标和当前状态
- 目录位置可以在 SKILL.md 中配置

### Q: 如何在多个项目中使用？

**A**: skill-dev-driver 是**项目级**的技能：
- 每个项目有自己的 `.yyclink/context/` 目录
- 在每个项目中单独初始化即可
- 项目之间的上下文互不干扰

### Q: 如何备份项目上下文？

**A**: 建议将 `.yyclink/context/` 纳入你的项目版本控制：
```bash
git add .yyclink/context/
git commit -m "记录项目状态"
```

### Q: Token 用量会不会很高？

**A**: skill-dev-driver 采用轻量索引设计：
- 基础用量：~700 token（索引 + 当前状态）
- 按需加载：~2000 token/子技能
- 单次对话总计：~2700-4700 token

## 更新日志

### v1.0.0 (2026-03-01)
- 初始版本
- 核心驾驶、项目记忆、解决方案库三个子技能
- 支持技能调度机制
- 支持项目上下文管理
- Token 优化设计

---

## 贡献

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

---

**作者**: YYCLink  
**GitHub**: https://github.com/wanddream/skill-dev-driver  
**YYCLink-Skills**: https://github.com/wanddream/YYCLink-Skills  
**协议**: MIT License
