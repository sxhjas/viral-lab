---
name: production-os
description: Turns a research pack into shoot-ready content packs - full voiceover script (6-part formula), frame-by-frame storyboard, paste-ready AI video prompts (Veo3/Seedance style), edit instructions, execution checklist, and a minimum-viable-test protocol (A/B release, 72h data rules). Trigger when a research pack exists, or the user asks for scripts / content generation / AI video versions.
---

# Production OS｜内容生产

## 职责

接收研究交接包，生成可直接执行的内容制作包。只做：脚本 → 分镜 → AI 制作指令 → 制作包 → 测试协议。

前提：`products/{产品}/product_brief.md` 与 `projects/{项目}/research_output.md` 已存在。
输出：`projects/{项目}/production/{视频标题}_production_pack.md`（每条视频独立文件）。

## 工具栈

| 工具 | 用途 | 选择原则 |
|------|------|---------|
| Seedance 类 | AI 视频生成 | 真实人物动作/产品操作 |
| Veo3 类 | AI 视频生成（原生音频） | 对话口播/高质感画面 |
| CapCut/剪映 | 剪辑合成 | 字幕/BGM/拼接 |

同一条视频可混用模型，每个分镜单独选择。**能低成本实拍的优先实拍**（AI 是备选不是信仰——一台产品一部手机十分钟能拍的 6 秒素材，不烧算力）。

## Step 1｜方向选择

从研究包"推荐内容方向"选定：方向 / 参考视频 / 核心骨架 / 目标情绪 / 时长目标。

## Step 2｜脚本生成（六段式公式）

```
Hook → Scenario → Conflict → Value → Proof → CTA
```

**写作规则：**
- Hook ≤15 字（英文 ≤10 词）
- Scenario 具体到时间/地点/状态（"凌晨 2 点站在水槽前"，不是"日常使用"）
- Conflict 必须用用户语言库里的原话词
- Value 省力感可视化：不说"很简单"，说"放进去，按一下，走人"
- Proof 只选最有力的一个（频率×时长类数字证据 > 参数）
- CTA 禁强推话术；**优先站队式提问**（让评论区替你完成完播率和二次分发）

短视频形态可压缩执行（如 6 秒纯贴纸视频：Hook/Conflict 由贴纸承担，Value/Proof 由画面+数字承担，CTA 放文案区）——参考视频验证过的形态不做时长扩写。

附：关键帧字幕文案（核心词全大写强调）+ BGM 建议（风格+剪辑软件搜索词）。

## Step 3｜分镜设计

| 分镜编号 | 时间点 | 时长 | 画面描述 | 景别 | 运镜 | 口播 | 字幕 | 推荐制作 |

原则：**封面帧（第 0 秒）单独列出**；产品操作演示独立分镜；结果展示独立分镜且 ≥3 秒。

## Step 4｜AI 制作指令

每个分镜一条可直接粘贴的 Prompt：

```
【分镜 XX】
推荐模型：
视频 Prompt（英文）：[主体][动作][景别][运镜][光线][背景][风格][时长]
视频 Prompt（中文备注）：
注意事项：
```

规则：人物特征跨分镜一致（**写一段"人物一致性总设定"供所有分镜复用**）；产品外观每镜都提；动作具体到手部；风格统一 `realistic, authentic UGC style, not commercial`。
- Veo3 类：可写 `character says: "[口播]"` + 语气描述；适合口播段
- Seedance 类：手部动作写明 `visible fingers`；少写负向描述

## Step 5｜制作包输出

制作概览 / 脚本 / 分镜表 / AI 指令 / CapCut 剪辑指令（剪辑顺序+字幕规范+BGM 音量配比：口播段 20%、展示段 45-60%+封面截帧）/ **执行检查清单**。

检查清单必含**内容红线核对项**（红线来自 Research OS 的"不建议复刻"结论），典型如：
- ⚠️ 对比内容三原则：素材新鲜现拍、旧方案按正确方式使用、过程可复现——**摆拍失真对比会被评论区当场打假**（实战有 249 赞打假实证），反噬品牌信任
- ⚠️ 安全/健康类叙事必须有据可实测，不做恐吓式内容
- ⚠️ 共情不卖惨：痛点是入口，收口必须是解脱与掌控感

## Step 6｜最小测试协议

**研究给出的公式优先级是推断，数据才是事实。**

第一轮：每条公式 1 条测试视频（最低可接受质量——测的是 Hook 和结构，不是制作水平）；间隔 48h 发布；统一 CTA、统一最优时段；字幕必加。

**72h 指标（按优先级）：** 完播率（>25% = 结构有效）> 分享数（>播放 0.5%）> 评论购买意向词（"where to buy/link?"）> 收藏 > 播放增速。**不看点赞。**

决策规则：完播达标+有购买意向→赢家进入变体量产（换身份/场景做 3-5 条）；完播达标但无购买意向→改 Value/Proof 重测；完播不达标→只换 Hook 重测，不动其他变量；全军覆没→回 Research OS 重审拆解结论。

测试结果回写 `knowledge/hook_formulas.md`（追加实测数据）和 `projects/{项目}/test_results.md`。

## 注意

- 每条视频独立文件；AI Prompt 用英文
- 写完 Step 4 统一检查人物一致性
- 每次完成更新 session_state.json
