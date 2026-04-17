---
name: travel-guide
description: 旅行攻略生成技能 - 根据用户指定的目的地、天数、出行时间和旅行风格，自动生成结构完整、信息详实的旅行攻略 Markdown 文档。输出包含：准备清单、天气参考、行程总览、每日详细行程（含交通/玩法/拍照/避坑）、美食打卡、住宿指南、交通指南、拍照出片点、实用Tips和朋友圈文案等模块。支持多种旅行风格（轻松版/特种兵版/亲子版/美食版/穷游版等）。
version: "1.3.0"
author: SOLO
tags:
  - travel
  - guide
  - trip-planning
  - markdown
  - travel-itinerary
---

# 旅行攻略生成技能 (Travel Guide Generator)

## 技能概述

本技能用于根据用户输入的目的地、天数、出行时间和旅行风格，自动生成一份**结构完整、信息详实、排版精美**的旅行攻略 Markdown 文档。生成的攻略文档参考小红书/飞书文档风格的旅行攻略模板，使用 HTML+CSS 实现卡片布局、色块包裹等视觉效果，包含行程规划、美食推荐、住宿指南、交通指南、拍照攻略、实用Tips等全方位信息。

## 触发条件

当用户的请求包含以下意图时，应立即调用本技能：
- 要求生成旅行攻略、旅游攻略、出行计划
- 询问某地的旅游/旅行信息并希望得到系统化的攻略文档
- 要求制定旅行行程、旅游计划
- 请求某目的地的 N天N晚攻略

## 输入参数

用户需要提供（或可推断）以下信息：

| 参数 | 必填 | 说明 | 示例 |
|------|------|------|------|
| 目的地 | ✅ | 旅行目的地城市/地区 | 西安、成都、东京、巴黎 |
| 天数 | ✅ | 旅行天数 | 4天3晚、3天2晚、7天6晚 |
| 出行时间 | ⚠️ 推荐 | 具体出行日期或季节 | 五一、国庆、暑假、3月中旬 |
| 旅行风格 | ❌ 可选 | 攻略风格定位 | 轻松版、特种兵版、亲子版、美食版、穷游版 |
| 出行人数 | ❌ 可选 | 人数和人群 | 情侣、家庭亲子、朋友3人、独自旅行 |
| 出发城市 | ❌ 可选 | 从哪里出发 | 北京、上海、广州 |

> 如果用户未提供出行时间或旅行风格，应主动询问或根据上下文推断合理的默认值。

## 输出格式

输出为 **Markdown (.md)** 格式的旅行攻略文档，严格遵循以下模板结构和排版规范。文档开头必须包含全局 CSS 样式块以实现卡片布局和统一字体。

---

## 📋 攻略文档模板结构

生成的 Markdown 文档必须包含以下所有章节（按顺序排列）：

### 第零章：全局样式（⭐必须放在文档最开头）

```html
<div style="font-size:14px; line-height:1.8; color:#333;">
```

> ⚠️ **重要**：文档最开头必须包裹此 `<div>` 标签，确保全文统一 14px 字体。文档最末尾用 `</div>` 闭合。

### 第一章：封面标题区

```html
<div align="center" style="margin-bottom:20px;">

# 🏮 {目的地}{天数}旅行攻略

### {风格标签} · {季节/节日}推荐

</div>

![{目的地}封面](images/{目的地}封面.jpg)

<div align="center" style="margin:20px 0;">

<table style="width:100%; max-width:600px; border-collapse:collapse; font-size:14px;">
<tr>
<td style="padding:12px; text-align:center; border:1px solid #eee; border-radius:8px;">📅 出行时间<br><b>{具体日期/季节}</b></td>
<td style="padding:12px; text-align:center; border:1px solid #eee; border-radius:8px;">👥 出行人群<br>{人群描述}</td>
<td style="padding:12px; text-align:center; border:1px solid #eee; border-radius:8px;">🚗 出行方式<br><b>{交通方式}</b></td>
<td style="padding:12px; text-align:center; border:1px solid #eee; border-radius:8px;">💰 人均预算<br><b>{预算范围}</b></td>
<td style="padding:12px; text-align:center; border:1px solid #eee; border-radius:8px;">✈️ 出发城市<br><b>{出发地}</b></td>
</tr>
</table>

</div>
```

### 第二章：准备清单（⭐卡片布局）

