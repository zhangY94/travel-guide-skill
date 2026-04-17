---
name: travel-guide
description: 旅行攻略生成技能 - 根据用户指定的目的地、天数、出行时间和旅行风格，自动生成结构完整、信息详实的旅行攻略 Markdown 文档。输出包含：准备清单、天气参考、行程总览、每日详细行程（含交通/玩法/拍照/避坑）、美食打卡、住宿指南、交通指南、拍照出片点、实用Tips和朋友圈文案等模块。支持多种旅行风格（轻松版/特种兵版/亲子版/美食版/穷游版等）。
version: "1.4.0"
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

本技能用于根据用户输入的目的地、天数、出行时间和旅行风格，自动生成一份**结构完整、信息详实、排版精美**的旅行攻略 Markdown 文档。生成的攻略文档参考小红书/飞书文档风格的旅行攻略模板，使用 HTML Flexbox 卡片布局实现视觉效果，包含行程规划、美食推荐、住宿指南、交通指南、拍照攻略、实用Tips等全方位信息。

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

输出为 **Markdown (.md)** 格式的旅行攻略文档，严格遵循以下模板结构和排版规范。

---

## 📋 攻略文档模板结构

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

<div style="display:flex; flex-wrap:wrap; justify-content:center; gap:10px; margin:20px 0;">
<div style="flex:1; min-width:100px; max-width:150px; background:#f5f5f5; border-radius:8px; padding:12px; text-align:center;">📅 出行时间<br><b>{具体日期/季节}</b></div>
<div style="flex:1; min-width:100px; max-width:150px; background:#f5f5f5; border-radius:8px; padding:12px; text-align:center;">👥 出行人群<br>{人群描述}</div>
<div style="flex:1; min-width:100px; max-width:150px; background:#f5f5f5; border-radius:8px; padding:12px; text-align:center;">🚗 出行方式<br><b>{交通方式}</b></div>
<div style="flex:1; min-width:100px; max-width:150px; background:#f5f5f5; border-radius:8px; padding:12px; text-align:center;">💰 人均预算<br><b>{预算范围}</b></div>
<div style="flex:1; min-width:100px; max-width:150px; background:#f5f5f5; border-radius:8px; padding:12px; text-align:center;">✈️ 出发城市<br><b>{出发地}</b></div>
</div>
```

### 第二章：准备清单（⭐卡片网格）

```html
## 📦 出发前准备清单

> ▼ {一句话提示，如"这些物品一个都不能少！"}

<div style="display:flex; flex-wrap:wrap; gap:12px;">
<div style="flex:1; min-width:200px; background:#f0f7ff; border-radius:12px; padding:16px;">
<div style="font-size:16px; font-weight:bold; margin-bottom:10px;">🪪 证件类</div>
<div style="font-size:13px; line-height:2;">
☐ 身份证（<b>必备</b>）<br>
☐ 学生证（景点<b>半价</b>）<br>
☐ 驾驶证（自驾必备）<br>
☐ 护照/签证（出境游）
</div>
</div>
<div style="flex:1; min-width:200px; background:#f5fff0; border-radius:12px; padding:16px;">
<div style="font-size:16px; font-weight:bold; margin-bottom:10px;">📱 电子设备</div>
<div style="font-size:13px; line-height:2;">
☐ 手机 + 充电器<br>
☐ 充电宝（<b>必备</b>）<br>
☐ 耳机<br>
☐ 相机/自拍杆
</div>
</div>
<div style="flex:1; min-width:200px; background:#fff5f0; border-radius:12px; padding:16px;">
<div style="font-size:16px; font-weight:bold; margin-bottom:10px;">👗 穿搭准备</div>
<div style="font-size:13px; line-height:2;">
☐ 舒适运动鞋<br>
☐ {季节衣物}（<b>温差大</b>）<br>
☐ 墨镜/防晒衣<br>
☐ {特色服饰}
</div>
</div>
<div style="flex:1; min-width:200px; background:#fef5ff; border-radius:12px; padding:16px;">
<div style="font-size:16px; font-weight:bold; margin-bottom:10px;">🧴 洗漱护肤</div>
<div style="font-size:13px; line-height:2;">
☐ 防晒霜（<b>SPF50+</b>）<br>
☐ 保湿面膜/润唇膏<br>
☐ 晴雨伞<br>
☐ 湿巾/纸巾
</div>
</div>
<div style="flex:1; min-width:200px; background:#fff8e6; border-radius:12px; padding:16px;">
<div style="font-size:16px; font-weight:bold; margin-bottom:10px;">💊 应急物品</div>
<div style="font-size:13px; line-height:2;">
☐ 肠胃药/感冒药<br>
☐ 创可贴<br>
☐ 晕船药（<b>坐船必带</b>）<br>
☐ 防蚊液
</div>
</div>
<div style="flex:2; min-width:300px; background:#f0f4ff; border-radius:12px; padding:16px;">
<div style="font-size:16px; font-weight:bold; margin-bottom:10px;">🚗 车辆检查（自驾适用）</div>
<div style="font-size:13px; line-height:2;">
☐ 检查轮胎气压 &nbsp;&nbsp; ☐ 检查机油/冷却液 &nbsp;&nbsp; ☐ <b>加满油</b> &nbsp;&nbsp; ☐ 备好ETC卡
</div>
</div>
</div>
```

> **卡片网格规则**：使用 `display:flex; flex-wrap:wrap; gap:12px`，每个卡片 `flex:1; min-width:200px`，屏幕窄时自动换行。

### 第三章：天气参考

```html
## 🌤️ {目的地}天气参考（{季节}）

