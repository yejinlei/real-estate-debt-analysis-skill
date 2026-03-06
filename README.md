# 房产债权分析技能 (Real Estate Debt Analysis Skill)

## 项目简介

这是一个基于Claude SKILL规范开发的房产债权分析工具，能够分析任何城市任何地区的房产债权价值和投资潜力。

## 核心功能

- **多输入格式支持**：
  - 直接输入房产数据
  - Excel表格（与Excel解析SKILL协作）
  - CSV/JSON文件（与文件解析SKILL协作）
  - 文本数据
  - 图片数据（与图片解析SKILL协作，支持OCR提取）
  - 音频数据（与音频解析SKILL协作，支持语音转写）
  - 多模态数据

- **智能价格分析**：
  - 支持全国主要城市和地区的房产价格分析
  - 基于城市等级、区域特征等因素进行价格评估
  - 提供安居客和阿里拍卖价格对比

- **投资价值评估**：
  - 计算债权覆盖率
  - 分析法拍折扣率
  - 评估流动性风险
  - 提供投资建议

- **多SKILL协作**：
  - 与Excel解析SKILL协作处理表格数据
  - 与文件解析SKILL协作处理CSV/JSON文件
  - 与图片解析SKILL协作处理图片中的表格和文本
  - 与音频解析SKILL协作处理语音数据
  - 与多模态解析SKILL协作处理混合格式数据

## 技术架构

- **SKILL定义**：`SKILL.md` - 包含技能的元数据、触发词、输入参数和输出格式
- **核心脚本**：`scripts/real_estate_analysis.py` - 实现房产债权分析的核心逻辑
- **配置文件**：`scripts/price_config.json` - 可自定义价格数据

## 使用方法

### 直接输入格式

```python
{
    "action": "analyze_debt_portfolio",
    "property_data": [
        {
            "address": "北京市海淀区中关村大街1号",
            "debt_principal": 500.0,
            "area": 100.0
        }
    ]
}
```

### 与Excel解析SKILL协作格式

```python
{
    "action": "analyze_debt_portfolio",
    "excel_data": {
        "headers": ["地址", "债权本金", "面积"],
        "rows": [
            ["上海市浦东新区陆家嘴环路1000号", 1000.0, 150.0],
            ["广州市天河区珠江新城冼村路28号", 800.0, 120.0]
        ]
    }
}
```

### 与图片解析SKILL协作格式

```python
{
    "action": "analyze_debt_portfolio",
    "image_data": {
        "extracted_table": {
            "headers": ["地址", "债权本金", "面积"],
            "rows": [
                ["深圳市南山区科技园南区高新南一道", 600.0, 110.0],
                ["成都市锦江区红星路三段", 400.0, 90.0]
            ]
        }
    }
}
```

## 配置说明

### 价格配置文件

技能支持通过`scripts/price_config.json`文件自定义价格数据：

```json
{
  "北京": 60000,
  "上海": 65000,
  "广州": 35000,
  "深圳": 55000,
  "杭州": 30000
}
```

### 环境变量

技能支持通过环境变量配置外部服务：
- `REPORT_GENERATOR_SERVICE`：报告生成服务地址
- `DATA_PROCESSING_SERVICE`：数据处理服务地址
- `WEB_SEARCH_SERVICE`：网络搜索服务地址

## 触发词

### 主要触发词
- 房产债权分析
- 债权价值评估
- 房产包投资分析
- 安居客和阿里拍卖价格对比
- 法拍房投资分析

### 与文件解析SKILL协作触发词
- 分析excel表格里的债权
- 帮我分析这个表格的债权数据
- 从表格中分析债权价值
- 解析excel并进行债权分析
- 分析csv文件中的债权数据
- 解析json文件并进行债权分析

### 与图片解析SKILL协作触发词
- 分析图片中的债权数据
- 从照片中提取房产信息
- 解析图片里的表格数据
- 帮我分析这张图片的债权信息

### 与音频解析SKILL协作触发词
- 分析语音中的债权信息
- 从录音中提取房产数据
- 解析音频里的债权本金和面积
- 帮我分析这段录音的房产信息

## 输出格式

```json
{
  "success": true,
  "action": "analyze_debt_portfolio",
  "analysis_results": [
    {
      "address": "北京市海淀区中关村大街1号",
      "debt_principal": 500.0,
      "area": 100.0,
      "anjuke_price": 60000,
      "auction_price": 51000,
      "auction_discount_rate": 0.85,
      "market_value": 5100000,
      "debt_coverage_ratio": 1.02,
      "liquidity_score": 85,
      "risk_level": "低",
      "investment_suggestion": "优先关注",
      "risk_assessment": {
        "legal_risk": "低",
        "market_risk": "中",
        "liquidity_risk": "低",
        "operational_risk": "中"
      }
    }
  ],
  "summary": "本次分析了1处房产，其中1处建议优先关注。平均债权覆盖率为102%，平均法拍折扣率为85%。",
  "report_url": "http://localhost:8000/reports/analysis_20260306_123456.pdf"
}
```

## 安装与使用

1. 克隆仓库：
   ```bash
   git clone https://github.com/yejinlei/real-estate-debt-analysis-skill.git
   ```

2. 安装依赖：
   ```bash
   pip install -r requirements.txt
   ```

3. 配置价格数据（可选）：
   ```bash
   cp scripts/price_config.json.example scripts/price_config.json
   # 编辑price_config.json文件
   ```

4. 部署到Claude SKILL环境

## 注意事项

- **数据时效性**：房产价格变化较快，注意数据更新时间
- **信息准确性**：法拍信息可能存在滞后，需多方验证
- **法律合规**：法拍房涉及法律程序，建议咨询专业律师
- **市场风险**：房地产市场存在波动风险，需谨慎评估
- **成本考虑**：法拍房虽价格低，但需考虑税费、装修等隐性成本

## 许可证

MIT License

## 联系方式

- GitHub：[https://github.com/yejinlei/real-estate-debt-analysis-skill](https://github.com/yejinlei/real-estate-debt-analysis-skill)