```html
## 📦 出发前准备清单

> ▼ {一句话提示，如"这些物品一个都不能少！"}

<table style="width:100%; border-collapse:separate; border-spacing:12px; table-layout:fixed;">
<tr>
<td style="background:#f0f7ff; border-radius:12px; padding:16px; vertical-align:top; width:25%;">
<div style="font-size:16px; font-weight:bold; margin-bottom:10px;">🪪 证件类</div>
<div style="font-size:13px; line-height:2;">
☐ 身份证（<b>必备</b>）<br>
☐ 学生证（景点<b>半价</b>）<br>
☐ 驾驶证（自驾必备）<br>
☐ 护照/签证（出境游）
</div>
</td>
<td style="background:#f5fff0; border-radius:12px; padding:16px; vertical-align:top; width:25%;">
<div style="font-size:16px; font-weight:bold; margin-bottom:10px;">📱 电子设备</div>
<div style="font-size:13px; line-height:2;">
☐ 手机 + 充电器<br>
☐ 充电宝（<b>必备</b>）<br>
☐ 耳机<br>
☐ 相机/自拍杆
</div>
</td>
<td style="background:#fff5f0; border-radius:12px; padding:16px; vertical-align:top; width:25%;">
<div style="font-size:16px; font-weight:bold; margin-bottom:10px;">👗 穿搭准备</div>
<div style="font-size:13px; line-height:2;">
☐ 舒适运动鞋<br>
☐ {季节衣物}（<b>温差大</b>）<br>
☐ 墨镜/防晒衣<br>
☐ {特色服饰}
</div>
</td>
<td style="background:#fef5ff; border-radius:12px; padding:16px; vertical-align:top; width:25%;">
<div style="font-size:16px; font-weight:bold; margin-bottom:10px;">🧴 洗漱护肤</div>
<div style="font-size:13px; line-height:2;">
☐ 防晒霜（<b>SPF50+</b>）<br>
☐ 保湿面膜/润唇膏<br>
☐ 晴雨伞<br>
☐ 湿巾/纸巾
</div>
</td>
</tr>
<tr>
<td style="background:#fff8e6; border-radius:12px; padding:16px; vertical-align:top; width:33%;">
<div style="font-size:16px; font-weight:bold; margin-bottom:10px;">💊 应急物品</div>
<div style="font-size:13px; line-height:2;">
☐ 肠胃药/感冒药<br>
☐ 创可贴<br>
☐ 晕船药（<b>坐船必带</b>）<br>
☐ 防蚊液
</div>
</td>
<td colspan="2" style="background:#f0f4ff; border-radius:12px; padding:16px; vertical-align:top; width:67%;">
<div style="font-size:16px; font-weight:bold; margin-bottom:10px;">🚗 车辆检查（自驾适用）</div>
<div style="font-size:13px; line-height:2;">
☐ 检查轮胎气压和磨损 &nbsp;&nbsp; ☐ 检查机油/冷却液/刹车油 &nbsp;&nbsp; ☐ <b>加满油</b>（出发前） &nbsp;&nbsp; ☐ 备好ETC卡
</div>
</td>
</tr>
</table>
```

> **卡片布局规则**：
> - 使用 `<table>` + `border-collapse:separate; border-spacing:12px` 实现卡片间距
> - 每个卡片使用不同浅色背景（蓝/绿/橙/紫/黄），`border-radius:12px` 圆角
> - 第一行 4 列（证件/电子/穿搭/洗漱），第二行 2~3 列（应急/车辆）
> - 卡片内标题 `font-size:16px; font-weight:bold`，内容 `font-size:13px; line-height:2`

### 第三章：天气参考

```html
## 🌤️ {目的地}天气参考（{季节}）

<table style="width:100%; border-collapse:collapse; font-size:13px; color:#333; font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Roboto,'PingFang SC','Microsoft YaHei',sans-serif;">
<tr style="background:#f5f5f5; font-weight:500;">
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">日期</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">天气</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">温度</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">穿衣建议</th>
</tr>
<tr>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>Day1</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">{天气emoji} {天气}</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{温度范围}℃</b></td>
<td style="padding:14px 16px;">{建议}</td>
</tr>
<tr style="background:#fafafa;">
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>Day2</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">{天气emoji} {天气}</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{温度范围}℃</b></td>
<td style="padding:14px 16px;">{建议}</td>
</tr>
<tr>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>Day3</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">{天气emoji} {天气}</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{温度范围}℃</b></td>
<td style="padding:14px 16px;">{建议}</td>
</tr>
</table>

<div style="background:#fff8e1; border-left:4px solid #ffc107; padding:12px 16px; border-radius:0 8px 8px 0; margin:12px 0; font-size:14px;">
💡 <b>温馨提示</b>：{季节性穿衣建议和注意事项，关键数据<b>加粗</b>标注}
</div>
```

### 第四章：行程总览

