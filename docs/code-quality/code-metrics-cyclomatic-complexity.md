---
title: 代码度量值-圈复杂度
ms.date: 5/7/2021
description: 了解 Visual Studio 中代码度量值的圈复杂度指标。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: b8de7119eb232afb904896cfedbbece9bbf2f8d5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601337"
---
# <a name="code-metrics---cyclomatic-complexity"></a>代码度量值-圈复杂度

使用代码度量值时，最不了解的项中的一个可能是圈复杂度。 实质上，具有圈复杂度，较高的数字很差，数字越小。 您可以使用圈复杂度来了解任何给定代码是如何测试、维护或故障排除的，以及代码生成错误的可能性的指示。 从较高层次来看，我们通过计算在源代码中所做的决策数来确定圈复杂度的值。 在本文中，我们首先介绍了圈复杂度的简单示例，以快速了解该概念，然后查看有关实际使用情况和建议限制的一些附加信息。 最后，还提供了一个可用于深入了解此主题的引文部分。

## <a name="example"></a>示例

圈复杂度定义为 " [NIST235](#nist235)中的决策逻辑量"。 简而言之，要在代码中做出的决策越多，就越复杂。

让我们看看它的运行情况。 创建新的控制台应用程序，并通过 **分析 > 计算解决方案的代码度量值**，立即计算代码指标。

![圈复杂度示例1](media/cyclomatic-complexity-example-1.png)

请注意，圈复杂度为 2 (最小值为) 。 如果添加非决策代码，请注意复杂性不会发生变化：

![圈复杂度示例2](media/cyclomatic-complexity-example-2.png)

如果添加决策，圈复杂度值将向上提升1：

![圈复杂度示例3](media/cyclomatic-complexity-example-3.png)

将 if 语句更改为具有4个决策的 switch 语句时，它将从原始2到6：

![圈复杂度示例4](media/cyclomatic-complexity-example-4.png)

让我们看一看 (假设) 较大的基本代码。

![圈复杂度示例5](media/cyclomatic-complexity-example-5.png)

请注意，当您向下钻取到 Products_Related 类时，大部分项的值为1，但其中有一些值的复杂性为5。 这可能并不是一个大问题，但是，由于大多数其他成员在同一类中都有1个，您应该清楚地了解这两个项，并查看其中的内容。 若要执行此操作，请右键单击该项目，然后从上下文菜单中选择 " **切换到源代码** "。 详细了解 `Product.set(Product)` 以下内容：

![圈复杂度示例6](media/cyclomatic-complexity-example-6.png)

对于所有 if 语句，可以看到圈复杂度为5的原因。 此时，您可能会决定这是一个可接受的复杂程度，或者您可能重构以降低复杂性。

## <a name="the-magic-number"></a>幻数

与此行业中的许多指标一样，没有与所有组织相适应的精确圈复杂度限制。 但是， [NIST235](#nist235) 确实表明限制为10是一个很好的起点：

"要用作限制的准确数字仍有争议。 由于 McCabe 的建议，原始限制10已有重要的支持证据，但已成功使用了高达15的限制。 对于比典型项目具有多个操作优势的项目，应保留超过10个的限制，例如经验丰富的人员、正式设计、新式编程语言、结构化编程、代码演练和全面的测试计划。 换句话说，组织可以选择大于10的复杂性限制，但前提是它确实知道它正在执行什么操作，并愿意投入更复杂的模块所需的额外测试工作。 " [NIST235](#nist235)

## <a name="cyclomatic-complexity-and-line-numbers"></a>圈复杂度和行号

只需查看代码的行数，就能获得极大的代码质量预测。 有一些基本的概念，即函数中的代码行越多，出现错误的可能性就越大。 但是，当你将圈复杂度与代码行结合使用时，你可以更清楚地了解可能出现的错误。

如软件保障技术中心所述 (NASA 上的 SATC) ：

"SATC 发现，最有效的评估是大小和 (圈) 复杂性的组合。 具有高复杂性和较大大小的模块往往具有最低的可靠性。 低和高复杂性的模块也是一种可靠性风险，因为它们往往是非常简要的代码，难于更改或修改。 " [SATC](#satc)

## <a name="code-analysis"></a>代码分析

代码分析包括一类可维护性规则。 有关详细信息，请参阅可 [维护性规则](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings)。 使用旧代码分析时，扩展的设计准则规则集包含可维护性区域：

![圈复杂度设计准则规则集](media/cyclomatic-complexity-design-guidelines.png)

在可维护性区域内，是一种复杂性的规则：

![圈复杂度可维护性规则](media/cyclomatic-complexity-maintainability-rule.png)

当圈复杂度达到25时，此规则会发出警告，因此它可以帮助你避免过多的复杂性。 若要了解有关规则的详细信息，请参阅 [CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502)

## <a name="putting-it-all-together"></a>将其全部放在一起

关键在于，较高的复杂性数字表示更多的错误概率，并增加了维护和故障排除的时间。 仔细查看具有高复杂性的所有函数，并决定是否应重构这些功能，以使它们不太复杂。

## <a name="citations"></a>引文

### <a name="mccabe5"></a>MCCABE5

McCabe、和 Watson (1994) ，软件复杂性 (CrossTalk：防卫 Software 工程) 的日志。

### <a name="nist235"></a>NIST235

Watson，& McCabe，T. J。  (1996) 。 结构化测试：使用圈复杂度指标 (NIST 特殊发布 500-235) 的测试方法。 从 McCabe Software 网站检索到5月 14 2011 日： [http://www.mccabe.com/pdf/mccabe-nist235r.pdf](http://www.mccabe.com/pdf/mccabe-nist235r.pdf)

### <a name="satc"></a>SATC

Rosenberg、L.、Hammer、Shaw、、 (1998) 。 软件指标和可靠性 (软件可靠性工程设计) 上的 IEEE 国际研讨会的诉讼。 从 Microsoft 状态大学网站检索到5月14日2011： [http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.104.4041&rep=rep1&type=pdf](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.104.4041&rep=rep1&type=pdf)