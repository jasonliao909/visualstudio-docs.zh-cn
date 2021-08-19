---
title: 计算代码指标
ms.date: 11/02/2018
description: 了解循环复杂性、类耦合和其他Visual Studio指标。 了解指标如何跟踪开发进度和识别风险。
ms.custom: SEO-VS-2020
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.codemetrics.toolwindow
dev_langs:
- CSharp
- VB
- FSharp
helpviewer_keywords:
- code metrics [Visual Studio]
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: fbd74301a7a7ff1299b8d9496e20793bbfabdf6f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122122158"
---
# <a name="code-metrics-values"></a>代码指标值

现代软件应用程序的复杂性增加也增加了使代码可靠且可维护的难度。 代码度量是一组软件度量值，使开发人员可以更好地了解他们正在开发的代码。 通过利用代码指标，开发人员可以了解应修改或更全面测试的类型和/或方法。 开发团队可以识别潜在风险、了解项目的当前状态，以及跟踪软件开发过程中的进度。

开发人员可以使用Visual Studio生成代码指标数据，用于测量其托管代码的复杂性和可维护性。 可以针对整个解决方案或单个项目生成代码指标数据。

若要了解如何在 Visual Studio 生成代码指标数据，请参阅[如何：生成代码指标数据](../code-quality/how-to-generate-code-metrics-data.md)。

## <a name="software-measurements"></a>软件度量

以下列表显示了要计算的代码Visual Studio结果：

- **可维护性** 索引 - 计算一个介于 0 和 100 之间的索引值，该值表示相对易于维护代码。 较高的值意味着更好的可维护性。 颜色编码的评分可用于快速识别代码中的故障点。 绿色分级介于 20 和 100 之间，表示代码具有良好的可维护性。 黄色分级介于 10 和 19 之间，表示代码可适当维护。 红色评级是介于 0 和 9 之间的分级，表示可维护性较低。 有关详细信息，请参阅可 [维护性索引范围和含义](code-metrics-maintainability-index-range-and-meaning.md)。

- **循环复杂性** - 度量代码的结构复杂性。 它是通过计算程序流中不同代码路径的数量创建的。 具有复杂控制流的程序需要执行更多测试才能实现良好的代码覆盖率，并且其可维护性较低。 有关详细信息，请参阅循环 [复杂性的维基百科条目](https://wikipedia.org/wiki/Cyclomatic_complexity)。

- **继承深度** - 指示从彼此继承的不同类的数量，一路返回到基类。 继承深度类似于类耦合，基类中的更改可能会影响其任何继承的类。 此数字越高，继承越深，基类修改导致中断性变更的可能性就越高。 对于"继承深度"，低值很好，高值则错误。

- **类** 耦合 - 通过参数、局部变量、返回类型、方法调用、泛型或模板实例化、基类、接口实现、外部类型上定义的字段和属性修饰来度量与唯一类的耦合。 良好的软件设计规定类型和方法应具有高内聚和低耦合性。 高耦合表示设计难以重用和维护，因为它与其他类型存在许多相互依赖关系。 有关详细信息，请参阅类 [耦合](code-metrics-class-coupling.md)。

::: moniker range=">=vs-2019"

- **源代码行** - 指示源文件中的确切源代码行数，包括空白行。 此指标从 Visual Studio 2019 版本 16.4 和 Microsoft.CodeAnalysis.Metrics (2.9.5) 开始提供。

- **可执行代码行** - 指示可执行代码行或操作近似数。 这是可执行代码中的操作计数。 此指标从 Visual Studio 2019 版本 16.4 和 Microsoft.CodeAnalysis.Metrics (2.9.5) 开始提供。 该值通常与上一个指标 **"** 代码行"非常匹配，这是旧模式下使用的基于 MSIL 指令的指标。
::: moniker-end
::: moniker range="vs-2017"

- **代码行** - 指示代码中的近似行数。 计数基于 IL 代码，因此不是源代码文件中的确切行数。 高计数可能指示类型或方法尝试执行过多工作，应拆分。 它还可能指示类型或方法可能难以维护。

   > [!NOTE]
   > [代码指标工具的命令行](../code-quality/how-to-generate-code-metrics-data.md#command-line-code-metrics)版本对实际代码行进行计数，因为它会分析源代码而不是 IL。
::: moniker-end

## <a name="anonymous-methods"></a>匿名方法

匿名 *方法* 只是一个没有名称的方法。 匿名方法最常用于将代码块作为委托参数传递。 在成员中声明的匿名方法（如方法或访问器）的代码指标结果与声明该方法的成员相关联。 它们不与调用 方法的成员关联。

## <a name="generated-code"></a>生成的代码

某些软件工具和编译器会生成添加到项目中且项目开发人员看不到或不应更改的代码。 大多数情况下，代码指标在计算指标值时将忽略生成的代码。 这使指标值能够反映开发人员可以看到和更改的值。

不会忽略Windows窗体生成的代码，因为它是开发人员可以看到和更改的代码。

## <a name="next-steps"></a>后续步骤

- [如何：生成代码指标数据](../code-quality/how-to-generate-code-metrics-data.md)
- [使用"代码指标结果"窗口](../code-quality/working-with-code-metrics-data.md)