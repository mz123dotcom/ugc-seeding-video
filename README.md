---
AIGC:
    Label: "1"
    ContentProducer: 001191440300708461136T1XGW3
    ProduceID: ec9aaeb38e2fc102dd43eac077938ab1_995b1c7be1c111f1b140525400de85a5
    ReservedCode1: sLIwZOcmeZknUUL68Wyo5+VuXkBDqNeCws85C13Y11kGg4rBqWjg2SEU8NRXxjm2guNDf6UP++Ab6ajeekc/mgH/sbEM3JF4PMvrwWYLZ2HcaFicOI1+unlwudP5CRCs4i6eEhUdpNEVJ1j9a1UlSkohUqwjQG12snGRpWKEKCisgfJbGKfkd3etWsI=
    ContentPropagator: 001191440300708461136T1XGW3
    PropagateID: ec9aaeb38e2fc102dd43eac077938ab1_995b1c7be1c111f1b140525400de85a5
    ReservedCode2: sLIwZOcmeZknUUL68Wyo5+VuXkBDqNeCws85C13Y11kGg4rBqWjg2SEU8NRXxjm2guNDf6UP++Ab6ajeekc/mgH/sbEM3JF4PMvrwWYLZ2HcaFicOI1+unlwudP5CRCs4i6eEhUdpNEVJ1j9a1UlSkohUqwjQG12snGRpWKEKCisgfJbGKfkd3etWsI=
---

# ugc-seeding-video

> 带货种草口播短视频的 Agent Skill：按「爆款逻辑」SOP，把产品信息变成可直接开拍的 15 秒 / 30 秒口播脚本、分镜表与视频生成提示词。

核心不是拍得漂亮，而是让陌生人在 **3 秒停住、15 秒听懂、30 秒想买**。

---

## 这个技能解决什么问题

做带货短视频最难的不是运镜，是"说什么、按什么顺序说"。这个技能把一整套口播创作规则固定下来：先锁产品事实，再套爆款结构，最后落到可执行的拍摄 / 生成参数，避免 AI 随口编参数、编价格、编功效。

## 什么时候触发

- 商品种草视频、带货口播视频、UGC 真人出镜短视频
- 探店视频（餐饮 / 门店套餐）
- 15 秒或 30 秒卖货短视频
- 用户说「按爆款逻辑」「按我们的流程做视频」「按这个步骤生成宣传视频」

**不适用**：品牌 TVC、企业宣传片、短剧剧情片、纯剪辑或纯图片任务。

适用品类：食品生鲜、饮品、3C 数码、家居日用、美妆个护、本地生活门店套餐。

## 七条硬规则

1. **先定产品事实，再写台词** —— 用户没给的产地、成分、参数、门店信息、价格、销量、认证、功效一律不写，只讲看得见的外观、可验证的操作与主观体感。
2. **价格只能来自用户** —— 给了 99 元就只能出现 99 元，不附会原价、折扣、限时。
3. **人物设计** —— 无参考图时用文字锁定概念形象并片内一致；有真人照片须确认肖像权，面部发型按图锁定。
4. **不套用旧片设定** —— 换产品即重设人物、场景、台词。
5. **所有生成走确认** —— 封闭式单选确认后才生成；失败不自动重试、不擅自换模型。
6. **默认无字幕** —— 无逐句字幕、无水印、无乱码文字、无假 Logo。
7. **不审片、不筛片** —— 一次成功即交付，改版另存不覆盖。

## 爆款逻辑六条（写台词的唯一标准）

| 环节 | 要求 |
|---|---|
| 开头钩子（3 秒内） | 对比式 / 避坑式 / 反差真香式，三选一 |
| 中段铁律 | 不讲参数、成分、工艺、道理，只讲体感、痛点、场景 |
| 中段结构 | 戳痛点 → 实测感受 → 生活场景 |
| 结尾 | 一句短洗脑金句 + 温和低压力促单 |
| 禁忌 | 禁"最 / 第一 / 全网最低 / 顶级"等绝对词，禁夸大与贬损同行 |
| 时长公式 | 15 秒版与 30 秒版各一套逐句台词模板 |

## 目录结构

```
ugc-seeding-video/
├── SKILL.md                      # 主文件：硬规则、爆款逻辑、生成参数、品类场景表、交付规范
└── references/
    ├── formulas.md               # 15s / 30s 逐句台词模板、四维分析、分镜表格式、已验证案例
    ├── prompt-template.md        # 五段式 Prompt 骨架、多段接续写法、逐字台词时间轴
    └── compliance.md             # 各品类可说 / 不可说清单与典型改写
```

## 安装

支持读取 `SKILL.md` 的 Agent 环境（Claude Code / 各类 Skills 目录规范）通用：

```bash
git clone https://github.com/mz123dotcom/ugc-seeding-video.git
# 放到你的 skills 目录，例如
cp -R ugc-seeding-video ~/.claude/skills/
```

`SKILL.md` 通过相对路径引用 `references/`，保持两者同级即可，无需改路径。

## 生成参数基线（默认值）

| 项 | 默认 |
|---|---|
| 模型 | seedance 2.0 fast（用户指定才换） |
| 比例 | 竖屏 9:16 |
| 时长 | 单段 4–15 秒，30 秒 = 15+15 两段 |
| 声音 | 模型原生普通话人声，保留环境声与动作声，不压强节奏 BGM |
| 画面 | 竖屏手机原生质感、浅景深、生活化白平衡，无棚拍硬光、无磨皮滤镜 |

## 版本与修订

- 用户明确要求修改才出新版，旧版另存不覆盖。
- 效果判断权归用户，工具侧不审片、不筛片。

## License

未指定前请视为保留所有权利；如需开源，建议在此补充 MIT / CC BY 4.0 等许可声明。
*（内容由AI生成，仅供参考）*