<div style="display:flex; flex-wrap:wrap; gap:10px;">
<div style="flex:1; min-width:150px; background:#f5f5f5; border-radius:10px; padding:14px 16px;">
<div style="font-size:15px; font-weight:bold; margin-bottom:6px;">📅 <b>Day1</b></div>
<div style="font-size:13px; color:#666;">{天气emoji} {天气}</div>
<div style="font-size:13px; margin-top:4px;"><b>{温度范围}℃</b></div>
<div style="font-size:12px; color:#888; margin-top:4px;">{穿衣建议}</div>
</div>
<div style="flex:1; min-width:150px; background:#ffffff; border-radius:10px; padding:14px 16px;">
<div style="font-size:15px; font-weight:bold; margin-bottom:6px;">📅 <b>Day2</b></div>
<div style="font-size:13px; color:#666;">{天气emoji} {天气}</div>
<div style="font-size:13px; margin-top:4px;"><b>{温度范围}℃</b></div>
<div style="font-size:12px; color:#888; margin-top:4px;">{穿衣建议}</div>
</div>
<div style="flex:1; min-width:150px; background:#f5f5f5; border-radius:10px; padding:14px 16px;">
<div style="font-size:15px; font-weight:bold; margin-bottom:6px;">📅 <b>Day3</b></div>
<div style="font-size:13px; color:#666;">{天气emoji} {天气}</div>
<div style="font-size:13px; margin-top:4px;"><b>{温度范围}℃</b></div>
<div style="font-size:12px; color:#888; margin-top:4px;">{穿衣建议}</div>
</div>
</div>

<div style="background:#fff8e1; border-left:4px solid #ffc107; padding:12px 16px; border-radius:0 8px 8px 0; margin:12px 0; font-size:14px;">
💡 <b>温馨提示</b>：{季节性穿衣建议，关键数据<b>加粗</b>}
</div>
```

### 第四章：行程总览

```html
## 🗺️ 行程总览

> ▼ {一句话概括行程特色}

<div style="display:flex; flex-wrap:wrap; gap:12px;">
<div style="flex:1; min-width:250px; background:#e8f5e9; border-radius:12px; padding:16px;">
<div style="font-size:18px; margin-bottom:8px;">🏃 <b>DAY1</b></div>
<div style="font-size:13px; color:#666; margin-bottom:6px;">🛣️ {当日主题}</div>
<div style="font-size:13px;">{景点A} → <b>{核心景点}</b> → {景点C}</div>
</div>
<div style="flex:1; min-width:250px; background:#e3f2fd; border-radius:12px; padding:16px;">
<div style="font-size:18px; margin-bottom:8px;">🏃 <b>DAY2</b></div>
<div style="font-size:13px; color:#666; margin-bottom:6px;">🏞️ {当日主题}</div>
<div style="font-size:13px;"><b>{核心景点}</b> → {景点F} → {景点G}</div>
</div>
<div style="flex:1; min-width:250px; background:#fce4ec; border-radius:12px; padding:16px;">
<div style="font-size:18px; margin-bottom:8px;">🏃 <b>DAY3</b></div>
<div style="font-size:13px; color:#666; margin-bottom:6px;">🌊 {当日主题}</div>
<div style="font-size:13px;"><b>{核心景点}</b> → {景点J} → 返程</div>
</div>
</div>
```

### 第五章：每日详细行程（⭐核心章节·卡片样式）

```html
<hr style="border:none; border-top:2px solid #eee; margin:30px 0;">