```html
## 🗺️ 行程总览

> ▼ {一句话概括行程特色}

<table style="width:100%; border-collapse:separate; border-spacing:10px; font-size:14px;">
<tr>
<td style="background:#e8f5e9; border-radius:12px; padding:16px; width:33%; vertical-align:top;">
<div style="font-size:18px; margin-bottom:8px;">🏃 <b>DAY1</b></div>
<div style="font-size:13px; color:#666; margin-bottom:6px;">🛣️ {当日主题}</div>
<div style="font-size:13px;">{景点A} → <b>{核心景点}</b> → {景点C}</div>
</td>
<td style="background:#e3f2fd; border-radius:12px; padding:16px; width:33%; vertical-align:top;">
<div style="font-size:18px; margin-bottom:8px;">🏃 <b>DAY2</b></div>
<div style="font-size:13px; color:#666; margin-bottom:6px;">🏞️ {当日主题}</div>
<div style="font-size:13px;"><b>{核心景点}</b> → {景点F} → {景点G}</div>
</td>
<td style="background:#fce4ec; border-radius:12px; padding:16px; width:33%; vertical-align:top;">
<div style="font-size:18px; margin-bottom:8px;">🏃 <b>DAY3</b></div>
<div style="font-size:13px; color:#666; margin-bottom:6px;">🌊 {当日主题}</div>
<div style="font-size:13px;"><b>{核心景点}</b> → {景点J} → 返程</div>
</td>
</tr>
</table>
```

### 第五章：每日详细行程（⭐核心章节·卡片样式）

每一天的行程按以下格式输出：

```html
<hr style="border:none; border-top:2px solid #eee; margin:30px 0;">

## 🔻 DAY{N}：{景点A} → {景点B} → {景点C} → {景点D}

> 📍 当日主题：{一句话描述当日特色}

### ✅ 景点游玩建议

#### ① 上午游玩建议（{景点组合}，建议安排 <b>{X}h</b>）

![{景点名称}](images/{景点名称}.jpg)

<table style="width:100%; border-collapse:separate; border-spacing:0; margin:12px 0; font-size:14px;">
<tr>
<td style="background:#e3f2fd; border-radius:12px 12px 0 0; padding:14px 18px; border-bottom:2px solid #2196f3;">
<div style="font-size:16px; font-weight:bold;">☐ {景点名称1}</div>
</td>
</tr>
<tr>
<td style="background:#f5f9ff; padding:16px 18px; border-left:3px solid #2196f3;">
<div style="margin-bottom:10px;">🚗 <b>交通</b>：{交通方式}，约<b>{X}km / {X}h</b>。{具体路线说明}</div>
<div style="margin-bottom:10px;">🎯 <b>玩法</b>：{景区简介}。<br>
&nbsp;&nbsp;🎫 门票：<b>{价格}</b>（建议提前在<b>"{公众号名}"</b>预约）<br>
&nbsp;&nbsp;🕐 开放时间：<b>{开始时间}~{结束时间}</b><br>
&nbsp;&nbsp;📍 游览路线：{路线A} → <b>{核心看点}</b> → {路线C}<br>
&nbsp;&nbsp;⏱️ 建议游玩 <b>{X}~{Y}小时</b></div>
<div style="margin-bottom:10px;">📷 <b>拍照</b>：<br>
&nbsp;&nbsp;• <b>{最佳机位}</b>：{拍摄建议}<br>
&nbsp;&nbsp;• <b>{第二机位}</b>：{拍摄建议}</div>
<div>⚠️ <b>避坑</b>：<br>
&nbsp;&nbsp;• 🔴 {最重要警示，<b>加粗</b>}<br>
&nbsp;&nbsp;• {其他注意事项}</div>
</td>
</tr>
</table>

#### ② 下午游玩建议（{景点名称}，建议安排 <b>{X}h</b>）

<table style="width:100%; border-collapse:separate; border-spacing:0; margin:12px 0; font-size:14px;">
<tr>
<td style="background:#e8f5e9; border-radius:12px 12px 0 0; padding:14px 18px; border-bottom:2px solid #4caf50;">
<div style="font-size:16px; font-weight:bold;">☐ {景点名称2}</div>
</td>
</tr>
<tr>
<td style="background:#f5fff5; padding:16px 18px; border-left:3px solid #4caf50;">
{同上格式，交通/玩法/拍照/避坑}
</td>
</tr>
</table>

#### ③ 晚上游玩建议（{活动/景点}，建议安排 <b>{X}h</b>）

<table style="width:100%; border-collapse:separate; border-spacing:0; margin:12px 0; font-size:14px;">
<tr>
<td style="background:#fff3e0; border-radius:12px 12px 0 0; padding:14px 18px; border-bottom:2px solid #ff9800;">
<div style="font-size:16px; font-weight:bold;">☐ {活动/景点名称}</div>
</td>
</tr>
<tr>
<td style="background:#fffbf5; padding:16px 18px; border-left:3px solid #ff9800;">
<div style="margin-bottom:10px;">🚗 <b>交通</b>：{同上格式}</div>
<div style="margin-bottom:10px;">🍜 <b>美食</b>：<br>
&nbsp;&nbsp;🥘 <b>{菜名}</b>（<b>{价格}</b>）：{特色描述}<br>
&nbsp;&nbsp;🍜 <b>{菜名}</b>（<b>{价格}</b>）：{特色描述}</div>
<div>⚠️ <b>避坑</b>：{同上格式}</div>
</td>
</tr>
</table>

<div style="background:#e8f5e9; border-radius:10px; padding:12px 16px; margin:16px 0; font-size:14px;">
💰 <b>DAY{N} 预算参考</b>：{项目1} <b>{X}元</b> + {项目2} <b>{X}元</b> + {项目3} <b>{X}元</b> ≈ <b>{总计}元/人</b>
</div>
```

