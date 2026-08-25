# Shit Skill 💩

> Explain the path, not just the nodes.

## 🚽 先别急着坐下

一次成功的拉屎，看起来只有一个目标，实际上有一整条不能乱跳的路径：

```text
💩 有需求
   ↓
🧭 找到厕所
   ↓
🚪 找对入口
   ↓
🧻 选择隔间
   ↓
⚙️ 执行
   ↓
✅ 检查结果
```

AI 协作也一样：

```text
发现问题
  -> 定位入口
  -> 找到相关路径
  -> 理解组件关系
  -> 建立因果解释
  -> 执行改动
  -> 验证结果
```

真正让人崩溃的，往往不是 AI 不知道答案，而是它已经读完 20 个文件，
最后只留下一句：

> “我改了 `b()`，问题解决了。”

等等，为什么从 `a()` 跳到 `b()`？为什么应该改这里？证据在哪？会影响什么？

**Shit Skill 不负责让 AI 说得更多。它负责让 AI 别跳步骤。**

---

## 🧠 这是什么？

Shit Skill 是一套面向低上下文人类的 AI 工作协议。

它要求 AI 把目标、上下文、探索路径、组件关系、因果链、原始证据、改动理由和
验证结果组织成一个人类能够理解、复述并继续使用的 mental model。

它不会要求 AI 暴露隐藏的 chain-of-thought，只要求输出可核验、与决策相关的解释。

核心标准是：

> 不要只告诉我你发现了什么。告诉我为什么走到这里，以及这个发现和目标有什么关系。

## 🧱 三层结构

```text
ShitSkill/
├── rules/       # 什么必须始终成立？
├── modules/     # 有哪些可复用的方法？
└── scenarios/   # 当前任务如何组合并执行它们？
```

| Layer | Responsibility |
| --- | --- |
| **Rules** | 原子化行为约束，例如改动前解释原因、结论必须引用原始证据。 |
| **Modules** | 可复用的方法论，例如建立 mental model、追踪路径、验证结论。 |
| **Scenarios** | 面向具体任务的 runner，负责选择 rules、组合 modules、控制流程与停止条件。 |

```text
Rule     -> What must be true?
Module   -> How can we achieve it?
Scenario -> How do we compose it here?
```

Workflow、module 顺序、handoff 和迭代全部属于 scenario。Module 不选择
rules，也不调度其他 modules。

## 🔄 它如何工作？

```text
User request
    ↓
Select scenario
    ↓
Load rules + modules
    ↓
Build the required mental model
    ↓
Follow evidence-backed paths
    ↓
Act only after explaining why
    ↓
Verify and report with source references
```

最终目标不是“AI 遵守了多少条规则”，而是人类看完以后能自己回答：

- 我们在解决什么？
- 为什么要走这条路径？
- 这些组件是怎么连接的？
- 具体运行时调用经过了哪些查找、分发、wrapper 和进程或 namespace 边界？
- 每个关键术语控制什么能力，缺少它会让哪一步发生什么变化？
- 数学概念是否按人的基础解释，是否只引入必要变量，公式怎么来的，前提为什么适用于当前问题？
- 为什么要做这个改动？
- 原始代码或文档证据在哪里？
- 结论依据是实现代码、部署配置、运行观测，还是仅仅是设计文档？
- 做完以后验证了什么？

## 🧰 已实现内容

### Rules

[14 条原子规则](rules/README.md)，覆盖：

- 上下文建立与渐进披露；
- 跳转理由、范围与抽象层级；
- 术语、因果关系和事实边界；
- 原文及代码行引用；
- 改动前解释；
- 成功前验证。

### Modules

- [`better-understanding`](modules/better-understanding/MODULE.md): 建立可被人脑执行和预测的 mental model。
- [`better-explanation`](modules/better-explanation/MODULE.md): 把已理解的内容组织成人能跟随的解释。
- [`top-down`](modules/top-down/MODULE.md): 从相关的高层结构逐步下钻到实现。
- [`path-navigation`](modules/path-navigation/MODULE.md): 解释为什么从一个节点走到下一个节点。
- [`causal-reasoning`](modules/causal-reasoning/MODULE.md): 建立有证据支撑的因果链。
- [`verification`](modules/verification/MODULE.md): 用与风险匹配的证据验证结论和改动。

### Scenarios

- [`bug-fix`](scenarios/bug-fix/SCENARIO.md)
- [`debugging`](scenarios/debugging/SCENARIO.md)
- [`code-review`](scenarios/code-review/SCENARIO.md)
- [`module-development`](scenarios/module-development/SCENARIO.md)
- [`repo-understanding`](scenarios/repo-understanding/SCENARIO.md)
- [`document-understanding`](scenarios/document-understanding/SCENARIO.md)
- [`architecture-understanding`](scenarios/architecture-understanding/SCENARIO.md)

每个 scenario 都是一份 executable specification，而不是固定回复模板。

## 📦 安装

让 TRAE 的 skill 目录指向本仓库：

```bash
ln -s /path/to/ShitSkill .trae/skills/shit-skill
```

入口文件是 [`SKILL.md`](SKILL.md)。

## 📚 设计来源

项目架构来自这次共享讨论：
[设计 Shit Skill](https://chatgpt.com/share/6a8ab070-43c4-83ee-868c-052316b860e5)。

一句话总结：

> 一个看似简单的目标，背后存在一条必须被正确执行的 workflow。