## 🔻 DAY{N}：{景点A} → {景点B} → {景点C} → {景点D}

> 📍 当日主题：{一句话描述当日特色}

### ✅ 景点游玩建议

#### ① 上午游玩建议（{景点组合}，建议安排 <b>{X}h</b>）

![{景点名称}](images/{景点名称}.jpg)

<div style="background:#e3f2fd; border-radius:12px 12px 0 0; padding:14px 18px; border-bottom:2px solid #2196f3;">
<div style="font-size:16px; font-weight:bold;">☐ {景点名称1}</div>
</div>
<div style="background:#f5f9ff; padding:16px 18px; border-left:3px solid #2196f3; border-radius:0 0 12px 12px; margin-bottom:16px;">
<div style="margin-bottom:10px;">🚗 <b>交通</b>：{交通方式}，约<b>{X}km / {X}h</b>。{具体路线}</div>
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
</div>

#### ② 下午游玩建议（{景点名称}，建议安排 <b>{X}h</b>）

<div style="background:#e8f5e9; border-radius:12px 12px 0 0; padding:14px 18px; border-bottom:2px solid #4caf50;">
<div style="font-size:16px; font-weight:bold;">☐ {景点名称2}</div>
</div>
<div style="background:#f5fff5; padding:16px 18px; border-left:3px solid #4caf50; border-radius:0 0 12px 12px; margin-bottom:16px;">
{同上格式：交通/玩法/拍照/避坑}
</div>

#### ③ 晚上游玩建议（{活动/景点}，建议安排 <b>{X}h</b>）

<div style="background:#fff3e0; border-radius:12px 12px 0 0; padding:14px 18px; border-bottom:2px solid #ff9800;">
<div style="font-size:16px; font-weight:bold;">☐ {活动/景点名称}</div>
</div>
<div style="background:#fffbf5; padding:16px 18px; border-left:3px solid #ff9800; border-radius:0 0 12px 12px; margin-bottom:16px;">
<div style="margin-bottom:10px;">🚗 <b>交通</b>：{同上格式}</div>
<div style="margin-bottom:10px;">🍜 <b>美食</b>：<br>
&nbsp;&nbsp;🥘 <b>{菜名}</b>（<b>{价格}</b>）：{特色描述}<br>
&nbsp;&nbsp;🍜 <b>{菜名}</b>（<b>{价格}</b>）：{特色描述}</div>
<div>⚠️ <b>避坑</b>：{同上格式}</div>
</div>

<div style="background:#e8f5e9; border-radius:10px; padding:12px 16px; margin:16px 0; font-size:14px;">
💰 <b>DAY{N} 预算参考</b>：{项目1} <b>{X}元</b> + {项目2} <b>{X}元</b> + {项目3} <b>{X}元</b> ≈ <b>{总计}元/人</b>
</div>
```

> **景点卡片规则**：每个景点用两个 `<div>` 组合（标题栏 + 内容栏），上午🔵蓝、下午🟢绿、晚上🟠橙。

### 第六章：美食打卡

```html
## 🍛 {目的地}美食打卡

![{目的地}美食](images/{目的地}美食.jpg)

