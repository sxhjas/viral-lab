# ViralLab 🌊

**An AI-native TikTok content growth operating system, built as Claude Code skills.**

One pipeline takes a brand from *"here's a product link"* to *"here are shoot-ready content packs"* — in a single day. The human sets quality standards and makes strategy calls; the AI executes everything else: full-coverage comment scraping, audience insight, viral video reverse-engineering, client-grade reports, scripts and storyboards.

> 中文版说明请见 [README.zh-CN.md](README.zh-CN.md)

---

## Why this exists

Traditional TikTok growth research has three fatal flaws:

| Problem | Typical reality | ViralLab's answer |
|---------|----------------|-------------------|
| Research is manual | 2–3 weeks per brand, based on a few dozen comments | **1 day**, 600+ voice-of-customer samples with full comment-section coverage |
| Personas are made up | "Women 25–35 who value quality" — zero evidence | Every persona must carry a **"gear cluster"** — the real products this crowd already owns. Adjectives can be faked; gear clusters can't |
| Experience evaporates | Lessons live in one operator's head | Every mistake becomes a rule inside the SKILL files. **SOP-as-code compounds across brands** |

Validated on 2 complete brand cases. The second one ran the full pipeline in one day and surfaced insights manual research would never find (see [Field results](#field-results)).

## Architecture

```
input: a product name / link
        │
┌───────▼─────────────────────────────────────────┐
│  Brand OS                                        │
│  Step 0 product brief (auto-researched)          │
│  → community mapping (subreddits ARE the first   │
│    persona draft)                                │
│  → dual-track full-coverage VOC (your brand AND  │
│    competitors' comment sections, scrolled to    │
│    the very end)                                 │
│  → insight pyramid: job → intent → emotion →     │
│    identity, every layer backed by user quotes   │
│  → output: client-ready strategy report +        │
│    research task card                            │
└───────┬─────────────────────────────────────────┘
┌───────▼─────────────────────────────────────────┐
│  Research OS (7 steps)                           │
│  keyword sweep (~150 videos) → recency/quality   │
│  filters → top-5 selection (9-dimension scoring) │
│  → frame-by-frame teardown with real transcripts │
│  → cross-video pattern mining → category         │
│  Viral DNA → handoff pack                        │
└───────┬─────────────────────────────────────────┘
┌───────▼─────────────────────────────────────────┐
│  Production OS                                   │
│  script (6-part formula) → storyboard →          │
│  paste-ready AI video prompts (Veo3/Seedance) →  │
│  edit instructions → minimum viable test         │
│  protocol (A/B, 72h data rules)                  │
└───────┬─────────────────────────────────────────┘
        │
┌───────▼──────────────┐   ┌───────────────────────┐
│  Knowledge base       │   │  Delivery layer        │
│  category Viral DNA   │   │  live report page      │
│  hook formula library │   │  (single HTML + charts,│
│  cross-brand insights │   │  deploy to any static  │
│  (compounds per brand)│   │  host)                 │
└───────────────────────┘   └───────────────────────┘
```

## Quickstart

```bash
git clone https://github.com/sxhjas/viral-lab.git
```

**As a Claude Code plugin** — point Claude Code at the repo, or copy `skills/` into your project's `.claude/skills/`. Then:

```
> I want to grow <product link> on TikTok
```

Claude will enter Brand OS Step 0 and walk the pipeline. Each skill is independently triggerable (drop a TikTok link to jump straight into Research OS teardown).

**Recommended workspace layout** (skills read/write these paths, relative to your project root):

```
products/{product}/product_brief.md
brands/{brand}/brand_brief.md + research_task_card.md + data_sources.md
projects/{project}/research_output.md + production/ + session_state.json
knowledge/viral_dna.md + hook_formulas.md + comment_insights.md
```

## What makes it different

1. **Dual-track, full-coverage VOC.** Scraping only your own reviews means only hearing people who already bought. Competitors' comment sections hold the reasons people *didn't* choose you. And comments must be scraped to exhaustion — top comments often hide behind lazy-loading.
2. **Product–community–product graph.** Which subreddit someone posts in already tells you who she is; the gear on her counter is more honest than any survey. Personas without a gear cluster get rejected.
3. **Real transcripts, not thumbnail guessing.** Teardowns use actual VTT subtitles / Whisper transcripts, so hooks and CTAs are quoted verbatim.
4. **Pyramid reports, client-ready.** Conclusion first (one-page, five judgments, each backed by a user quote), methodology sinks to the appendix. If the client can't read it in 2 minutes, it doesn't ship.
5. **Self-evolving SOPs.** Scraper died? Comparison video got called out as staged by 249 upvotes? The fix and the red line get written back into the skill. The system is stronger after every brand.

## Field results

From the second validation case (a North American baby-care appliance brand, anonymized):

- **615** valid voice-of-customer samples in one day (Reddit full threads + TikTok own/competitor comment sections at full coverage + Amazon reviews)
- **150 → 19 → 5** viral videos swept, filtered, torn down frame-by-frame
- Found that the category's #1 competitor is **the dishwasher people already own** — the top objection in every comment section, with the counter-argument sitting in a 2,112-upvote user comment
- Found a **13.9M-view** debate about water safety in the category's biggest video — a traffic pool no brand had claimed
- Watched an influencer's staged comparison get fact-checked by the comment section (249 upvotes) — which became a hard content rule: *comparisons must be fair and reproducible*

## Prerequisites & tool adapters

The skills describe *what* to collect; *how* depends on what you have. Each data source lists alternatives:

| Data source | Primary method | Fallbacks |
|-------------|---------------|-----------|
| Reddit threads + comments | any Reddit CLI/API client | official API, Pushshift-style dumps, manual export |
| TikTok search | any TikTok search CLI | keyword search in browser + manual list |
| TikTok comments (full) | browser automation (scroll loop on `comment-level-1` nodes until count stops growing) | manual scroll + copy |
| TikTok transcripts | official VTT via page data (`subtitleInfos`) or `yt-dlp --write-sub` | Whisper on downloaded audio |
| Amazon reviews | browser automation on product page | manual copy of top reviews |
| Web/market research | any web search API | manual search |

Claude Code with a browser-automation MCP (e.g. Claude in Chrome) covers everything above out of the box.

## Repo layout

```
skills/brand-os/SKILL.md        product brief + market + VOC + personas + strategy report
skills/research-os/SKILL.md     viral discovery + scoring + teardown + Viral DNA
skills/production-os/SKILL.md   scripts + storyboards + AI prompts + test protocol
knowledge/                      empty templates with format specs (fills as you run brands)
examples/                       a fictional brand walked through the full pipeline
```

## Roadmap

- [x] Two full brand validations
- [x] Three-skill architecture finalized
- [ ] Test-result feedback loop (72h data → formula ranking updates)
- [ ] Multi-brand parallel runs (knowledge-base compounding at scale)

## Author

**Jasmine** — growth operator turned AI-systems designer. 5 years in content-led growth (Douyin → TikTok US).

📕 小红书 / RED: [@小飞碟AI啾](https://xhslink.com/m/Akk9B3i582e) — build logs & case studies

## License

[MIT](LICENSE)