> **景点卡片规则**：
> - 每个景点使用一个独立 `<table>` 卡片，包含标题行（彩色背景）+ 内容行（浅色背景）
> - 上午卡片用 **蓝色系**（`#2196f3`），下午用 **绿色系**（`#4caf50`），晚上用 **橙色系**（`#ff9800`）
> - 标题行 `border-radius:12px 12px 0 0`，内容行 `border-left:3px solid {颜色}` 左侧色条
> - 内容区各维度（交通/玩法/拍照/避坑）用 `margin-bottom:10px` 分段

### 第六章：美食打卡

```html
## 🍛 {目的地}美食打卡

![{目的地}美食](images/{目的地}美食.jpg)

<table style="width:100%; border-collapse:collapse; font-size:13px; color:#333; font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Roboto,'PingFang SC','Microsoft YaHei',sans-serif;">
<tr style="background:#f5f5f5; font-weight:500;">
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">美食名称</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">推荐指数</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">人均价格</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">特色描述</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">推荐店铺</th>
</tr>
<tr>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">🐟 <b>{美食1}</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8; color:#ffb800;">⭐⭐⭐⭐⭐</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{X}元</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8; line-height:1.7;">{口感/特色描述}</td>
<td style="padding:14px 16px;">{区域}·<b>{店铺名}</b></td>
</tr>
<tr style="background:#fafafa;">
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">🥟 <b>{美食2}</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8; color:#ffb800;">⭐⭐⭐⭐⭐</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{X}元</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8; line-height:1.7;">{口感/特色描述}</td>
<td style="padding:14px 16px;"><b>{街区}</b>、{位置}</td>
</tr>
<tr>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">🍜 <b>{美食3}</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8; color:#ffb800;">⭐⭐⭐⭐</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{X}元</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8; line-height:1.7;">{口感/特色描述}</td>
<td style="padding:14px 16px;">{区域}·<b>{店铺名}</b></td>
</tr>
<tr style="background:#fafafa;">
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">🥔 <b>{美食4}</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8; color:#ffb800;">⭐⭐⭐⭐⭐</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{X}元</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8; line-height:1.7;">{口感/特色描述}</td>
<td style="padding:14px 16px;"><b>{街区}</b>、{位置}</td>
</tr>
</table>

<div style="background:#fff3e0; border-left:4px solid #ff9800; padding:12px 16px; border-radius:0 8px 8px 0; margin:12px 0; font-size:14px;">
📍 <b>美食街区推荐</b>：<br>
🏆 <b>{街区1}</b>：{特色描述}<br>
🌃 <b>{街区2}</b>：{特色描述}<br>
🔥 <b>{街区3}</b>：{特色描述}
</div>
```

### 第七章：住宿指南

```html
## 🏨 {目的地}住宿指南

<table style="width:100%; border-collapse:separate; border-spacing:10px; font-size:14px;">
<tr>
<td style="background:#e3f2fd; border-radius:12px; padding:16px; vertical-align:top; width:50%;">
<div style="font-size:16px; font-weight:bold; margin-bottom:8px;">🌊 <b>{区域1}</b><br><span style="font-size:12px; color:#888;">（{子区域}）</span></div>
<div style="font-size:13px; line-height:1.8;">
✅ {优势1}<br>✅ {优势2}<br>✅ {优势3}<br>
<span style="color:#e53935;">❌ {劣势1}<br>❌ {劣势2}</span><br>
👥 {适合人群}<br>
💰 <b>{X}~{Y}元</b>/晚
</div>
</td>
<td style="background:#e8f5e9; border-radius:12px; padding:16px; vertical-align:top; width:50%;">
<div style="font-size:16px; font-weight:bold; margin-bottom:8px;">🏙️ <b>{区域2}</b> ⭐首推<br><span style="font-size:12px; color:#888;">（{子区域}）</span></div>
<div style="font-size:13px; line-height:1.8;">
✅ {优势1}<br>✅ {优势2}<br>
<span style="color:#e53935;">❌ {劣势1}<br>❌ {劣势2}</span><br>
👥 <b>{推荐人群}</b><br>
💰 <b>{X}~{Y}元</b>/晚
</div>
</td>
</tr>
</table>
```

### 第八章：交通指南