<div style="display:flex; flex-wrap:wrap; gap:12px;">
<div style="flex:1; min-width:280px; background:#ffffff; border-radius:12px; padding:16px; border-left:4px solid #ffb800;">
<div style="font-size:15px; font-weight:bold; margin-bottom:6px;">🐟 <b>{美食1}</b></div>
<div style="font-size:12px; color:#ffb800; margin-bottom:6px;">⭐⭐⭐⭐⭐</div>
<div style="font-size:13px; color:#666; margin-bottom:4px;">💰 人均：<b>{X}元</b></div>
<div style="font-size:13px; margin-bottom:6px;">{口感/特色描述}</div>
<div style="font-size:12px; color:#888;">📍 {区域}·<b>{店铺名}</b></div>
</div>
<div style="flex:1; min-width:280px; background:#fafafa; border-radius:12px; padding:16px; border-left:4px solid #ffb800;">
<div style="font-size:15px; font-weight:bold; margin-bottom:6px;">🥟 <b>{美食2}</b></div>
<div style="font-size:12px; color:#ffb800; margin-bottom:6px;">⭐⭐⭐⭐⭐</div>
<div style="font-size:13px; color:#666; margin-bottom:4px;">💰 人均：<b>{X}元</b></div>
<div style="font-size:13px; margin-bottom:6px;">{口感/特色描述}</div>
<div style="font-size:12px; color:#888;">📍 <b>{街区}</b>、{位置}</div>
</div>
<div style="flex:1; min-width:280px; background:#ffffff; border-radius:12px; padding:16px; border-left:4px solid #ffb800;">
<div style="font-size:15px; font-weight:bold; margin-bottom:6px;">🍜 <b>{美食3}</b></div>
<div style="font-size:12px; color:#ffb800; margin-bottom:6px;">⭐⭐⭐⭐</div>
<div style="font-size:13px; color:#666; margin-bottom:4px;">💰 人均：<b>{X}元</b></div>
<div style="font-size:13px; margin-bottom:6px;">{口感/特色描述}</div>
<div style="font-size:12px; color:#888;">📍 {区域}·<b>{店铺名}</b></div>
</div>
<div style="flex:1; min-width:280px; background:#fafafa; border-radius:12px; padding:16px; border-left:4px solid #ffb800;">
<div style="font-size:15px; font-weight:bold; margin-bottom:6px;">🥔 <b>{美食4}</b></div>
<div style="font-size:12px; color:#ffb800; margin-bottom:6px;">⭐⭐⭐⭐⭐</div>
<div style="font-size:13px; color:#666; margin-bottom:4px;">💰 人均：<b>{X}元</b></div>
<div style="font-size:13px; margin-bottom:6px;">{口感/特色描述}</div>
<div style="font-size:12px; color:#888;">📍 <b>{街区}</b>、{位置}</div>
</div>
</div>

<div style="background:#fff3e0; border-left:4px solid #ff9800; padding:12px 16px; border-radius:0 8px 8px 0; margin:12px 0; font-size:14px;">
📍 <b>美食街区推荐</b>：<br>
🏆 <b>{街区1}</b>：{特色描述}<br>
🌃 <b>{街区2}</b>：{特色描述}<br>
🔥 <b>{街区3}</b>：{特色描述}
</div>
```

> **美食卡片规则**：`flex:1; min-width:280px`，每行2~3个，交替白/浅灰背景，左侧金色色条 `#ffb800`。

### 第七章：住宿指南

```html
## 🏨 {目的地}住宿指南

<div style="display:flex; flex-wrap:wrap; gap:12px;">
<div style="flex:1; min-width:280px; background:#e3f2fd; border-radius:12px; padding:16px;">
<div style="font-size:16px; font-weight:bold; margin-bottom:8px;">🌊 <b>{区域1}</b><br><span style="font-size:12px; color:#888;">（{子区域}）</span></div>
<div style="font-size:13px; line-height:1.8;">
✅ {优势1}<br>✅ {优势2}<br>✅ {优势3}<br>
<span style="color:#e53935;">❌ {劣势1}<br>❌ {劣势2}</span><br>
👥 {适合人群}<br>
💰 <b>{X}~{Y}元</b>/晚
</div>
</div>
<div style="flex:1; min-width:280px; background:#e8f5e9; border-radius:12px; padding:16px;">
<div style="font-size:16px; font-weight:bold; margin-bottom:8px;">🏙️ <b>{区域2}</b> ⭐首推<br><span style="font-size:12px; color:#888;">（{子区域}）</span></div>
<div style="font-size:13px; line-height:1.8;">
✅ {优势1}<br>✅ {优势2}<br>
<span style="color:#e53935;">❌ {劣势1}<br>❌ {劣势2}</span><br>
👥 <b>{推荐人群}</b><br>
💰 <b>{X}~{Y}元</b>/晚
</div>
</div>
<div style="flex:1; min-width:280px; background:#fce4ec; border-radius:12px; padding:16px;">
<div style="font-size:16px; font-weight:bold; margin-bottom:8px;">🏝️ <b>{区域3}</b><br><span style="font-size:12px; color:#888;">（{子区域}）</span></div>
<div style="font-size:13px; line-height:1.8;">
✅ {优势1}<br>✅ {优势2}<br>
<span style="color:#e53935;">❌ {劣势1}</span><br>
👥 {适合人群}<br>
💰 <b>{X}~{Y}元</b>/晚
</div>
</div>
<div style="flex:1; min-width:280px; background:#f3e5f5; border-radius:12px; padding:16px;">
<div style="font-size:16px; font-weight:bold; margin-bottom:8px;">🏞️ <b>{区域4}</b><br><span style="font-size:12px; color:#888;">（{子区域}）</span></div>
<div style="font-size:13px; line-height:1.8;">
✅ {优势1}<br>
<span style="color:#e53935;">❌ {劣势1}<br>❌ {劣势2}</span><br>
👥 {适合人群}<br>
💰 <b>{X}~{Y}元</b>/晚
</div>
</div>
</div>
```

