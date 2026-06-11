# Tasks

## Task 1: 目录结构重组与文件迁移

重构目录结构，将扁平的 references/ 按领域知识分类，并迁移现有文件。

- [ ] SubTask 1.1: 创建新的目录结构
  - [ ] 创建 references/platform/ 目录
  - [ ] 创建 references/detection/ 目录
  - [ ] 创建 references/positioning/ 目录
  - [ ] 创建 references/examples/ 目录
- [ ] SubTask 1.2: 迁移现有文件
  - [ ] 将 PLATFORM_RULES.md 移动到 references/platform/
  - [ ] 将 SENSITIVE_WORDS.md 移动到 references/detection/
  - [ ] 将 REPLACEMENT_SUGGESTIONS.md 移动到 references/detection/
  - [ ] 将 ACCOUNT_POSITIONING.md 移动到 references/positioning/
  - [ ] 将 CONTENT_EXAMPLES.md 移动到 references/examples/
- [ ] SubTask 1.3: 清理旧目录
  - [ ] 删除 references/ 下的旧文件（确认迁移成功后）

## Task 2: 为所有文件添加 YAML Frontmatter 和版本历史

为每个 Markdown 文件添加统一的版本标头。

- [ ] SubTask 2.1: 为 SKILL.md 添加 Frontmatter
  - [ ] name: xiaohongshu-content-checker
  - [ ] version: 2.1.0
  - [ ] last_updated: 2026-05
  - [ ] type: skill-router
- [ ] SubTask 2.2: 为 README.md 添加 Frontmatter
  - [ ] name: xiaohongshu-content-checker-readme
  - [ ] version: 2.1.0
  - [ ] last_updated: 2026-05
  - [ ] type: documentation
- [ ] SubTask 2.3: 为 references/platform/PLATFORM_RULES.md 添加 Frontmatter
  - [ ] name: PLATFORM_RULES
  - [ ] version: 2.1.0
  - [ ] last_updated: 2026-05
  - [ ] type: reference-knowledge
- [ ] SubTask 2.4: 为 references/detection/SENSITIVE_WORDS.md 添加 Frontmatter
  - [ ] name: SENSITIVE_WORDS
  - [ ] version: 2.1.0
  - [ ] last_updated: 2026-05
  - [ ] type: reference-knowledge
- [ ] SubTask 2.5: 为 references/detection/REPLACEMENT_SUGGESTIONS.md 添加 Frontmatter
  - [ ] name: REPLACEMENT_SUGGESTIONS
  - [ ] version: 2.1.0
  - [ ] last_updated: 2026-05
  - [ ] type: reference-knowledge
- [ ] SubTask 2.6: 为 references/positioning/ACCOUNT_POSITIONING.md 添加 Frontmatter
  - [ ] name: ACCOUNT_POSITIONING
  - [ ] version: 2.1.0
  - [ ] last_updated: 2026-05
  - [ ] type: reference-knowledge
- [ ] SubTask 2.7: 为 references/examples/CONTENT_EXAMPLES.md 添加 Frontmatter
  - [ ] name: CONTENT_EXAMPLES
  - [ ] version: 2.1.0
  - [ ] last_updated: 2026-05
  - [ ] type: reference-knowledge
- [ ] SubTask 2.8: 为所有文件添加版本历史章节

## Task 3: SKILL.md 核心路由层重构

将 SKILL.md 从知识库改造为调度中心。

- [ ] SubTask 3.1: 添加知识库路由映射表
  - [ ] 定义 @读取 标签和对应文件路径
  - [ ] 说明何时加载哪个知识库
- [ ] SubTask 3.2: 定义四大核心工作流
  - [ ] @工作流 1: 账号定位与发布意图确认
  - [ ] @工作流 2: 快速敏感词与违规风险检测
  - [ ] @工作流 3: 自然流与匹配度诊断
  - [ ] @工作流 4: 优化改写与最终发布建议
