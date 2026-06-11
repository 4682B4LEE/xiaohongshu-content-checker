# 小红书笔记检测 Skill 架构重构 Spec

## Why

当前 Skill 采用"超长运营指南式"的单体文件结构，存在职责越界、重复维护和版本混乱的问题。需要将 SKILL.md 从"知识库"角色转变为"路由调度中心"，实现结构化、可路由、按需加载、易于版本管理的现代化 AI Skill 架构。

## What Changes

- **BREAKING**: 重构目录结构，将扁平的 references/ 按领域知识分类为 platform/、detection/、positioning/、examples/
- **BREAKING**: 新增 design.md 记录架构决策和工作流映射表
- **BREAKING**: 为所有 Markdown 文件添加 YAML Frontmatter 版本标头
- **BREAKING**: 将 SKILL.md 中的具体知识（敏感词列表、平台规则细则）下沉到 references/
- **BREAKING**: SKILL.md 改造为"调度中心"，使用 @读取 标签控制知识库加载
- **BREAKING**: 定义四大核心工作流（@工作流 1-4）替代原有 5 步骤 SOP
- **BREAKING**: 泛化业务边界，消除 TRAE 定制内容耦合
- **BREAKING**: README.md 瘦身，不再承担 SOP 操作手册功能

## Impact

- Affected specs: 小红书笔记检测 Skill 全部功能
- Affected code: SKILL.md, README.md, references/*.md, 新增 design.md

## ADDED Requirements

### Requirement: 目录结构重组

The system SHALL 建立清晰的知识域边界目录结构：

```
xiaohongshu-content-checker/
├── README.md                      # 面向人类：简介、安装与快速上手
├── SKILL.md                       # 面向大模型：核心路由、工作流定义、输出规范
├── design.md                      # (新增) 面向维护者：架构决策记录
└── references/                    # 面向大模型：按需加载的知识库
    ├── platform/
    │   └── PLATFORM_RULES.md      # 平台规则与算法机制
    ├── detection/
    │   ├── SENSITIVE_WORDS.md     # 敏感词库
    │   └── REPLACEMENT_SUGGESTIONS.md # 替换建议库
    ├── positioning/
    │   └── ACCOUNT_POSITIONING.md # 账号定位指南
    └── examples/
        └── CONTENT_EXAMPLES.md    # 内容优化案例
```

#### Scenario: 目录迁移
- **WHEN** 执行重构时
- **THEN** 原有 references/ 下文件按类型迁移到新目录
- **AND** 旧路径不再使用

### Requirement: 版本元数据规范

The system SHALL 为每个 Markdown 文件添加统一 YAML Frontmatter：

```yaml
---
name: [文件名称]
version: 2.1.0
last_updated: 2026-05
type: [skill-router / reference-knowledge / documentation]
---
```

#### Scenario: 文件头部标头
- **WHEN** 读取任何 Skill 文件时
- **THEN** 文件头部包含完整的 YAML Frontmatter
- **AND** 文末包含版本历史记录

### Requirement: SKILL.md 核心路由层

The system SHALL 将 SKILL.md 改造为大模型"调度中心"：

1. **知识库路由映射表**（Reference Router）：
   - @读取: references/platform/PLATFORM_RULES.md (处理违规、流量机制时)
   - @读取: references/detection/SENSITIVE_WORDS.md (进行文本排雷时)
   - @读取: references/detection/REPLACEMENT_SUGGESTIONS.md (生成修改建议时)
   - @读取: references/positioning/ACCOUNT_POSITIONING.md (分析账号人设时)
   - @读取: references/examples/CONTENT_EXAMPLES.md (需要参考改写风格时)

2. **四大核心工作流**：
   - @工作流 1: 账号定位与发布意图确认
   - @工作流 2: 快速敏感词与违规风险检测
   - @工作流 3: 自然流与匹配度诊断
   - @工作流 4: 优化改写与最终发布建议

#### Scenario: 工作流调度
- **WHEN** 用户请求检测笔记时
- **THEN** SKILL.md 根据当前阶段按需加载对应知识库
- **AND** 不加载无关知识库以节省上下文

### Requirement: 知识库下沉与去重

The system SHALL 消除 SKILL.md 与 References 的重复维护：

- 将 SKILL.md 中的"敏感词 5 大分类"、"变体类型表"剪切到 SENSITIVE_WORDS.md
- 将 SKILL.md 中的"修改原则（降低风险、增强匹配等）"剪切到 REPLACEMENT_SUGGESTIONS.md
- 将 SKILL.md 中的"CES 评分模型"剪切到 PLATFORM_RULES.md

#### Scenario: 内容唯一性
- **WHEN** 检查知识库内容时
- **THEN** 每个知识点只存在于一个文件中
- **AND** SKILL.md 只保留路由引用，不包含具体知识

### Requirement: 业务边界泛化

The system SHALL 消除 TRAE 定制内容耦合：

- 将"数码工具（TRAE开发的游戏/工具）"改写为更通用的行业选项
- 将 TRAE 示例文本转移到 CONTENT_EXAMPLES.md 作为特定垂类案例
- 主流程使用通用化引导

#### Scenario: 通用选项
- **WHEN** 用户选择内容领域时
- **THEN** 选项为通用行业（科技数码、职场效率、生活方式等）
- **AND** 不再默认指向 TRAE 相关内容

## MODIFIED Requirements

### Requirement: README.md 瘦身

README.md SHALL 从 SOP 操作手册重构为项目介绍：

- **简介 (What is this)**：一句话说明基于多工作流的小红书内容风控 Agent
- **核心能力 (Features)**：简述人设匹配、敏感词排雷、自然流优化三大能力
- **如何使用 (How to use)**：提供推荐的对话起手式（Prompt 模板）
- **文件架构说明 (Structure)**：简要解释 SKILL.md 和 references/ 的分工

### Requirement: 保留标准化输出

保留原有的 9步标准化输出模板结构，作为强制校验规则：
1. 总体结论
2. 内容定位卡
3. 核心问题摘要
4. 敏感词与高风险表达检测
5. 账号定位与人群匹配度
6. 自然流影响因素判断
7. 修改建议
8. 优化后版本
9. 发布前检查清单

## REMOVED Requirements

### Requirement: 单体文件知识存储
**Reason**: 职责越界，SKILL.md 不应同时承担路由和知识库角色
**Migration**: 知识迁移到 references/ 下对应分类文件

### Requirement: TRAE 定制化主流程
**Reason**: 业务边界过窄，限制 Skill 通用性
**Migration**: TRAE 内容作为 examples/ 下的垂类案例保留