### 第八章：交通指南

```html
## 🚄 {目的地}交通指南

### 🚗 自驾（如适用）

<div style="display:flex; flex-wrap:wrap; gap:12px;">
<div style="flex:1; min-width:280px; background:#f5f5f5; border-radius:12px; padding:16px;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🛣️ <b>{路线1}</b>（主流）</div>
<div style="font-size:13px; line-height:2;">
📏 距离：<b>约{X}km</b><br>
⏱️ 耗时：<b>{X}h</b><br>
🎫 过路费：约{X}元<br>
⛽ 油费：约{X}元
</div>
</div>
<div style="flex:1; min-width:280px; background:#e8f0fe; border-radius:12px; padding:16px; border-left:4px solid #4285f4;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🛣️ <b>{路线2}</b> ⭐推荐</div>
<div style="font-size:13px; line-height:2;">
📏 距离：<b>约{X}km</b><br>
⏱️ 耗时：<b>{X}h</b><br>
🎫 过路费：约{X}元<br>
⛽ 油费：约{X}元
</div>
</div>
</div>

### ✈️ 飞机 / 🚄 高铁 / 🚇 市内交通
{使用列表格式，关键数据<b>加粗</b>}
```

### 第九章：拍照出片点

```html
## 📷 {目的地}拍照出片点

<div style="display:flex; flex-wrap:wrap; gap:12px;">
<div style="flex:1; min-width:220px; background:#ffffff; border-radius:12px; padding:14px 16px;">
<div style="font-size:14px; font-weight:bold; margin-bottom:6px;">1️⃣ <b>{地点1}</b></div>
<div style="font-size:12px; color:#666; margin-bottom:4px;">🕐 {最佳时间}</div>
<div style="font-size:13px; margin-bottom:4px;">📷 {拍摄建议}</div>
<div style="font-size:12px; color:#888;">🏔️ {出片风格}</div>
</div>
<div style="flex:1; min-width:220px; background:#fafafa; border-radius:12px; padding:14px 16px;">
<div style="font-size:14px; font-weight:bold; margin-bottom:6px;">2️⃣ <b>{地点2}</b></div>
<div style="font-size:12px; color:#666; margin-bottom:4px;">🕐 {最佳时间}</div>
<div style="font-size:13px; margin-bottom:4px;">📷 {拍摄建议}</div>
<div style="font-size:12px; color:#888;">🌅 {出片风格}</div>
</div>
<div style="flex:1; min-width:220px; background:#ffffff; border-radius:12px; padding:14px 16px;">
<div style="font-size:14px; font-weight:bold; margin-bottom:6px;">3️⃣ <b>{地点3}</b></div>
<div style="font-size:12px; color:#666; margin-bottom:4px;">🕐 {最佳时间}</div>
<div style="font-size:13px; margin-bottom:4px;">📷 {拍摄建议}</div>
<div style="font-size:12px; color:#888;">🌊 {出片风格}</div>
</div>
</div>
```

### 第十章：需要预约的景点

