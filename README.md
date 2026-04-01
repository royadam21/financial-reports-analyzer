# 财报分析项目

## 项目概述

主人发来上市公司的财报源文件（PDF），虾砌码负责解读、分析、制作内容详实、数据准确、逻辑清晰的财报分析报告网页。

## 交付物

### 1. PC端网页 (`{公司名}_report_{年份}.html`)
- 全屏深色主题，腾讯财报风格
- 包含：KPI概览、营收分析、利润分析、资产负债表、现金流、核心业务分析、行业对比、AI总结等模块
- 使用Chart.js图表库
- 固定导航栏 + 平滑滚动

### 2. 移动端网页 (`{公司名}_report_{年份}_mobile.html`)
- 移动端适配布局，紧凑卡片式设计
- 底部固定导航栏（核心指标、业务分布、市场布局、AI总结）
- 横向滚动KPI卡片
- 触摸友好的交互

### ⚠️ 移动端必须包含的元素（必须严格遵守）

#### 底部导航栏
```html
<nav class="bottom-nav">
    <a href="#" onclick="showTab('kpi'); return false;" class="active" data-tab="kpi">
        <span class="nav-icon">📊</span>
        <span>核心指标</span>
    </a>
    <a href="#" onclick="showTab('business'); return false;" data-tab="business">
        <span class="nav-icon">🏢</span>
        <span>业务分布</span>
    </a>
    <!-- 其他标签... -->
</nav>
```

#### CSS样式
```css
.bottom-nav {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    background: rgba(26,26,46,0.98);
    backdrop-filter: blur(10px);
    border-top: 1px solid var(--border-color);
    display: flex;
    z-index: 1000;
    padding: 8px 0;
    padding-bottom: max(8px, env(safe-area-inset-bottom));
}
```

#### showTab函数同步高亮
```javascript
function showTab(tabName) {
    document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
    document.querySelectorAll('.tab-btn').forEach(el => el.classList.remove('active'));
    document.querySelectorAll('.bottom-nav a').forEach(el => el.classList.remove('active'));
    document.getElementById('tab-' + tabName).classList.add('active');
    const topBtn = document.querySelector('.tab-btn[data-tab="' + tabName + '"]');
    const bottomBtn = document.querySelector('.bottom-nav a[data-tab="' + tabName + '"]');
    if (topBtn) topBtn.classList.add('active');
    if (bottomBtn) bottomBtn.classList.add('active');
}
```

#### 禁止出现的元素
- ❌ 禁止出现「PC版/移动版切换」按钮
- ❌ 禁止出现 desktop-toggle 相关HTML和CSS

## 报告模块（根据实际财报内容灵活设计）

根据原始财报内容，AI自主设计最适合的模块结构，示例模块包括但不限于：

- **封面Hero** - 公司名称、财报周期、核心数据概览
- **KPI卡片区** - 营收、净利润、毛利率、每股收益等关键指标
- **营收分析** - 按业务线/地区拆解，图表展示
- **利润分析** - 毛利、净利、利润率趋势
- **资产负债表** - 资产、负债、权益变化
- **现金流分析** - 经营/投资/筹资现金流
- **核心业务分析** - 各业务线表现
- **行业对比** - 与主要竞争对手数据对比
- **总结与展望** - 基于财报内容的综合分析

**核心原则：财报有什么就分析什么，模块跟着内容走。**

## 数据处理规则

- 所有数据必须来源于原始财报PDF，**绝不编造**
- 货币单位需统一标注（如：亿元人民币）
- 百分比、增长率需精确计算
- 表格数据保留两位小数
- 引用数据需标注来源页码

## 文件命名规范

- PC端：`{公司名}_report_{年份}.html`（如：腾讯_report_2025.html）
- 移动端：`{公司名}_report_{年份}_mobile.html`
- 源文件：`{公司名}_财报_{年份}.pdf`

## 参考模板

腾讯财报分析（已完成）：
- 目录：`C:\Users\11985\.openclaw\workspace_coding\projects\财报分析\tencent_report_2025\`
- PC端：`tencent_report_2025.html`
- 移动端：`tencent_report_2025_mobile.html`

美团财报分析（已完成）：
- 目录：`C:\Users\11985\.openclaw\workspace_coding\projects\财报分析\meituan_report_2025\`
- PC端：`meituan_report_2025.html`
- 移动端：`meituan_report_2025_mobile.html`

比亚迪财报分析（已完成）：
- 目录：`C:\Users\11985\.openclaw\workspace_coding\projects\财报分析\byd_report_2025\`
- PC端：`byd_report_2025.html`
- 移动端：`byd_report_2025_mobile.html`
