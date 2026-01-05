# 第 04 章：复数处理与规则配置

不同语言在表达数量时有不同的语法规则（例如英语中 1 个和多个的区别）。`easy_localization` 提供了强大的复数处理能力。

## 复数翻译基础

使用 `plural()` 方法来处理与数量相关的翻译。

### 1. JSON 资源定义

在 JSON 文件中，使用一个包含特定关键字的对象来定义复数形式：

```json
{
  "money": {
    "zero": "您没有钱",
    "one": "您有 {} 美元",
    "many": "您有 {} 美元",
    "other": "您有 {} 美元"
  }
}
```

> ⚠️ 注意：`other` 字段是必须提供的，作为兜底选项。

### 2. 代码调用

```dart
// 使用 extension 方法
Text('money').plural(10.50) // 输出: 您有 10.5 美元

// 带有数字格式化
Text('money').plural(1000000, format: NumberFormat.compact()) // 输出: 您有 1M 美元
```

## 支持的复数分类

根据国际标准，复数分类包括：

- `zero`: 数量为 0
- `one`: 数量为 1（单数）
- `two`: 数量为 2
- `few`: 少数
- `many`: 多数
- `other`: 其他（通用/必须）

## 进阶配置：ignorePluralRules

在某些语言中，复数逻辑可能非常简单。默认情况下，`easy_localization` 会忽略 `few` 和 `many` 分类。如果您需要启用这些分类，请在初始化时设置：

```dart
EasyLocalization(
  ignorePluralRules: false, // 设置为 false 以启用完整的 CLDR 复数规则
  // ... 其他配置
)
```

## 参数化复数

您还可以在复数翻译中混入其他命名参数或位置参数。

```json
{
  "money_named": {
    "one": "{name} 有 {money} 美元",
    "other": "{name} 有 {money} 美元"
  }
}
```

```dart
var output = plural('money_named', 10.23, namedArgs: {'name': '张三', 'money': '10.23'});
```

## 接下来

掌握了复数处理后，我们来看看如何更高效地组织大型项目的翻译文件。请参考 [05 进阶：链接翻译与文件拆分](05-advanced-linked-translations-and-files.md)。
