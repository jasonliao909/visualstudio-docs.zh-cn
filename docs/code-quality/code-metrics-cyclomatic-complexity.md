---
title: 代码度量 - 圈复杂度
ms.date: 5/7/2021
description: 了解 Visual Studio 中代码度量的圈复杂度度量。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: b8de7119eb232afb904896cfedbbece9bbf2f8d5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601337"
---
# <a name="code-metrics---cyclomatic-complexity"></a>代码度量 - 圈复杂度

使用代码度量时，最难理解的一项似乎是圈复杂度。 简单而言，圈复杂度的数字越低越好，数字越高则相反。 可使用圈复杂度来了解对任何给定代码进行测试、维护或故障排除的难度，以及指示代码生成错误的可能性。 大体而言，我们通过计算源代码中做出的决策数来确定圈复杂度的值。 本文首先介绍一个简单的圈复杂度示例，帮助你快速了解概念，然后介绍一些有关实际使用情况和建议的限制的附加信息。 最后，还提供了一部分引文可用于进一步探讨此主题。

## <a name="example"></a>示例

圈复杂度定义为测量“源代码函数中的决策逻辑数量”[NIST235](#nist235)。 简而言之，在代码中要做出的决策就多，就越复杂。

我们来看一下实际的效果。 创建一个新的控制台应用程序，并立即通过转到“分析”>“计算解决方案的代码度量”来计算代码度量。

![圈复杂度示例 1](media/cyclomatic-complexity-example-1.png)

请注意，圈复杂度为 2（可能的最低值）。 如果添加非决策代码，请注意复杂度不会变化：

![圈复杂度示例 2](media/cyclomatic-complexity-example-2.png)

如果添加一个决策，圈复杂度值将增加 1：

![圈复杂度示例 3](media/cyclomatic-complexity-example-3.png)

将 if 语句更改为需要做出 4 个决策的 switch 语句时，它将从原来的 2 变为 6：

![圈复杂度示例 4](media/cyclomatic-complexity-example-4.png)

接下来看一个（假设的）更大的代码库。

![圈复杂度示例 5](media/cyclomatic-complexity-example-5.png)

请注意，在向下钻取到 Products_Related 类时，大多数项的值都为 1，但其中一些项的复杂度为 5。 这本身可能不是什么大问题，但鉴于大多数其他成员在同一类中的值都为 1，因此应仔细查看这两项，了解其中包含的内容。 为此，可右键单击该项，然后从上下文菜单中选择“转到源代码”。 仔细查看 `Product.set(Product)`：

![圈复杂度示例 6](media/cyclomatic-complexity-example-6.png)

鉴于所有这些 if 语句，因此圈复杂度为 5。 此时，你可以确定这是可接受的复杂度级别，或者可以重构来降低复杂度。

## <a name="the-magic-number"></a>幻数

与此行业中的许多度量一样，圈复杂度对所有组织均不存在限制。 但 [NIST235](#nist235) 确实表示限制为 10 是理想起点：

“但是，用作限制的确切数字仍然存在一些争议。 McCabe 提出的最初限制为 10，这一数字有大量的支持证据，但限制为 15 也有过成功的案例。 对于与典型项目相比具有多项操作优势（例如经验丰富的员工、正式设计、现代编程语言、结构化编程、代码演练和全面的测试计划）的项目，应保留大于 10 的限制。 换句话说，一个组织可以选择一个大于 10 的复杂度限制，但前提是组织清楚自己在做什么并且愿意投入更复杂模块所需的额外测试工作。” [NIST235](#nist235)

## <a name="cyclomatic-complexity-and-line-numbers"></a>圈复杂度和行号

仅查看代码行数本身，充其量只是对代码质量的一个非常广泛的预测。 函数中的代码行数越多，出错的可能性就越大，这一观点有一定的基本道理。 但是，将圈复杂度与代码行相结合时，可以更清楚地了解错误发生的可能性。

如 NASA 的软件保障技术中心 (SATC) 所述：

“SATC 发现最有效的评估是将大小和（圈）复杂度相结合。 复杂度高的大型模块往往具有最低的可靠性。 复杂度低的小型模块也具有可靠性风险，因为它们往往是非常简洁的代码，难以更改或修改。” [SATC](#satc)

## <a name="code-analysis"></a>代码分析

代码分析包括可维护性规则的类别。 有关详细信息，请参阅[可维护性规则](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings)。 使用旧式代码分析时，扩展设计指南规则集包含一个可维护性区域：

![圈复杂度设计指南规则集](media/cyclomatic-complexity-design-guidelines.png)

在可维护性区域中，有一个复杂度规则：

![圈复杂度可维护性规则](media/cyclomatic-complexity-maintainability-rule.png)

圈复杂度达到 25 时，此规则会发出警告，因此该规则有助于防止过高的复杂度。 若要详细了解此规则，请参阅 [CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502)

## <a name="putting-it-all-together"></a>总结

最重要的是，复杂度数字高意味着随着维护和故障排除时间的增加，出现错误的可能性更大。 请仔细查看任何具有较高复杂度的函数，并确定是否应重构这些函数，使其复杂度降低。

## <a name="citations"></a>引文

### <a name="mccabe5"></a>MCCABE5

McCabe, T. and A. Watson (1994), Software Complexity (CrossTalk: The Journal of Defense Software Engineering).

### <a name="nist235"></a>NIST235

Watson, A. H., & McCabe, T. J. (1996). Structured Testing: A Testing Methodology Using the Cyclomatic Complexity Metric (NIST Special Publication 500-235). 2011 年 5 月 14 日检索自 McCabe Software 网站：[http://www.mccabe.com/pdf/mccabe-nist235r.pdf](http://www.mccabe.com/pdf/mccabe-nist235r.pdf)

### <a name="satc"></a>SATC

Rosenberg, L., Hammer, T., Shaw, J. (1998). Software Metrics and Reliability (Proceedings of IEEE International Symposium on Software Reliability Engineering). 2011 年 5 月 14 日检索自 Penn State University 网站[http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.104.4041&rep=rep1&type=pdf](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.104.4041&rep=rep1&type=pdf)