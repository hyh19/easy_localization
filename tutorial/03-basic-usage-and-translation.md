# 第 03 章：基础用法与翻译技巧

在本章节中，我们将学习如何在应用中执行翻译操作、切换语言以及如何处理复杂的动态文本。

## 切换与获取语言

`easy_localization` 提供了便捷的 `BuildContext` 扩展方法来管理 Locale。

### 切换语言

```dart
// 设置为美国英语
context.setLocale(Locale('en', 'US'));

// 设置为简体中文
context.setLocale(Locale('zh', 'CN'));
```

### 获取当前 Locale

```dart
print(context.locale.toString()); // 输出: en_US
```

## 执行翻译

您可以使用多种方式来调用翻译功能，最推荐的是使用 `context.tr()` 或 `String` 的扩展方法。

### 基本翻译

```dart
// 在 Widget 中使用
Text(context.tr('title'))

// 使用 String 扩展方法（推荐）
Text('title').tr()

// 在逻辑代码中使用
String translated = 'title'.tr();
```

## 处理动态参数

通常翻译文本中会包含动态数据，如用户名或数量。

### 1. 列表参数 (args)

JSON 定义：

```json
{
  "welcome": "欢迎回来, {}!"
}
```

代码使用：

```dart
Text('welcome').tr(args: ['张三']) // 输出: 欢迎回来, 张三!
```

### 2. 命名参数 (namedArgs)

JSON 定义：

```json
{
  "info": "您当前的语言是 {lang}"
}
```

代码使用：

```dart
Text('info').tr(namedArgs: {'lang': 'Dart'}) // 输出: 您当前的语言是 Dart
```

## 性别切换 (Gender)

您可以根据性别动态显示不同的文本。

JSON 定义：

```json
{
  "gender": {
    "male": "先生, 您好",
    "female": "女士, 您好",
    "other": "您好"
  }
}
```

代码使用：

```dart
Text('gender').tr(gender: "male") // 输出: 先生, 您好
```

## 接下来

处理完基础翻译后，复杂的复数处理也是必不可少的。请参考 [04 复数处理与规则配置](04-plurals-and-plural-rules.md)。
