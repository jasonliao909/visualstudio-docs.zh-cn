---
title: 计算代码度量值
ms.date: 11/02/2018
description: 了解圈复杂度、类耦合和其他 Visual Studio 代码度量值。 了解度量值如何跟踪开发进度并确定风险。
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
ms.openlocfilehash: 8cbcb6f53f70de6f42b87551309a557f31b29f03a3bb73ea9825075bcb481a23
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121455499"
---
# <a name="code-metrics-values"></a>代码度量值

新式软件应用程序的复杂性增加还会增加代码的可靠性和可维护性。 代码度量是一组软件度量值，使开发人员可以更好地了解他们正在开发的代码。 通过利用代码度量，开发人员可以了解应该改编哪些类型和/或方法或对这些方法进行更全面的测试。 开发团队可以确定潜在风险、了解项目的当前状态以及在软件开发过程中跟踪进度。

开发人员可以使用 Visual Studio 来生成代码度量数据来度量其托管代码的复杂性和可维护性。 可以为整个解决方案或单个项目生成代码度量数据。

有关如何在 Visual Studio 中生成代码度量数据的信息，请参阅[如何：生成代码度量数据](../code-quality/how-to-generate-code-metrics-data.md)。

## <a name="software-measurements"></a>软件度量

以下列表显示 Visual Studio 计算的代码度量结果：

- 可 **维护性索引**-计算0到100之间的索引值，它表示维护代码的相对轻松程度。 较高的值表示更好的可维护性。 颜色编码分级可用于快速标识代码中的问题点。 绿色评级介于20和100之间，表示代码具有良好的可维护性。 黄色评分介于10和19之间，表示代码适度维护。 红色评分是0到9之间的评分，表示可维护性低。 有关详细信息，请参阅可 [维护性索引范围和含义](code-metrics-maintainability-index-range-and-meaning.md)。

- **圈复杂度** -度量代码的结构复杂性。 它通过计算程序流中的不同代码路径的数目来创建。 具有复杂控制流的程序需要进行更多测试才能实现良好的代码覆盖率，并且维护性更少。 有关详细信息，请参阅 [圈复杂度的维基百科条目](https://wikipedia.org/wiki/Cyclomatic_complexity)。

- **继承深度** -指示不同类的数量，这些类彼此继承，并回到基类。 继承深度类似于类耦合，因为基类中的更改可能会影响其任何继承的类。 此数字越大，继承越深入，导致重大更改的可能性越高，导致重大更改。 若要深入了解继承，值越小，值就越小。

- **类耦合** -通过参数、本地变量、返回类型、方法调用、泛型或模板实例化、基类、接口实现、在外部类型上定义的字段和特性修饰来度量与唯一类的耦合。 优秀的软件设计要求类型和方法应具有较高的聚合和低耦合。 高耦合性表明，由于它对其他类型的互依关系，难于重复使用和维护的设计。 有关详细信息，请参阅 [类耦合](code-metrics-class-coupling.md)。

::: moniker range=">=vs-2019"

- **源代码行** 数-表示源文件中存在的源代码行的确切数目，包括空行。 此指标从 Visual Studio 2019 16.4 和 CodeAnalysis (2.9.5) 开始可用。

- **可执行代码的行** 数-表示可执行代码行或操作的大致数目。 这是可执行代码中的操作数。 此指标从 Visual Studio 2019 16.4 和 CodeAnalysis (2.9.5) 开始可用。 值通常与上一个度量值（即在旧模式下使用的基于 MSIL 指令的度量值的 **行**）接近。
::: moniker-end
::: moniker range="vs-2017"

- **代码行** -指示代码中的近似行数。 计数基于 IL 代码，因此不是源代码文件中的准确行数。 较高的计数可能表示某个类型或方法正在尝试执行过多的工作并且应拆分。 它还可能指示可能难以维护类型或方法。

   > [!NOTE]
   > 代码度量值工具的 [命令行版本](../code-quality/how-to-generate-code-metrics-data.md#command-line-code-metrics) 对实际代码行进行计数，因为它分析源代码而不是 IL。
::: moniker-end

## <a name="anonymous-methods"></a>匿名方法

*匿名方法* 只是没有名称的方法。 匿名方法经常用于将代码块作为委托参数进行传递。 在成员中声明的匿名方法（如方法或访问器）的代码度量结果与声明该方法的成员相关联。 它们不与调用方法的成员相关联。

## <a name="generated-code"></a>生成的代码

某些软件工具和编译器会生成添加到项目中的代码，并且项目开发人员不会查看或不应更改。 通常，当代码度量值计算指标值时，它会忽略生成的代码。 这样，指标值就可以反映开发人员可以查看和更改的内容。

不会忽略为 Windows 窗体生成的代码，因为它是开发人员可以查看和更改的代码。

## <a name="next-steps"></a>后续步骤

- [如何：生成代码度量数据](../code-quality/how-to-generate-code-metrics-data.md)
- [使用 "代码度量结果" 窗口](../code-quality/working-with-code-metrics-data.md)