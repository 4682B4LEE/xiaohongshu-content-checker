# 小红书笔记检测 Skill v2.5.0 优化计划

## 目标

根据 SOLO Skill 提分官评审反馈，针对性修复三个扣分点，提升总分从 17/25 到 20+/25。

## 修改范围

- `/Users/roylee/Desktop/Trae/RedBook-Skills/xiaohongshu-content-checker/SKILL.md`
- `/Users/roylee/Desktop/Trae/RedBook-Skills/xiaohongshu-content-checker/README.md`
- `/Users/roylee/Desktop/Trae/RedBook-Skills/xiaohongshu-content-checker/references/mode-full.md`
- `/Users/roylee/Desktop/Trae/RedBook-Skills/xiaohongshu-content-checker/references/mode-fast.md`
- `/Users/roylee/Desktop/Trae/RedBook-Skills/xiaohongshu-content-checker/references/mode-batch.md`
- `/Users/roylee/Desktop/Trae/RedBook-Skills/xiaohongshu-content-checker/references/mode-video.md`
- 新增 `/Users/roylee/Desktop/Trae/RedBook-Skills/xiaohongshu-content-checker/references/feedback/FEEDBACK_TEMPLATE.md`
- 新增 `/Users/roylee/Desktop/Trae/RedBook-Skills/xiaohongshu-content-checker/CHANGELOG.md`

---

## 任务一：自进化力 - 添加反馈收集与数据沉淀机制

### 1.1 在 SKILL.md 中新增反馈收集工作流

**位置**：在"上下文复用"之后，"唤醒语"之前

**新增内容**：
```markdown
## 反馈收集与自进化

每次检测完成后，在输出底部添加反馈收集区：

```
---
💬 本次检测是否准确？
- [ ] 完全准确
- [ ] 有误判（请说明：______）
- [ ] 有漏判（请说明：______）
- [ ] 其他建议（请说明：______）
```

**反馈处理规则**：
- 如果用户反馈误判/漏判，记录到对话上下文
- 定期（每月）分析反馈数据，更新知识库
- 高频误判项优先更新 SENSITIVE_WORDS.md
- 高频漏判项补充到 REPLACEMENT_SUGGESTIONS.md
```

### 1.2 创建 references/feedback/FEEDBACK_TEMPLATE.md

**文件内容**：
```markdown
---
name: feedback-template
version: 2.5.0
last_updated: 2026-05-21
type: reference-knowledge
---

# 反馈记录模板

## 记录格式

| 日期 | 笔记类型 | 误判/漏判内容 | 用户反馈 | 处理状态 | 知识库更新 |
|------|---------|--------------|---------|---------|-----------|

## 月度分析工作流

1. 汇总当月所有反馈
2. 分类统计：误判类型 / 漏判类型 / 其他建议
3. 高频问题（出现 ≥3 次）优先更新知识库
4. 更新后验证：用反馈案例重新检测，确认修复

## 版本历史

- v2.5.0 (2026-05-21): 新增反馈收集与自进化机制。
```

### 1.3 在 mode-full.md / mode-fast.md / mode-batch.md / mode-video.md 的输出结构末尾添加反馈区

**mode-full.md 修改**：
在"6. 发布前检查清单"后新增：
```markdown
### 7. 反馈收集

```
---
💬 本次检测是否准确？
- [ ] 完全准确
- [ ] 有误判（请说明：______）
- [ ] 有漏判（请说明：______）
- [ ] 其他建议（请说明：______）

您的反馈将帮助我们持续优化检测准确率。
```
```

**mode-fast.md 修改**：
在"4. 简化发布前检查清单"后新增简化版反馈区。

**mode-batch.md 修改**：
在汇总报告末尾添加批量反馈收集区。

**mode-video.md 修改**：
在视频专项检测后添加反馈区。

---

## 任务二：体验感 - 增强视觉层次与交互确认

### 2.1 在 mode-full.md 中强制使用 emoji 色标

**修改"3. 风险检测结果"**：
```markdown
### 3. 风险检测结果

**违规风险**：
| 风险等级 | 标识 | 说明 |
|---------|------|------|
| 极高 | 🔴 | 强导流、医疗/金融/教育效果承诺 |
| 高 | 🟠 | 虚假宣传、绝对承诺 |
| 中 | 🟡 | 广告法极限词、诱导互动 |
| 低 | 🟢 | 标题党、同质化营销黑话 |

**流量风险**：
| 风险等级 | 标识 | 说明 |
|---------|------|------|
| 高 | 🟠 | 可能影响推荐表现 |
| 中 | 🟡 | 存在推荐受限风险 |
| 低 | 🟢 | 轻微影响 |
```

### 2.2 在 mode-full.md 中采用"修改前 | 修改后"表格对比

**修改"5. 修改建议与优化版本"**：
```markdown
### 5. 修改建议与优化版本

**标题优化**：

| 修改前 | 修改后 | 修改原因 |
|--------|--------|---------|
| [原标题] | [优化标题] | [说明] |

**正文优化**：

| 修改前 | 修改后 | 修改原因 |
|--------|--------|---------|
| [原文片段] | [优化片段] | [说明] |

**标签优化**：

| 修改前 | 修改后 | 修改原因 |
|--------|--------|---------|
| [原标签] | [优化标签] | [说明] |
```

### 2.3 在 mode-full.md 中增加关键节点交互确认

**在"5. 修改建议与优化版本"后新增**：
```markdown
> 💡 **交互确认**：是否需要生成完整优化版本？
> - 回复"是"：输出完整改写后的笔记
> - 回复"否"：仅保留修改建议，不输出改写版本
```

### 2.4 在 mode-fast.md 中同样增加色标和对比表格