```html
## 🎫 需要预约的景点

<div style="display:flex; flex-wrap:wrap; gap:12px;">
<div style="flex:1; min-width:250px; background:#ffffff; border-radius:12px; padding:16px; border-left:4px solid #ef5350;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🏛️ <b>{景点1}</b></div>
<div style="font-size:13px; line-height:1.8;">
🎫 门票：🔴 <b>免费</b>（交通{X}元）<br>
🕐 时间：<b>{开放时间}</b><br>
📱 预约："{公众号}"<br>
⭐ 难度：⭐⭐
</div>
</div>
<div style="flex:1; min-width:250px; background:#fafafa; border-radius:12px; padding:16px; border-left:4px solid #ff9800;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🏞️ <b>{景点2}</b></div>
<div style="font-size:13px; line-height:1.8;">
🎫 门票：<b>{X}元</b>（含船）<br>
🕐 时间：<b>{开放时间}</b><br>
📱 预约："{公众号}"<br>
⭐ 难度：⭐⭐⭐
</div>
</div>
<div style="flex:1; min-width:250px; background:#ffffff; border-radius:12px; padding:16px; border-left:4px solid #4caf50;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🌊 <b>{景点3}</b></div>
<div style="font-size:13px; line-height:1.8;">
🎫 门票：<b>{X}元</b>（A线含船）<br>
🕐 时间：<b>{开放时间}</b><br>
📱 预约："{公众号}"<br>
⭐ 难度：⭐⭐⭐
</div>
</div>
</div>
```

### 第十一章：实用Tips（⭐大色块）

```html
## 📌 {目的地}游玩实用Tips

> ▼ {N}条实用建议，出发前必看！

<div style="display:flex; flex-wrap:wrap; gap:12px;">
<div style="flex:1; min-width:280px; background:#e3f2fd; border-radius:12px; padding:16px;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🚗 1. 自驾路线选择</div>
<div style="font-size:13px; line-height:1.8;">
去程走<b>G348三峡公路</b>（风景绝美），回程走<b>G50沪渝高速</b>（快速便捷）。
</div>
</div>
<div style="flex:1; min-width:280px; background:#fce4ec; border-radius:12px; padding:16px;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🏗️ 2. 三峡大坝攻略</div>
<div style="font-size:13px; line-height:1.8;">
🔴 <b>免费但必须预约！</b>刷身份证入园。电瓶车<b>10元</b>。
</div>
</div>
<div style="flex:1; min-width:280px; background:#fff8e1; border-radius:12px; padding:16px;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🌤️ 3. 清江画廊看天气</div>
<div style="font-size:13px; line-height:1.8;">
🔴 <b>一定要晴天去！</b>阴雨天风景大打折扣。
</div>
</div>
<div style="flex:1; min-width:280px; background:#e8f5e9; border-radius:12px; padding:16px;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🏨 4. 住宿选择</div>
<div style="font-size:13px; line-height:1.8;">
推荐住<b>市中心/沿江大道</b>附近。预算充足选<b>江景房</b>。
</div>
</div>
<div style="flex:1; min-width:280px; background:#f3e5f5; border-radius:12px; padding:16px;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🅿️ 5. 停车信息</div>
<div style="font-size:13px; line-height:1.8;">
景区<b>10元/次</b>，市区路边<b>3~5元/小时</b>。
</div>
</div>
<div style="flex:1; min-width:280px; background:#ffebee; border-radius:12px; padding:16px;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">🍜 6. 吃饭防坑</div>
<div style="font-size:13px; line-height:1.8;">
🔴 <b>别在景区内吃饭！</b>回市区或县城吃。
</div>
</div>
<div style="flex:1; min-width:280px; background:#e0f7fa; border-radius:12px; padding:16px;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">💰 7. 省钱技巧</div>
<div style="font-size:13px; line-height:1.8;">
学生证<b>半价</b>；旅游年卡<b>100元/年</b>。
</div>
</div>
<div style="flex:1; min-width:280px; background:#efebe9; border-radius:12px; padding:16px;">
<div style="font-size:15px; font-weight:bold; margin-bottom:8px;">📞 8. 应急信息</div>
<div style="font-size:13px; line-height:1.8;">
市中心医院：<b>0717-6223999</b><br>高速救援：<b>12122</b>
</div>
</div>
</div>
```

> **Tips 色块规则**：`flex:1; min-width:280px`，每行2~3个，不同浅色背景轮换。

### 第十二章：朋友圈文案