```html
## 🚄 {目的地}交通指南

### 🚗 自驾（如适用）
<table style="width:100%; border-collapse:collapse; font-size:13px; color:#333; font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Roboto,'PingFang SC','Microsoft YaHei',sans-serif;">
<tr style="background:#f5f5f5; font-weight:500;">
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">路线</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">距离</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">耗时</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">过路费</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">油费</th>
</tr>
<tr>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{路线1}</b>（主流）</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">约{X}km</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{X}h</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">约{X}元</td>
<td style="padding:14px 16px;">约{X}元</td>
</tr>
<tr style="background:#fafafa;">
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{路线2}</b>（⭐推荐）</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">约{X}km</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{X}h</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">约{X}元</td>
<td style="padding:14px 16px;">约{X}元</td>
</tr>
</table>

### ✈️ 飞机 / 🚄 高铁 / 🚇 市内交通
{使用列表格式，关键数据<b>加粗</b>}
```

### 第九章：拍照出片点

```html
## 📷 {目的地}拍照出片点

<table style="width:100%; border-collapse:collapse; font-size:13px; color:#333; font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Roboto,'PingFang SC','Microsoft YaHei',sans-serif;">
<tr style="background:#f5f5f5; font-weight:500;">
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">序号</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">拍摄地点</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">最佳时间</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">拍摄建议</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">出片风格</th>
</tr>
<tr>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">1</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{地点1}</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">{时间}</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8; line-height:1.7;">{建议}</td>
<td style="padding:14px 16px;">🏔️ {风格}</td>
</tr>
<tr style="background:#fafafa;">
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">2</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{地点2}</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">{时间}</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8; line-height:1.7;">{建议}</td>
<td style="padding:14px 16px;">🌅 {风格}</td>
</tr>
<tr>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">3</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{地点3}</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">{时间}</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8; line-height:1.7;">{建议}</td>
<td style="padding:14px 16px;">🌊 {风格}</td>
</tr>
</table>
```

### 第十章：需要预约的景点

```html
## 🎫 需要预约的景点

<table style="width:100%; border-collapse:collapse; font-size:13px; color:#333; font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Roboto,'PingFang SC','Microsoft YaHei',sans-serif;">
<tr style="background:#f5f5f5; font-weight:500;">
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">景点名称</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">门票价格</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">开放时间</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">预约方式</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">预约难度</th>
</tr>
<tr>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{景点1}</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">🔴 <b>免费</b>（交通{X}元）</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{时间}</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">"{公众号}"</td>
<td style="padding:14px 16px;">⭐⭐</td>
</tr>
<tr style="background:#fafafa;">
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{景点2}</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{X}元</b>（含船）</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{时间}</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">"{公众号}"</td>
<td style="padding:14px 16px;">⭐⭐⭐</td>
</tr>
<tr>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{景点3}</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{X}元</b>（A线含船）</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{时间}</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">"{公众号}"</td>
<td style="padding:14px 16px;">⭐⭐⭐</td>
</tr>
</table>
```

### 第十一章：实用Tips（⭐大色块包裹）

```html
## 📌 {目的地}游玩实用Tips

> ▼ {N}条实用建议，出发前必看！

<table style="width:100%; border-collapse:separate; border-spacing:10px; font-size:14px;">
<tr>
<td style="background:#e3f2fd; border-radius:12px; padding:16px; vertical-align:top; width:50%;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🚗 1. 自驾路线选择</div>
<div style="font-size:13px; line-height:1.8;">
去程走<b>G348三峡公路</b>（风景绝美），回程走<b>G50沪渝高速</b>（快速便捷）。G348弯道多，新手司机注意安全。
</div>
</td>
<td style="background:#fce4ec; border-radius:12px; padding:16px; vertical-align:top; width:50%;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🏗️ 2. 三峡大坝攻略</div>
<div style="font-size:13px; line-height:1.8;">
🔴 <b>免费但必须预约！</b>刷身份证入园。景区内电瓶车<b>10元</b>，建议加购游船票。
</div>
</td>
</tr>
<tr>
<td style="background:#fff8e1; border-radius:12px; padding:16px; vertical-align:top; width:50%;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🌤️ 3. 清江画廊看天气</div>
<div style="font-size:13px; line-height:1.8;">
🔴 <b>一定要晴天去！</b>阴雨天风景大打折扣。出发前查好天气预报。
</div>
</td>
<td style="background:#e8f5e9; border-radius:12px; padding:16px; vertical-align:top; width:50%;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🏨 4. 住宿选择</div>
<div style="font-size:13px; line-height:1.8;">
推荐住<b>市中心/沿江大道</b>附近，吃喝玩乐方便。预算充足选<b>江景房</b>。
</div>
</td>
</tr>
<tr>
<td style="background:#f3e5f5; border-radius:12px; padding:16px; vertical-align:top; width:50%;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🅿️ 5. 停车信息</div>
<div style="font-size:13px; line-height:1.8;">
景区停车场<b>10元/次</b>，市区路边<b>3~5元/小时</b>。
</div>
</td>
<td style="background:#ffebee; border-radius:12px; padding:16px; vertical-align:top; width:50%;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🍜 6. 吃饭防坑</div>
<div style="font-size:13px; line-height:1.8;">
🔴 <b>别在景区内吃饭！</b>又贵又一般。回市区或县城吃。
</div>
</td>
</tr>
<tr>
<td style="background:#e0f7fa; border-radius:12px; padding:16px; vertical-align:top; width:50%;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">💰 7. 省钱技巧</div>
<div style="font-size:13px; line-height:1.8;">
学生证<b>半价</b>；旅游年卡<b>100元/年</b>；高速ETC打折。
</div>
</td>
<td style="background:#efebe9; border-radius:12px; padding:16px; vertical-align:top; width:50%;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">📞 8. 应急信息</div>
<div style="font-size:13px; line-height:1.8;">
市中心医院：<b>0717-6223999</b><br>
高速救援：<b>12122</b>
</div>
</td>
</tr>
</table>
```

