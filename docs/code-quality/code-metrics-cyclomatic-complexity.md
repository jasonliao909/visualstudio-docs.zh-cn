---
title: 代码指标 - 循环复杂性
ms.date: 5/7/2021
description: 了解代码中代码指标的循环复杂性Visual Studio。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 949944b7bec47bf952e51ede2cb5593cb84e407ba1e7554765a5ce33edaded9f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121240960"
---
# <a name="code-metrics---cyclomatic-complexity"></a>代码指标 - 循环复杂性

使用代码指标时，最不了解的项之一似乎是循环复杂性。 本质上，由于循环复杂性，数字越高，错误就越高，数字就越高。 可以使用循环复杂性来了解任何给定代码测试、维护或故障排除的复杂性，以及指示代码生成错误的可能性。 从较高层面看，我们通过计算源代码中做出的决策数来确定循环复杂性的价值。 本文首先介绍一个简单的循环复杂性示例，以快速理解概念，然后查看有关实际使用情况和建议的限制的一些附加信息。 最后，有一部分引文可用于深入探讨此主题。

## <a name="example"></a>示例

循环复杂性定义为度量"源代码函数中的决策逻辑量["NIST235。](#nist235) 简而言之，在代码中必须做出的决策就多，它越复杂。

让我们看一下它的操作。 创建新的控制台应用程序，并立即通过"分析""计算解决方案> **计算代码指标"，立即计算代码指标**。

![循环复杂性示例 1](media/cyclomatic-complexity-example-1.png)

请注意，循环复杂度为 2 (可能的最低值) 。 如果添加非决策代码，请注意复杂性不会变化：

![循环复杂性示例 2](media/cyclomatic-complexity-example-2.png)

如果添加决策，则循环复杂性值将增加 1：

![循环复杂性示例 3](media/cyclomatic-complexity-example-3.png)

将 if 语句更改为具有 4 个决策的 switch 语句时，它将从原始的 2 更改为 6：

![循环复杂性示例 4](media/cyclomatic-complexity-example-4.png)

让我们看一下一个假设 () 代码库。

![循环复杂性示例 5](media/cyclomatic-complexity-example-5.png)

请注意，在向下钻取到 Products_Related 类时，大多数项的值为 1，但其中一些项的复杂度为 5。 这本身可能不是大问题，但鉴于大多数其他成员在同一个类中具有 1，你一定要仔细查看这两个项，并查看它们中是什么。 为此，可以右键单击该项，然后从上下文菜单中选择"转到源代码"。 请仔细查看 `Product.set(Product)` ：

![循环复杂性示例 6](media/cyclomatic-complexity-example-6.png)

给定所有 if 语句后，可以看到为何循环复杂性为 5。 此时，你可以确定这是可接受的复杂性级别，或者可以重构以降低复杂性。

## <a name="the-magic-number"></a>幻数

与此行业中的许多指标一样，没有适合所有组织的确切的循环复杂性限制。 但是 [，NIST235](#nist235) 确实表示限制为 10 是一个很好的起点：

"但是，用作限制的精确数字仍有点不精确。 McCabe 建议的原始限制 10 具有大量支持证据，但限制也已成功使用，最高为 15。 对于与典型项目相比具有多种操作优势的项目，应保留超过 10 个的限制，例如经验丰富的员工、正式设计、现代编程语言、结构化编程、代码演练和全面的测试计划。 换句话说，组织可以选取大于 10 的复杂性限制，但只有在它确定它知道它正在做什么并且愿意投入更复杂的模块所需的额外测试工作时，它才能选择。 [NIST235](#nist235)

## <a name="cyclomatic-complexity-and-line-numbers"></a>循环复杂性和行号

仅查看代码行数本身是代码质量的一种非常广泛的预测器。 有一些基本事实，即函数中的代码行数越多，出错的可能性就大。 但是，将循环复杂性与代码行相结合时，可以更清楚地了解错误的可能性。

如 NASA 软件保障技术中心 (SATC) 所述：

"SATC 发现最有效的评估是大小和循环 (复杂性) 的组合。 具有高复杂性和较大大小的模块往往具有最低的可靠性。 具有低大小和高复杂性的模块也是可靠性风险，因为它们往往非常复杂的代码，难以更改或修改。" [SATC](#satc)

## <a name="code-analysis"></a>代码分析

代码分析包括可维护性规则的类别。 有关详细信息，请参阅可 [维护性规则](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings)。 使用旧代码分析时，扩展设计准则规则集包含可维护性区域：

![循环复杂性设计准则规则集](media/cyclomatic-complexity-design-guidelines.png)

在可维护性区域中，有一个复杂性规则：

![循环复杂性可维护性规则](media/cyclomatic-complexity-maintainability-rule.png)

当循环复杂性达到 25 时，此规则发出警告，这样有助于避免过于复杂。 若要详细了解规则，请参阅 [CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502)

## <a name="putting-it-all-together"></a>全部放在一起

最后一点就是，高复杂性数字意味着出错的可能性更大，同时需要增加维护和故障排除的时间。 请仔细查看任何具有较高复杂性的函数，并确定是否应重构这些函数，使其不太复杂。

## <a name="citations"></a>引文

### <a name="mccabe5"></a>MCCABE5

McCabe， T. and A. Watson (1994) ， Software Complexity (CrossTalk： The Journal of Defense Software Engineering) .

### <a name="nist235"></a>NIST235

Watson， A. H.， & McCabe， T. J.  (1996) 。 结构化测试：使用 NIST 特别出版物 500-235 (循环复杂性指标的测试) 。 从 McCabe Software 网站检索到的 2011 年 5 月 14 日： [http://www.mccabe.com/pdf/mccabe-nist235r.pdf](http://www.mccabe.com/pdf/mccabe-nist235r.pdf)

### <a name="satc"></a>SATC

Rosenberg， L.， Hammer， T.， 一维， J. (1998) 。 软件指标和可靠性 (IEEE 国际软件可靠性工程研讨会) 。 从 Penn State University 网站检索到的 2011 年 5 月 14 日： [http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.104.4041&rep=rep1&type=pdf](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.104.4041&rep=rep1&type=pdf)