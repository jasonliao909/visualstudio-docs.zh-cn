---
title: T4 文本模板指令
description: 了解 T4 测试模板指令及其如何向文本模板转换引擎提供说明。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, import directive
- text templates, include directive
- text templates, assembly directive
- text templates, output directive
- text templates, directives
- text templates, template directive
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 59dee856b6779328d7382d2b816e55b66c6f50e9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122055310"
---
# <a name="t4-text-template-directives"></a>T4 文本模板指令

指令为文本模板转换引擎提供说明。

指令的语法如下所示：

```
<#@ DirectiveName [AttributeName = "AttributeValue"] ... #>
```

必须将所有特性值放在双引号内。 如果值本身包含引号，则必须使用 \ 字符对这些引号进行转义。

指令通常是模板文件或包含的文件中的第一个元素。 不应将它们放置在代码块 `<#...#>` 内，也不应放置在类功能块 `<#+...#>` 之后。

[T4 模板指令](../modeling/t4-template-directive.md)

```
<#@ template [language="VB"] [hostspecific="true|TrueFromBase"] [debug="true"] [inherits="templateBaseClass"] [culture="code"] [compilerOptions="options"] [visibility="internal"] [linePragmas="false"] #>
```

[T4 参数指令](../modeling/t4-parameter-directive.md)

```
<#@ parameter type="Full.TypeName" name="ParameterName" #>
```

[T4 输出指令](../modeling/t4-output-directive.md)

```
<#@ output extension=".fileNameExtension" [encoding="encoding"] #>
```

[T4 程序集指令](../modeling/t4-assembly-directive.md)

```
<#@ assembly name="[assembly strong name|assembly file name]" #>
```

[T4 导入指令](../modeling/t4-import-directive.md)

```
<#@ import namespace="namespace" #>
```

[T4 包含指令](../modeling/t4-include-directive.md)

```
<#@ include file="filePath" #>
```

[T4 CleanUpBehavior 指令](../modeling/t4-cleanupbehavior-directive.md)

```
<#@ CleanupBehavior processor="T4VSHost" CleanupAfterProcessingtemplate="true" #>
```

此外，您还可以创建自己的指令。 有关详细信息，请参阅创建自定义 [T4 文本模板指令处理器](../modeling/creating-custom-t4-text-template-directive-processors.md)。 如果使用可视化和建模 SDK 来创建域特定语言 (DSL)，将作为 DSL 的一部分生成指令处理器。
