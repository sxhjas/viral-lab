---
name: research-os
description: Viral video reverse-engineering for a product category. Sweeps ~150 recent videos by keyword, filters by recency/quality, scores candidates on 9 dimensions to pick a Top 5, tears each down frame-by-frame using real transcripts (storyboard first, then hook mechanics, emotional flow, reusable templates), mines cross-video patterns into a category Viral DNA, and hands off a research pack. Trigger when a research task card arrives from brand-os, when the user drops a short-video link to analyze, or asks to find viral videos / analyze competitors' content.
---

# Research OS｜爆款研究

## 职责

接收产品档案 + 研究任务卡，执行标准化爆款研究，输出研究包供 Production OS 使用。不做脚本生成。

输出：`projects/{项目}/research_output.md`；知识库回写 `knowledge/`（见 Step 7）。

## 视频内容获取（两级）

- 🥇 **真实逐字稿**（Step 4 必用）：优先取平台官方字幕（页面数据 JSON 的 `subtitleInfos` 里有 VTT 地址，页内 fetch 即得；或 `yt-dlp --write-sub --write-auto-sub`）；无字幕的口播视频用 Whisper 转录音频。**Hook 第一句话和 CTA 必须逐字准确**
- 🥈 **封面图**（Step 3 快筛用）：oEmbed 接口取 thumbnail_url。封面=第一帧，可确认 Hook 视觉语言，不能推断后续内容

## Step 1｜内容战略层

**不重新发明内容方向**——直接接收 Brand Brief 的内容矩阵，本步只补三样：搜索关键词（从用户语言库提取）、平台策略、搜索优先级。

执行前必读 `knowledge/` 三个文件：品类已有记录→优先验证既有公式仍否有效；无记录→正常执行且 Step 7 必须回写。

无爆款可参考的方向（零竞争空位）不搜索，直接标注"进 Production OS 原创"。

## Step 2｜爆款发现

**样本标准：** 初扫 ~100-150 条（多平台合并）→ 去重过滤后候选池 ~20 条 → Top 5 深拆。

**时效规则（最高优先级）：**
- 🥇 优先 1 个月内发布；🥈 不足 100 条扩至 3 个月；❌ 更早一律丢弃，除非播放 ≥500 万
- 判断方法：短视频平台的视频 ID 通常内嵌时间戳（如 TikTok `video ID >> 32` = Unix 时间戳）

**过滤：** 播放 <10 万丢弃；数据异常（如赞播比畸低）标注不入选；关键词命中但内容无关丢弃；同账号最多 2 条入池。

**关键词五维**（每维 2-3 个词）：品牌词+产品词 / 卖点词（用用户的说法）/ 痛点词 / 竞品词 / 场景词。

**候选池字段：** 编号/账号/平台/链接/发布日期/播放/赞/分享/评论/一句话方向/数据可信度。**每条必须附完整链接。**

## Step 3｜评分筛选（20 → 5）

9 维基础分（各 10 分）：Hook 强度 / 完播潜力 / 评论质量 / 分享价值 / 产品适配度 / AI 复刻可行性 / 转化逻辑 / 可裂变潜力 / 受众匹配度。

**品牌权重调整（评分后执行，±2 分/维）：** 从 Brand Brief 提取——主导意图/情绪对应的内容类型加分；原点人群重合度加分；有摆拍嫌疑的对比内容在 AI 复刻可行性上减分。

只对播放量前 10 做全维评分，其余标注落选原因。Top 5 需覆盖任务卡的多个方向（单一方向刷屏时，为方向覆盖保留代表作）。

## Step 4｜逐条深度拆解（①-⑨）

**分镜先于分析输出。** 每条视频按以下九节：

1. **① 基础拆解**：类型/时长/场景/人物设定/产品出现方式/是否口播（标注逐字稿来源 ✅）/过程展示/对比展示
2. **② 分镜结构**（5 列缺一不可）：分镜｜画面｜口播（中文）｜口播（英文）｜字幕 + BGM
3. **③ 语言层**：Hook/演示/结果/CTA 各段核心句（EN+CN）+ 字幕设计规律
4. **④ Hook 机制**：类型 + 前 3 秒逐层结构 + 触发机制（用心理学机制术语）
5. **⑤ 情绪路径**：逐时段情绪状态 + 用户内心独白
6. **⑥ 爆款结构公式**：模块化拼装式
7. **⑦ 可复用模板**：Hook/演示/结果/CTA 原文模板（含[变量槽位]）+ 中文
8. **⑧ 变量系统**：变量类型/当前值/新品牌可替换选项
9. **⑨ 复刻建议**：核心发现一句话 + 3 条变体方向

**拆解不止看内容，必须看评论区**：高赞评论是品类情绪的直接证据（实战中曾发现最大爆款的评论区本身就是一场无品牌认领的万级互动辩论——这类发现比视频本身值钱）。

## Step 5｜共同规律提炼

五问，每条规律一句话结论+支撑案例：共同 Hook 模式 / 共同内容结构 / 共同视觉规律【推断需标注】/ 共同转化触发点 / 共同评论关键词。

## Step 6｜品类 Viral DNA

五问：停留驱动力 / 完播驱动力 / 传播驱动力 / 转化驱动力 / 底层传播逻辑（这个品类最不可替代的传播引擎是什么）+ 最值得复制的内容基因 3 条。

## Step 7｜研究交接包 + 知识库回写（必须执行）

交接包：研究摘要 / Top 5 拆解 / 共同规律 / Viral DNA / 推荐内容方向 3-5 个（具体到脚本方向）/ **AI 可行性排序**（供 Production OS 定优先级）/ **不建议复刻的内容类型**（附原因）。

知识库回写（追加不覆盖，格式 `## {品类}｜来源：{品牌}｜{日期}`）：
- `knowledge/viral_dna.md`：本品类驱动力全套
- `knowledge/hook_formulas.md`：验证有效的新 Hook 公式（**必须附视频链接+播放量作为证据**）
- `knowledge/comment_insights.md`：跨品牌共性的用户语言模式（仅品牌专属的不写）

## 注意

- 推断内容必须标注，不得作为 Production OS 制作依据
- 数据异常必须标注，不得忽略
- 每步完成更新 session_state.json
