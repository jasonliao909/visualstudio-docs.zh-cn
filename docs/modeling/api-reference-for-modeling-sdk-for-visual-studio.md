---
title: 建模 SDK 的 API 参考
description: 了解 Visual Studio 可视化和建模 SDK 如何提供 (dsl) 工具生成的特定平台。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 644b31985d6e187ef757ec1c0cb37827776ac022
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122157587"
---
# <a name="api-reference-for-modeling-sdk-for-visual-studio"></a>Visual Studio 的建模 SDK 的 API 参考

Visual Studio 可视化和建模 SDK 提供了一种平台，用于构建域特定语言 (DSL) 工具。

本部分包含名称以 "VisualStudio" 开头的命名空间的参考资料。

|命名空间|内容|
|-|-|
|<xref:Microsoft.VisualStudio.Modeling?displayProperty=fullName>|诸如 ModelElement 之类的类，该类是在 DSL 中定义的所有域类的基类。|
|<xref:Microsoft.VisualStudio.Modeling.Design?displayProperty=fullName>|构成 DSL 定义的一部分的类。|
|<xref:Microsoft.VisualStudio.Modeling.Diagnostics?displayProperty=fullName>|模型存储查看器和性能度量工具。|
|<xref:Microsoft.VisualStudio.Modeling.Diagrams?displayProperty=fullName>|诸如 ShapeElement 之类的类，它是在 DSL 中定义的所有形状的基类。|
|<xref:Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement?displayProperty=fullName>|手势和选择方法。|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition?displayProperty=fullName>|DSL 定义设计器的 API。|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition.Design?displayProperty=fullName>|DSL 定义设计器的内部类。|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition.ExtensionEnablement?displayProperty=fullName>|允许通过命令、笔势和验证来扩展 DSL 设计器的属性。|
|<xref:Microsoft.VisualStudio.Modeling.Extensibility?displayProperty=fullName>|实现 DSL 扩展性的 ModelElement 扩展方法。|
|<xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement?displayProperty=fullName>|扩展性特性|
|<xref:Microsoft.VisualStudio.Modeling.Immutability?displayProperty=fullName>|允许您将模型的某些部分设置为只读。|
|[VisualStudio 集成](/previous-versions/ee904412(v=vs.140))|Modelbus API，可帮助你集成不同的模型。|
|[VisualStudio （& e）](/previous-versions/ee904394(v=vs.140))|允许用户导航到模型和元素以创建 Modelbus 引用的对话框。|
|`Microsoft.VisualStudio.Modeling.Integration.Picker.Hosting`|选取器服务。|
|[VisualStudio 命令行界面](/previous-versions/ee869435(v=vs.140))|用于 Visual Studio 的 Modelbus 适配器框架。|
|[VisualStudio （如果选择）](/previous-versions/ee886769(v=vs.140))|允许用户导航到模型和元素以创建 Modelbus 引用的 "选取器" 对话框。|
|<xref:Microsoft.VisualStudio.Modeling.Shell?displayProperty=fullName>|Dsl 和 Visual Studio 之间的接口。|
|<xref:Microsoft.VisualStudio.Modeling.Shell.ExtensionEnablement?displayProperty=fullName>|允许您 (上下文) 菜单命令定义快捷方式。|
|<xref:Microsoft.VisualStudio.Modeling.Validation?displayProperty=fullName>|允许您定义验证约束。|

## <a name="see-also"></a>请参阅

- [自定义 T4 文本转换](../modeling/customizing-t4-text-transformation.md)
