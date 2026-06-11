# 重构执行检查清单

## 阶段一：目录结构与文件迁移

- [ ] 新目录结构已创建（platform/、detection/、positioning/、examples/）
- [ ] PLATFORM_RULES.md 已移动到 references/platform/
- [ ] SENSITIVE_WORDS.md 已移动到 references/detection/
- [ ] REPLACEMENT_SUGGESTIONS.md 已移动到 references/detection/
- [ ] ACCOUNT_POSITIONING.md 已移动到 references/positioning/
- [ ] CONTENT_EXAMPLES.md 已移动到 references/examples/
- [ ] 旧 references/ 下的文件已清理

## 阶段二：YAML Frontmatter 与版本历史

- [ ] SKILL.md 包含完整的 YAML Frontmatter（name/version/last_updated/type）
- [ ] README.md 包含完整的 YAML Frontmatter
- [ ] PLATFORM_RULES.md 包含完整的 YAML Frontmatter
- [ ] SENSITIVE_WORDS.md 包含完整的 YAML Frontmatter
- [ ] REPLACEMENT_SUGGESTIONS.md 包含完整的 YAML Frontmatter
- [ ] ACCOUNT_POSITIONING.md 包含完整的 YAML Frontmatter
- [ ] CONTENT_EXAMPLES.md 包含完整的 YAML Frontmatter
- [ ] 所有文件的版本号一致（2.1.0）
- [ ] 所有文件包含版本历史章节

## 阶段三：SKILL.md 路由层重构

- [ ] SKILL.md 顶部包含知识库路由映射表（@读取 标签）
- [ ] 定义了四大核心工作流（@工作流 1-4）
- [ ] SKILL.md 中已删除敏感词 5 大分类列表
- [ ] SKILL.md 中已删除变体类型表
- [ ] SKILL.md 中已删除修改原则详细说明
- [ ] SKILL.md 中已删除 CES 评分模型详细说明
- [ ] 业务选项已泛化（TRAE 定制内容改为通用行业）
- [ ] 保留 9步标准化输出模板结构

## 阶段四：知识库去重与整合

- [ ] SENSITIVE_WORDS.md 包含完整的敏感词分类和变体类型
- [ ] REPLACEMENT_SUGGESTIONS.md 包含修改原则
- [ ] PLATFORM_RULES.md 包含 CES 评分模型
- [ ] CONTENT_EXAMPLES.md 包含 TRAE 垂类案例和通用案例
- [ ] 知识库之间无内容重叠
- [ ] 每个知识点只存在于一个文件中

## 阶段五：README.md 瘦身

- [ ] README.md 包含简介（What is this）
- [ ] README.md 包含核心能力（Features）
- [ ] README.md 包含如何使用（How to use）
- [ ] README.md 包含文件架构说明（Structure）
- [ ] README.md 已删除详细的 5 步骤 SOP 流程
- [ ] README.md 已删除详细的输出示例
- [ ] README.md 已删除重复的平台规则说明

## 阶段六：design.md 架构决策记录

- [ ] design.md 已创建
- [ ] 包含工作流映射表（4 个 Workflow 的详细说明）
- [ ] 包含核心边界决策记录
- [ ] 包含目录结构说明和职责边界

## 阶段七：最终验证

- [ ] 目录结构符合 spec 要求
- [ ] 所有文件路径正确
- [ ] SKILL.md 中的 @读取 路径与实际文件路径一致
- [ ] 无重复内容
- [ ] 无遗漏的关键功能
- [ ] 9步输出模板完整保留
- [ ] Git 提交并推送到远程仓库