> **Tips 色块规则**：
> - 使用 2 列 × N 行的卡片网格布局（`border-spacing:10px`）
> - 每个色块使用不同浅色背景（蓝/粉/黄/绿/紫/红/青/棕），`border-radius:12px` 圆角
> - 标题 `font-size:15px; font-weight:bold`，内容 `font-size:13px; line-height:1.8`
> - 警示类 Tips 使用红色系背景（`#ffebee`），普通 Tips 使用其他颜色

### 第十二章：朋友圈文案

```html
## 📱 {目的地}朋友圈文案

> ▼ {N}条精选文案，发朋友圈直接复制！

<table style="width:100%; border-collapse:separate; border-spacing:8px; font-size:14px;">
<tr>
<td style="background:#fce4ec; border-radius:10px; padding:12px 16px; width:50%;">1. ✅ 打卡📍{目的地} {日期}</td>
<td style="background:#e3f2fd; border-radius:10px; padding:12px 16px; width:50%;">2. {文艺风格文案}</td>
</tr>
<tr>
<td style="background:#e8f5e9; border-radius:10px; padding:12px 16px; width:50%;">3. {幽默风格文案}</td>
<td style="background:#fff8e1; border-radius:10px; padding:12px 16px; width:50%;">4. {古风/文艺文案}</td>
</tr>
</table>
```

### 第十三章：费用预算

```html
## 💰 费用预算参考（人均）

<table style="width:100%; border-collapse:collapse; font-size:13px; color:#333; font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Roboto,'PingFang SC','Microsoft YaHei',sans-serif;">
<tr style="background:#f5f5f5; font-weight:500;">
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">项目</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">预算（元）</th>
<th style="padding:14px 16px; text-align:left; border-bottom:1px solid #e8e8e8;">备注</th>
</tr>
<tr>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">🚄 大交通</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{X}</b></td>
<td style="padding:14px 16px;">{出发地}→{目的地}往返</td>
</tr>
<tr style="background:#fafafa;">
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">🏨 住宿</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{X}</b></td>
<td style="padding:14px 16px;">{N}晚，{X}元/晚</td>
</tr>
<tr>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">🎫 门票</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{X}</b></td>
<td style="padding:14px 16px;">主要景点合计</td>
</tr>
<tr style="background:#fafafa;">
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">🍜 餐饮</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{X}</b></td>
<td style="padding:14px 16px;">{N}天，{X}元/天</td>
</tr>
<tr>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">🚇 市内交通</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{X}</b></td>
<td style="padding:14px 16px;">地铁+打车</td>
</tr>
<tr style="background:#fafafa;">
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">🛍️ 购物/其他</td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>{X}</b></td>
<td style="padding:14px 16px;">纪念品、特产等</td>
</tr>
<tr style="background:#f0f0f0; font-weight:bold;">
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;">💰 <b>合计</b></td>
<td style="padding:14px 16px; border-right:1px solid #e8e8e8;"><b>≈ {X}</b></td>
<td style="padding:14px 16px;"></td>
</tr>
</table>

<div style="background:#e8f5e9; border-left:4px solid #43a047; padding:12px 16px; border-radius:0 8px 8px 0; margin:12px 0; font-size:14px;">
💡 <b>省钱版</b>（约<b>{X}元/人</b>）：{省钱方案}<br>
💡 <b>品质版</b>（约<b>{X}元/人</b>）：{品质方案}<br>
⚠️ 以上为参考预算，实际花费因个人消费习惯而异。
</div>
```

### 结尾

```html
<hr style="border:none; border-top:2px solid #eee; margin:30px 0;">

<div align="center" style="font-size:14px;">

> 📌 <b>写在最后</b>：{一段温暖的结语，总结目的地特色和旅行感受}

</div>

</div>
```