- [ ] SubTask 3.3: 删除 SKILL.md 中的具体知识内容
  - [ ] 删除敏感词 5 大分类列表
  - [ ] 删除变体类型表
  - [ ] 删除修改原则详细说明
  - [ ] 删除 CES 评分模型详细说明
  - [ ] 保留路由引用和简要说明
- [ ] SubTask 3.4: 泛化业务边界
  - [ ] 将 TRAE 定制选项改为通用行业选项
  - [ ] 保留 9步标准化输出模板结构

## Task 4: 知识库内容整合与去重

确保知识库之间无重叠，每个知识点只存在于一个文件中。

- [ ] SubTask 4.1: 整合 SENSITIVE_WORDS.md
  - [ ] 将 SKILL.md 中的敏感词分类和变体类型表移入
  - [ ] 确保内容与现有敏感词库无重复
- [ ] SubTask 4.2: 整合 REPLACEMENT_SUGGESTIONS.md
  - [ ] 将 SKILL.md 中的修改原则移入
  - [ ] 确保替换建议覆盖所有敏感词类型
- [ ] SubTask 4.3: 整合 PLATFORM_RULES.md
  - [ ] 将 SKILL.md 中的 CES 评分模型移入
  - [ ] 确保平台规则完整
- [ ] SubTask 4.4: 整合 CONTENT_EXAMPLES.md
  - [ ] 将 TRAE 相关示例移入作为垂类案例
  - [ ] 添加更多通用行业示例

## Task 5: README.md 瘦身重构

将 README.md 从 SOP 手册改为项目介绍。

- [ ] SubTask 5.1: 重写简介部分
  - [ ] 一句话说明 Skill 用途
- [ ] SubTask 5.2: 重写核心能力部分
  - [ ] 简述三大核心能力
- [ ] SubTask 5.3: 重写如何使用部分
  - [ ] 提供推荐的对话起手式
- [ ] SubTask 5.4: 添加文件架构说明
  - [ ] 解释 SKILL.md 和 references/ 的分工
- [ ] SubTask 5.5: 删除详细的 SOP 流程说明
  - [ ] 删除 5 步骤详细工作流程
  - [ ] 删除详细的输出示例
  - [ ] 删除重复的平台规则说明

## Task 6: 新增 design.md 架构决策记录

创建 design.md 记录重构思路和未来迭代方向。

- [ ] SubTask 6.1: 记录工作流映射表
  - [ ] 4 个主 Workflow 的类型、做什么、不做什么、上下游
- [ ] SubTask 6.2: 记录核心边界决策
  - [ ] 本系统重在"辅导优化"，而非"替代创作"
  - [ ] 不主动制造焦虑或做绝对判断
  - [ ] 按需加载知识库的设计 rationale
- [ ] SubTask 6.3: 记录目录结构说明
  - [ ] 解释每个目录的职责边界

## Task 7: 验证与测试

验证所有文件的一致性和完整性。

- [ ] SubTask 7.1: 检查目录结构
  - [ ] 确认所有文件在新目录中
  - [ ] 确认旧文件已清理
- [ ] SubTask 7.2: 检查 YAML Frontmatter
  - [ ] 确认所有文件都有完整的 Frontmatter
  - [ ] 确认版本号一致
- [ ] SubTask 7.3: 检查知识库去重
  - [ ] 确认 SKILL.md 无具体知识内容
  - [ ] 确认知识库之间无重叠
- [ ] SubTask 7.4: 检查交叉引用
  - [ ] 确认 SKILL.md 中的 @读取 路径正确
  - [ ] 确认 references/ 中的内部链接正确
- [ ] SubTask 7.5: 检查 9步输出模板
  - [ ] 确认 SKILL.md 中保留 9步结构
  - [ ] 确认输出格式一致

# Task Dependencies

- Task 1 必须在 Task 2 之前完成（先迁移再添加标头）
- Task 1 必须在 Task 3 之前完成（先确定路径再写路由）
- Task 3 和 Task 4 可以并行执行
- Task 5 依赖 Task 3（README 引用新的工作流）
- Task 6 可以独立执行
- Task 7 依赖所有其他 Task 完成
