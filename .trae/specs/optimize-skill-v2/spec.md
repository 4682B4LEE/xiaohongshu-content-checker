# 小红书内容检测 Skill 优化 Spec

## Why

当前的小红书内容检测 Skill 虽然具备基础的敏感词检测和账号定位分析能力，但在"人设匹配度诊断""营销浓度评估""CES算法洞察"等深度风控维度上存在不足。结合 gemini.md 的专家方案，需要对 Skill 的工作流程、检测维度、输出格式进行系统性升级，帮助创作者从根源上提升笔记获取自然流的概率。

## What Changes

- **重构工作流程**：将原4阶段流程升级为5步骤标准工作流（SOP），强化"先定位、后检测"原则
- **新增人设确认环节**：在账号定位阶段明确引入"人设类型"确认（干货型/测评型/情绪共鸣型/好物分享型）
- **新增笔记意图确认**：在检测前确认笔记核心诉求（涨粉/带货/互动/引流私域）和目标关键词
- **新增营销浓度判断**：评估内容是否过度像硬广、是否缺少真实用户体验（UGC感）
- **强化变体敏感词识别**：在工作流程中明确强调谐音梗、拼音缩写、emoji替代等变体识别
- **引入CES评分模型**：在优化建议中融入点赞、收藏、评论、转发、完播率的人群标签权重分析
- **强化网感要求**：明确要求修改后的文案必须符合小红书平台语境（emoji合理、口语化、有情绪价值）
- **丰富最终输出**：增加"3个高分标题备选"和"发布前CheckList"
- **更新参考文档**：同步更新 references/ 下的敏感词库和替换建议库

## Impact

- Affected specs: 小红书内容检测 Skill 的核心工作流程、输出格式、参考文档
- Affected code: SKILL.md, README.md, references/SENSITIVE_WORDS.md, references/REPLACEMENT_SUGGESTIONS.md

## ADDED Requirements

### Requirement: 五步标准工作流（SOP）

The system SHALL provide a standardized 5-step workflow for content auditing:

#### Scenario: 账号定位与受众诊断
- **WHEN** 用户开始检测流程
- **THEN** 系统必须先收集账号的垂类赛道、人设类型、粉丝画像，建立审核基准线
- **AND** 人设类型必须包括：干货型、测评型、情绪共鸣型、好物分享型

#### Scenario: 当前笔记方向确认
- **WHEN** 用户提供待测文案
- **THEN** 系统必须先确认笔记的核心诉求（涨粉/带货转化/纯日常互动/引流私域）
- **AND** 确认笔记期望打中的搜索关键词或标签

#### Scenario: 自然流阻碍因素排查
- **WHEN** 完成定位和意图确认后
- **THEN** 系统进行宏观层面的排查：
  - 匹配度诊断：当前内容是否会破坏账号垂直度
  - 营销浓度判断：是否过度像硬广、是否缺少UGC感
  - 外部平台导流风险：是否有向微信、淘宝等第三方导流的暗号

#### Scenario: 文案像素级敏感词排雷
- **WHEN** 进行敏感词检测
- **THEN** 输出格式必须包含：原句、风险词/敏感词、违规类型、限流概率、修改建议
- **AND** 必须识别变体形式：谐音梗、拼音缩写、符号间隔、emoji替代、错别字

#### Scenario: 最终优化与发布建议
- **WHEN** 完成所有诊断后
- **THEN** 系统必须提供：
  - 3个包含目标关键词且不违规的吸引力标题备选
  - 全文安全重写版（排版美观，合理添加Emoji）
  - 发布前CheckList（图片侵权、话题标签等提醒）

### Requirement: CES算法洞察

The system SHALL incorporate CES scoring model insights in optimization suggestions:

#### Scenario: 提供算法优化建议
- **WHEN** 给出自然流优化建议
- **THEN** 系统应结合CES评分模型（点赞、收藏、评论、转发、完播率）及人群标签权重
- **AND** 解释为什么某些修改能提升推荐概率

### Requirement: 网感保持

The system SHALL ensure modified content maintains Xiaohongshu platform tone:

#### Scenario: 文案重写
- **WHEN** 提供修改后的文案
- **THEN** 必须符合小红书平台语境：emoji使用合理、口语化、有情绪价值
- **AND** 不能像机器人发文，保持真实分享的UGC感

## MODIFIED Requirements

### Requirement: 敏感词检测维度

The system SHALL enhance sensitive word detection with variant recognition:

#### Scenario: 变体识别
- **WHEN** 检测敏感词
- **THEN** 除常规词汇外，必须识别：
  - 拼音缩写：VX、GZH、PYQ
  - 谐音替换：薇信、加微、票圈
  - 符号间隔：微❤️、V/X
  - emoji替代：微🌟、加👆
  - 错别字：维信、威信

### Requirement: 输出格式规范

The system SHALL provide structured output with risk classification:

#### Scenario: 风险等级判定
- **WHEN** 输出检测结果
- **THEN** 必须明确标注违规类型：绝对化用语、政治敏感、导流违规、软广嫌疑、贬低竞品等
- **AND** 给出限流概率评估：高/中/低

## REMOVED Requirements

无移除需求，本次为增强型优化。