> ⚠️ **重要**：文档最末尾的 `</div>` 用于闭合开头 `<div style="font-size:14px;">` 的全局样式容器。

---

## 内容生成规则

### 1. 信息准确性
- **必须通过网络搜索**获取目的地的最新信息（景点开放时间、门票价格、交通路线等）
- 价格信息需标注"仅供参考，以实际为准"
- 预约信息需注明预约渠道和时间节点

### 2. 行程合理性
- 每日行程安排需考虑**地理位置邻近性**，减少不必要的往返
- 时间安排需合理，考虑交通衔接和游览时间
- 每天安排 3-5 个景点/活动为宜，避免过于紧凑
- 需考虑用餐时间（早餐 7:00-9:00，午餐 11:30-13:30，晚餐 17:30-19:30）

### 3. 风格适配
根据用户选择的旅行风格调整内容：
- **轻松版**：每天不超3个景点，10:00后出发，留足休息时间
- **特种兵版**：紧凑安排，早起晚归，最大化游览数量
- **亲子版**：增加适合儿童的景点，降低步行强度，增加休息频次
- **美食版**：以美食为主线串联行程，增加美食街区和小吃摊位
- **穷游版**：优先免费/低价景点，推荐平价美食和住宿

### 4. 排版规范（⭐重点·v1.3 卡片+斑马纹版）

#### 4.1 全局字体
- 文档最开头使用 `<div style="font-size:14px; line-height:1.8; color:#333;">` 包裹全文
- 文档最末尾用 `</div>` 闭合
- 所有正文内容统一 **14px** 字体，行高 **1.8**

#### 4.2 数据表格统一样式（⭐斑马条纹）

所有数据展示类表格（天气、美食、交通、拍照、预约、预算）必须使用统一的斑马条纹样式：

```css
/* 表格基础样式 */
font-size: 13px;
color: #333;
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'PingFang SC', 'Microsoft YaHei', sans-serif;
border-collapse: collapse;

/* 表头 */
background: #f5f5f5;
font-weight: 500;
padding: 14px 16px;
text-align: left;
border-bottom: 1px solid #e8e8e8;

/* 数据行 - 斑马条纹 */
奇数行：background: #ffffff;  /* 白色 */
偶数行：background: #fafafa;  /* 极浅灰 */

/* 单元格 */
padding: 14px 16px;
border-right: 1px solid #e8e8e8;  /* 列分隔线（最后一列不加） */
line-height: 1.7;  /* 长文本列 */
vertical-align: middle;

/* 合计行 */
background: #f0f0f0;
font-weight: bold;

/* 星级评分颜色 */
color: #ffb800;  /* 金黄色 */
```

> **表格样式要点**：
> - ❌ 不使用彩色表头（如蓝/红/紫/绿背景+白字）
> - ❌ 不使用圆角（`border-radius: 0`）
> - ✅ 表头统一浅灰 `#f5f5f5`，`font-weight: 500`
> - ✅ 斑马条纹：奇数白 `#fff`，偶数浅灰 `#fafafa`
> - ✅ 列分隔线 `#e8e8e8`，表头底部线 `#e8e8e8`
> - ✅ 全部左对齐（包括数字列）
> - ✅ 内边距 `14px 16px`，字号 `13px`
> - ✅ 系统字体栈（PingFang SC / Microsoft YaHei）

#### 4.3 卡片布局体系

| 卡片类型 | 使用场景 | 布局方式 | 背景色系 |
|:---|:---|:---|:---|
| **准备清单卡片** | 出发前物品 | 4列网格（第一行）+ 2~3列（第二行） | 蓝/绿/橙/紫/黄/灰 |
| **行程总览卡片** | 每日行程概览 | 3列等宽网格 | 绿/蓝/粉 |
| **景点详情卡片** | 每个景点/活动 | 全宽卡片（标题行+内容行） | 上午蓝/下午绿/晚上橙 |
| **住宿对比卡片** | 住宿区域推荐 | 2列网格 | 蓝/绿 |
| **Tips 色块** | 实用建议 | 2列 × N行网格 | 多色系轮换 |
| **文案卡片** | 朋友圈文案 | 2列网格 | 粉/蓝/绿/黄轮换 |

#### 4.4 卡片 CSS 规范

```css
/* 通用卡片样式 */
border-radius: 12px;          /* 圆角 */
padding: 16px;                /* 内边距 */
border-collapse: separate;    /* 表格分离模式 */
border-spacing: 10px~12px;    /* 卡片间距 */

/* 卡片内标题 */
font-size: 16px;
font-weight: bold;
margin-bottom: 8px~10px;

/* 卡片内正文 */
font-size: 13px;
line-height: 1.8~2;

/* 左侧色条（景点卡片内容行） */
border-left: 3px solid {主题色};
```

