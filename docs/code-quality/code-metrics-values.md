---
title: 计算代码度量
ms.date: 11/02/2018
description: 了解圈复杂度、类耦合和其他 Visual Studio 代码度量。 了解度量如何跟踪开发进度并确定风险。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601333"
---
# <a name="code-metrics-values"></a>代码度量值

新式软件应用程序的复杂性增加也增加了使代码可靠和可维护的难度。 代码度量是一组软件度量值，使开发人员可以更好地了解他们正在开发的代码。 开发人员利用代码度量可以了解应修改哪些类型和/或方法或对其进行更全面的测试。 开发团队可确定潜在风险、了解项目的当前状态以及在软件开发过程中跟踪进度。

开发人员可使用 Visual Studio 生成代码度量数据，以衡量其托管代码的复杂性和可维护性。 可为整个解决方案或单个项目生成代码度量数据。

有关如何在 Visual Studio 中生成代码度量数据的信息，请参阅[如何：生成代码度量数据](../code-quality/how-to-generate-code-metrics-data.md)。

## <a name="software-measurements"></a>软件度量

以下列表显示 Visual Studio 计算的代码度量结果：

- **可维护性指数** - 计算介于 0 到 100 之前的指数值，它表示维护代码的相对难易程度。 较高的值表示可维护性更高。 颜色编码评级可用于快速标识代码中的故障点。 绿色评级介于 20 到 100 之间，表示代码可维护性良好。 黄色评级介于 10 到 19 之间，表示代码可维护性适中。 红色评级是介于 0 到 9 之间的评级，表示可维护性低。 有关详细信息，请参阅[可维护性指数的范围和含义](code-metrics-maintainability-index-range-and-meaning.md)。

- **圈复杂度** - 度量代码的结构化复杂度。 通过计算程序流中不同代码路径的数目来得到该值。 具有复杂控制流的程序需要进行更多测试才能实现良好的代码覆盖率，而且可维护性较低。 有关详细信息，请参阅[有关圈复杂度的 Wikipedia 文章](https://wikipedia.org/wiki/Cyclomatic_complexity)。

- **继承深度** - 指示彼此继承、一直继承到基类的不同类的数量。 继承深度类似于类耦合，因为基类中的更改可能会影响其任何继承的类。 此数字越大，继承越深入，基类修改导致中断性变更的可能性就越大。 就继承深度而言，较小的值更适合，而较大的值则不适合。

- **类耦合** - 通过参数、本地变量、返回类型、方法调用、泛型实例化或模板实例化、基类、接口实现、在外部类型上定义的字段和特性修饰来度量与唯一类的耦合度。 良好的软件设计决定类型和方法应具有高内聚和低耦合度。 高耦合度表明一个设计由于与其他类型有许多相互依存关系而难以重用和维护。 有关详细信息，请参阅[类耦合](code-metrics-class-coupling.md)。

::: moniker range=">=vs-2019"

- **源代码行** - 表示源文件中存在的源代码行（包括空行）的确切数目。 此度量从 Visual Studio 2019 版本 16.4 和 Microsoft.CodeAnalysis.Metrics (2.9.5) 开始可用。

- **可执行代码行** - 表示可执行代码行或操作的大致数目。 这是对可执行代码中操作数的计数。 此度量从 Visual Studio 2019 版本 16.4 和 Microsoft.CodeAnalysis.Metrics (2.9.5) 开始可用。 该值通常与上一个度量代码行（即在旧模式下使用的基于 MSIL 指令的度量）接近。
::: moniker-end
::: moniker range="vs-2017"

- **代码行** - 指示代码中的大致数目。 计数基于 IL 代码，因此不是源代码文件中的准确行数。 较高的计数可能表示某个类型或方法正在尝试执行过多的工作，应进行拆分。 它还可能指示类型或方法可能难以维护。

   > [!NOTE]
   > 代码度量工具的[命令行版本](../code-quality/how-to-generate-code-metrics-data.md#command-line-code-metrics)计算实际代码行数，因为它分析源代码而不是 IL。
::: moniker-end

## <a name="anonymous-methods"></a>匿名方法

匿名方法只是没有名称的方法。 匿名方法经常用于将代码块作为委托参数进行传递。 在成员中声明的匿名方法（如方法或访问器）的代码度量结果与声明该方法的成员相关联。 它们不与调用方法的成员关联。

## <a name="generated-code"></a>生成的代码

某些软件工具和编译器会生成添加到项目中的代码，而项目开发人员不能查看或不应更改这些代码。 通常，当代码度量计算度量值时，它会忽略生成的代码。 这样，度量值就可以反映开发人员可以查看和更改的内容。

不会忽略为 Windows 窗体生成的代码，因为这是开发人员可以查看和更改的代码。

## <a name="next-steps"></a>后续步骤

- [如何：生成代码度量数据](../code-quality/how-to-generate-code-metrics-data.md)
- [使用“代码度量结果”窗口](../code-quality/working-with-code-metrics-data.md)