```html
## 📱 {目的地}朋友圈文案

> ▼ {N}条精选文案，发朋友圈直接复制！

<div style="display:flex; flex-wrap:wrap; gap:10px;">
<div style="flex:1; min-width:250px; background:#fce4ec; border-radius:10px; padding:12px 16px; font-size:13px;">1. ✅ 打卡📍{目的地} {日期}</div>
<div style="flex:1; min-width:250px; background:#e3f2fd; border-radius:10px; padding:12px 16px; font-size:13px;">2. {文艺风格文案}</div>
<div style="flex:1; min-width:250px; background:#e8f5e9; border-radius:10px; padding:12px 16px; font-size:13px;">3. {幽默风格文案}</div>
<div style="flex:1; min-width:250px; background:#fff8e1; border-radius:10px; padding:12px 16px; font-size:13px;">4. {古风/文艺文案}</div>
</div>
```

### 第十三章：费用预算

```html
## 💰 费用预算参考（人均）

<div style="display:flex; flex-wrap:wrap; gap:10px; margin-bottom:12px;">
<div style="flex:1; min-width:130px; background:#f5f5f5; border-radius:10px; padding:14px 16px; text-align:center;">
<div style="font-size:20px; margin-bottom:4px;">🚄</div>
<div style="font-size:12px; color:#888;">大交通</div>
<div style="font-size:16px; font-weight:bold;"><b>{X}</b>元</div>
</div>
<div style="flex:1; min-width:130px; background:#ffffff; border-radius:10px; padding:14px 16px; text-align:center;">
<div style="font-size:20px; margin-bottom:4px;">🏨</div>
<div style="font-size:12px; color:#888;">住宿（{N}晚）</div>
<div style="font-size:16px; font-weight:bold;"><b>{X}</b>元</div>
</div>
<div style="flex:1; min-width:130px; background:#f5f5f5; border-radius:10px; padding:14px 16px; text-align:center;">
<div style="font-size:20px; margin-bottom:4px;">🎫</div>
<div style="font-size:12px; color:#888;">门票</div>
<div style="font-size:16px; font-weight:bold;"><b>{X}</b>元</div>
</div>
<div style="flex:1; min-width:130px; background:#ffffff; border-radius:10px; padding:14px 16px; text-align:center;">
<div style="font-size:20px; margin-bottom:4px;">🍜</div>
<div style="font-size:12px; color:#888;">餐饮（{N}天）</div>
<div style="font-size:16px; font-weight:bold;"><b>{X}</b>元</div>
</div>
<div style="flex:1; min-width:130px; background:#f5f5f5; border-radius:10px; padding:14px 16px; text-align:center;">
<div style="font-size:20px; margin-bottom:4px;">🚇</div>
<div style="font-size:12px; color:#888;">市内交通</div>
<div style="font-size:16px; font-weight:bold;"><b>{X}</b>元</div>
</div>
<div style="flex:1; min-width:130px; background:#ffffff; border-radius:10px; padding:14px 16px; text-align:center;">
<div style="font-size:20px; margin-bottom:4px;">🛍️</div>
<div style="font-size:12px; color:#888;">购物/其他</div>
<div style="font-size:16px; font-weight:bold;"><b>{X}</b>元</div>
</div>
</div>

<div style="background:#e8f5e9; border-radius:12px; padding:16px; text-align:center; margin:12px 0;">
<div style="font-size:13px; color:#666;">💰 人均合计</div>
<div style="font-size:24px; font-weight:bold; color:#2e7d32;"><b>≈ {X} 元</b></div>
</div>

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

> 📌 <b>写在最后</b>：{一段温暖的结语}

</div>

</div>
```

---

## 内容生成规则

### 1. 信息准确性
- **必须通过网络搜索**获取目的地的最新信息
- 价格信息需标注"仅供参考，以实际为准"
- 预约信息需注明预约渠道和时间节点

### 2. 行程合理性
- 每日行程考虑**地理位置邻近性**，减少往返
- 每天安排 3-5 个景点/活动为宜
- 需考虑用餐时间（早餐 7:00-9:00，午餐 11:30-13:30，晚餐 17:30-19:30）

### 3. 风格适配
- **轻松版**：每天不超3个景点，10:00后出发
- **特种兵版**：紧凑安排，早起晚归
- **亲子版**：增加适合儿童的景点，降低步行强度
- **美食版**：以美食为主线串联行程
- **穷游版**：优先免费/低价景点

### 4. 排版规范（⭐重点·v1.4 纯卡片版）