#### 4.5 高亮标注体系

| 标注类型 | 格式 | 使用场景 | 示例 |
|:---|:---|:---|:---|
| **关键数据** | `<b>{内容}</b>` | 价格、时间、距离、电话 | <b>35元/人</b> |
| **警示信息** | `🔴 <b>{内容}</b>` | 必须注意的严重警告 | 🔴 <b>免费但必须预约！</b> |
| **推荐标记** | `⭐` | 首推选项 | ⭐ 首推区域 |

> ⚠️ **注意**：在 HTML 卡片内部，使用 `<b>` 标签而非 Markdown `**` 进行加粗。

#### 4.6 色块提示框样式

用于温馨提示、美食推荐、预约提醒等场景：

```html
<!-- 黄色提示框 -->
<div style="background:#fff8e1; border-left:4px solid #ffc107; padding:12px 16px; border-radius:0 8px 8px 0; margin:12px 0; font-size:14px;">
💡 <b>温馨提示</b>：{内容}
</div>

<!-- 绿色预算框 -->
<div style="background:#e8f5e9; border-left:4px solid #43a047; padding:12px 16px; border-radius:0 8px 8px 0; margin:12px 0; font-size:14px">
💰 <b>预算参考</b>：{内容}
</div>

<!-- 橙色美食框 -->
<div style="background:#fff3e0; border-left:4px solid #ff9800; padding:12px 16px; border-radius:0 8px 8px 0; margin:12px 0; font-size:14px;">
📍 <b>美食街区</b>：{内容}
</div>
```

### 5. 图片处理（⭐重点）

#### 5.1 图片来源规则
- **禁止使用 AI 生成图片**（AI 生成图片不够真实自然）
- **必须通过网络搜索获取真实照片**：使用 WebSearch 搜索景点/美食的实拍照片
- 优先选择以下来源的高质量图片：
  - 官方旅游网站、政府文旅网站
  - 知名旅游平台（携程、马蜂窝、飞猪等）
  - 新闻媒体报道配图
  - 专业摄影网站（图虫等）
- 图片搜索关键词格式：`"{景点名} 高清 实拍 摄影高清"` 或 `"{美食名} {城市} 美食 高清"`

#### 5.2 图片下载与保存
- 使用 `curl` 或 `wget` 下载图片
- 图片保存至与攻略文档同目录的 `images/` 文件夹
- 图片统一使用 `.jpg` 格式
- 文件命名使用中文：`{景点/美食名称}.jpg`

#### 5.3 图片引用规范
- 在 Markdown 中使用相对路径引用：`![{描述}](images/{文件名}.jpg)`
- 每个主要景点配 **1张** 真实照片，放置在该景点卡片之前
- 美食打卡章节配 **1~2张** 美食实拍照片
- 封面配 **1张** 目的地标志性全景照片
- 总计约 **8~12张**

### 6. 语言风格
- 采用**友好、实用、接地气**的写作风格
- 适当使用口语化表达和网络用语
- 避坑提示使用明确警示语气（配合 🔴 标记）
- 美食描述突出口感和特色
- 价格使用具体数字，避免模糊表述

## 工作流程

当用户请求生成旅行攻略时，按以下步骤执行：

1. **确认需求**：明确目的地、天数、出行时间、旅行风格等参数
2. **信息搜集**：通过网络搜索收集目的地最新信息（控制在 3~5 次搜索内）
   - 搜索目的地热门景点、美食、住宿、交通信息
   - 搜索天气情况和季节性建议
   - 搜索最新门票价格和预约政策
3. **图片搜集**：通过网络搜索下载真实照片（与信息搜集可并行）
   - 搜索并下载目的地封面图
   - 搜索并下载各核心景点实拍图
   - 搜索并下载美食实拍图
4. **行程规划**：根据搜集的信息规划合理行程
   - 按地理位置分组景点
   - 安排每日动线和时间节点
   - 穿插餐饮和休息时间
5. **内容生成**：按模板结构生成完整攻略文档
   - ⚠️ 必须以 `<div style="font-size:14px;">` 开头
   - 严格遵循 HTML 卡片布局模板
   - 景点卡片按时段使用对应色系（蓝/绿/橙）
   - Tips 使用 2 列彩色色块网格
   - 文档末尾用 `</div>` 闭合
6. **文档输出**：将最终 Markdown 文档和 images 文件夹保存到用户工作区

## 示例调用

**用户输入**：
> 帮我生成一份西安4天3晚的旅行攻略，五一假期去，轻松版，两个人从北京出发

**输出**：
生成一份完整的 `西安4天3晚旅行攻略（五一轻松版）.md` 文件，包含上述所有章节，使用 HTML 卡片布局和色块样式，附带 8~12 张网络搜索的真实照片，保存至 `images/` 文件夹。