**修改"2. 命中风险列表"**：
```markdown
### 2. 命中风险列表

| 风险等级 | 标识 | 风险项 | 位置 | 修改建议 |
|---------|------|--------|------|---------|
| 🔴 极高 | +4 | [风险描述] | [位置] | [建议] |
| 🟠 高 | +3 | [风险描述] | [位置] | [建议] |
| 🟡 中 | +2 | [风险描述] | [位置] | [建议] |
| 🟢 低 | +1 | [风险描述] | [位置] | [建议] |
```

---

## 任务三：完成度 - 规范版本历史

### 3.1 创建 CHANGELOG.md

**文件内容**：
```markdown
# Changelog

所有 notable changes 将记录在此文件。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/)。

## [2.5.0] - 2026-05-21

### Added
- 新增反馈收集与自进化机制（references/feedback/FEEDBACK_TEMPLATE.md）
- 新增 CHANGELOG.md 规范版本记录
- 输出模板强制使用 emoji 色标（🔴🟠🟡🟢）
- 修改建议采用"修改前 | 修改后"表格对比
- 关键节点增加交互确认

### Changed
- 优化输出模板视觉层次
- 规范所有 references 版本历史格式

## [2.4.0] - 2026-05-21

### Changed
- 重写 README.md 反映最新架构
- 删除 agents/ 目录

## [2.3.0] - 2026-05-18

### Added
- 新增可计算风险评分规则（references/risk-rubric.md）
- 新增 Mode Router：极速排雷/完整检测/批量检测/视频笔记
- 新增 mode-fast.md / mode-full.md / mode-batch.md / mode-video.md

### Changed
- SKILL.md 重构为路由中心（716行 → 87行）
- 拆分发布风险等级与定位匹配度为独立维度
- 清理绝对化表述（"必限流"→"存在推荐受限风险"）

### Removed
- 删除 design.md、test-results/（开发文档移出运行包）

## [2.1.0] - 2026-05-14

### Changed
- 重构为调度中心架构
- 引入四大核心工作流
- 知识库下沉按需加载

## [2.0.0] - 2026-05-12

### Added
- 初始版本
- 完整检测工作流、敏感词库、输出模板
```

### 3.2 更新 README.md 版本历史

**修改版本历史表格**：
```markdown
| 版本 | 日期 | 变更说明 |
|------|------|----------|
| 2.5.0 | 2026-05-21 | 新增反馈收集机制、输出色标与对比表格、CHANGELOG规范 |
| 2.4.0 | 2026-05-21 | 重写 README 反映最新架构，删除 agents 目录 |
| 2.3.0 | 2026-05-18 | Skill 架构改造：路由中心 + 知识库拆分，新增可计算风险评分 |
| 2.1.0 | 2026-05-14 | 重构为调度中心架构，引入四大核心工作流 |
| 2.0.0 | 2026-05-12 | 初始版本 |
```

### 3.3 更新所有 references 文件的版本历史

将 v2.4.0 的"版本号更新"改为具体变更说明：
- mode-full.md: "v2.4.0 (2026-05-21): 版本号更新。" → "v2.4.0 (2026-05-21): 版本号与日期统一更新。"
- mode-fast.md: 同上
- mode-batch.md: 同上
- mode-video.md: 同上
- risk-rubric.md: 同上
- PLATFORM_RULES.md: 同上
- SENSITIVE_WORDS.md: 同上
- REPLACEMENT_SUGGESTIONS.md: 同上
- ACCOUNT_POSITIONING.md: 同上
- CONTENT_EXAMPLES.md: 同上

---

## 任务四：版本号统一更新

### 4.1 更新所有文件版本号到 2.5.0

**需要更新的文件**（12个）：
1. SKILL.md: version 2.4.0 → 2.5.0
2. README.md: version 2.4.0 → 2.5.0
3. references/risk-rubric.md: version 2.4.0 → 2.5.0
4. references/mode-fast.md: version 2.4.0 → 2.5.0
5. references/mode-full.md: version 2.4.0 → 2.5.0
6. references/mode-batch.md: version 2.4.0 → 2.5.0
7. references/mode-video.md: version 2.4.0 → 2.5.0
8. references/platform/PLATFORM_RULES.md: version 2.4.0 → 2.5.0
9. references/detection/SENSITIVE_WORDS.md: version 2.4.0 → 2.5.0
10. references/detection/REPLACEMENT_SUGGESTIONS.md: version 2.4.0 → 2.5.0
11. references/positioning/ACCOUNT_POSITIONING.md: version 2.4.0 → 2.5.0
12. references/examples/CONTENT_EXAMPLES.md: version 2.4.0 → 2.5.0

---

## 实施步骤

1. [ ] 创建 references/feedback/ 目录和 FEEDBACK_TEMPLATE.md
2. [ ] 创建 CHANGELOG.md
3. [ ] 在 SKILL.md 中新增反馈收集工作流
4. [ ] 在 mode-full.md 中添加反馈区、色标、对比表格、交互确认
5. [ ] 在 mode-fast.md 中添加反馈区、色标、对比表格
6. [ ] 在 mode-batch.md 和 mode-video.md 中添加反馈区
7. [ ] 更新 README.md 版本历史
8. [ ] 更新所有 references 文件的版本历史
9. [ ] 统一所有文件版本号到 2.5.0
10. [ ] 提交 Git

## 预期提分

| 修复项 | 维度 | 预计提分 |
|--------|------|---------|
| 反馈收集机制 | 自进化力 | +2~3 分 |
| 输出色标与对比表格 | 体验感 | +0.5~1 分 |
| CHANGELOG 规范 | 完成度 | +0.5 分 |
| **合计** | | **+3~4.5 分** |

**预期总分**：17 + 3~4.5 = **20~21.5/25**（达到 PASS 门控）