#### 4.1 全局字体
- 文档最开头 `<div style="font-size:14px; line-height:1.8; color:#333;">`，末尾 `</div>` 闭合

#### 4.2 ⚠️ 禁止使用 table
- **全文禁止使用 `<table>`、`<tr>`、`<td>`、`<th>` 标签**
- 所有数据展示统一使用 **Flexbox 卡片布局**

#### 4.3 Flexbox 卡片布局规范

```css
/* 容器 */
display: flex;
flex-wrap: wrap;       /* 自动换行 */
gap: 12px;             /* 卡片间距 */

/* 卡片 */
flex: 1;               /* 等分空间 */
min-width: 280px;      /* 最小宽度，窄屏自动换行 */
border-radius: 12px;   /* 圆角 */
padding: 16px;         /* 内边距 */
```

#### 4.4 各模块卡片参数

| 模块 | min-width | 背景色 | 特殊样式 |
|:---|:---:|:---|:---|
| **准备清单** | 200px | 蓝/绿/橙/紫/黄 | 车辆检查 `flex:2` |
| **天气** | 150px | 灰/白交替 | — |
| **行程总览** | 250px | 绿/蓝/粉 | — |
| **景点详情** | 全宽 | 标题栏+内容栏 | 上午蓝/下午绿/晚上橙 |
| **美食** | 280px | 白/浅灰交替 | 左侧金色色条 `#ffb800` |
| **住宿** | 280px | 蓝/绿/粉/紫 | — |
| **交通路线** | 280px | 灰/蓝 | 推荐路线左侧蓝色色条 |
| **拍照点** | 220px | 白/浅灰交替 | — |
| **预约景点** | 250px | 白/浅灰交替 | 左侧彩色色条 |
| **Tips** | 280px | 多色轮换 | — |
| **朋友圈文案** | 250px | 粉/蓝/绿/黄 | — |
| **费用预算** | 130px | 灰/白交替 | 居中，大数字 |

#### 4.5 高亮标注体系

| 标注类型 | 格式 | 示例 |
|:---|:---|:---|
| **关键数据** | `<b>{内容}</b>` | <b>35元/人</b> |
| **警示信息** | `🔴 <b>{内容}</b>` | 🔴 <b>免费但必须预约！</b> |

#### 4.6 色块提示框

```html
<!-- 黄色提示框 -->
<div style="background:#fff8e1; border-left:4px solid #ffc107; padding:12px 16px; border-radius:0 8px 8px 0; margin:12px 0;">
💡 <b>温馨提示</b>：{内容}
</div>

<!-- 绿色预算框 -->
<div style="background:#e8f5e9; border-left:4px solid #43a047; padding:12px 16px; border-radius:0 8px 8px 0; margin:12px 0;">
💰 <b>预算参考</b>：{内容}
</div>
```

### 5. 图片处理（⭐重点）

- **禁止使用 AI 生成图片**
- **必须通过网络搜索获取真实照片**
- 图片保存至 `images/` 文件夹，`.jpg` 格式，中文命名
- 封面1张 + 景点各1张 + 美食1~2张 ≈ **8~12张**
- Markdown 引用：`![{描述}](images/{文件名}.jpg)`

### 6. 语言风格
- 友好、实用、接地气
- 避坑提示配合 🔴 标记
- 美食描述突出口感
- 价格使用具体数字

## 工作流程

1. **确认需求**：明确目的地、天数、出行时间、旅行风格
2. **信息搜集**：网络搜索（3~5次），收集景点/美食/住宿/交通/天气信息
3. **图片搜集**：搜索下载真实照片（与信息搜集并行）
4. **行程规划**：按地理位置分组，安排动线和时间
5. **内容生成**：
   - ⚠️ 以 `<div style="font-size:14px;">` 开头
   - ⚠️ **禁止使用 `<table>`**，全部用 Flexbox 卡片
   - 景点卡片按时段色系（蓝/绿/橙）
   - Tips 用彩色色块网格
   - 末尾 `</div>` 闭合
6. **文档输出**：Markdown + images 文件夹保存到用户工作区

## 示例调用

**用户输入**：
> 帮我生成一份西安4天3晚的旅行攻略，五一假期去，轻松版，两个人从北京出发

**输出**：
生成 `西安4天3晚旅行攻略（五一轻松版）.md`，使用 Flexbox 卡片布局，附带 8~12 张真实照片。
