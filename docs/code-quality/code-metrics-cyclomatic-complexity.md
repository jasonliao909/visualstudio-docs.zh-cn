---
title: 代码指标 - 循环复杂性
ms.date: 5/7/2021
description: 了解代码中代码指标的循环复杂性Visual Studio。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1798b0faa1b0cf44ae490f5b27571e5466b82ca9
ms.sourcegitcommit: cc66c898ce82f9f1159bd505647f315792cac9fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2021
ms.locfileid: "109682543"
---
# <a name="code-metrics---cyclomatic-complexity"></a>代码指标 - 循环复杂性

使用代码指标时，最不了解的项之一似乎是循环复杂性。 本质上，由于循环复杂性，数字越高，错误就越高，数字就越高。 可以使用循环复杂性来了解任何给定代码测试、维护或故障排除的复杂性，以及指示代码生成错误的可能性。 从较高层面看，我们通过计算源代码中做出的决策数来确定循环复杂性的价值。 本文首先通过一个简单的循环复杂性示例来快速了解概念，然后查看有关实际使用情况和建议的限制的一些附加信息。 最后，有一部分引文可用于深入探讨此主题。

## <a name="example"></a>示例

循环复杂性定义为度量"源代码函数中的决策逻辑量["NIST235。](#nist235) 简而言之，在代码中必须做出的决策就多，它越复杂。

让我们看一下它的操作。 创建新的控制台应用程序，并立即通过"分析""计算解决方案> **计算代码指标"，立即计算代码指标**。

![循环复杂性示例 1](media/cyclomatic-complexity-example-1.png)

请注意，循环复杂度为 2 (可能的最低值) 。 如果添加非决策代码，请注意复杂性不会变化：

![循环复杂性示例 2](media/cyclomatic-complexity-example-2.png)

如果添加决策，则循环复杂性值将增加 1：

![循环复杂性示例 3](media/cyclomatic-complexity-example-3.png)

将 if 语句更改为具有 4 个决策的 switch 语句时，它将从原始的 2 更改为 6：

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

只需查看代码的行数，就能获得极大的代码质量预测。 有一个基本事实，即函数中的代码行数越多，出错的可能性就大。 但是，将循环复杂性与代码行相结合时，可以更清楚地了解错误的可能性。

如 NASA 的 软件保障 技术 (SATC) 所述：

"SATC 发现最有效的评估是大小和循环 (复杂性) 的组合。 具有高复杂性和较大大小的模块往往具有最低的可靠性。 具有低大小和高复杂性的模块也是可靠性风险，因为它们往往非常复杂的代码，难以更改或修改。" [SATC](#satc)

## <a name="code-analysis"></a>代码分析

代码分析包括可维护性规则的类别。 有关详细信息，请参阅可 [维护性规则](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings)。 使用旧代码分析时，扩展设计准则规则集包含可维护性区域：

![循环复杂性设计准则规则集](media/cyclomatic-complexity-design-guidelines.png)

在可维护性区域中，有一个复杂性规则：

![循环复杂性可维护性规则](media/cyclomatic-complexity-maintainability-rule.png)

当循环复杂性达到 25 时，此规则发出警告，因此它可以帮助你避免过于复杂。 若要详细了解规则，请参阅 [CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502)

## <a name="putting-it-all-together"></a>全部放在一起

最后一点就是，高复杂性数字意味着出错的可能性更大，同时需要增加维护和故障排除的时间。 请仔细查看任何具有较高复杂性的函数，并确定是否应重构这些函数，使其不太复杂。

## <a name="citations"></a>引文

### <a name="mccabe5"></a>MCCABE5

McCabe、和 Watson (1994) ，软件复杂性 (CrossTalk：防卫 Software 工程) 的日志。

### <a name="nist235"></a>NIST235

Watson，& McCabe，T. J。  (1996) 。 结构化测试：使用圈复杂度指标 (NIST 特殊发布 500-235) 的测试方法。 从 McCabe Software 网站检索到5月 14 2011 日： [http://www.mccabe.com/pdf/mccabe-nist235r.pdf](http://www.mccabe.com/pdf/mccabe-nist235r.pdf)

### <a name="satc"></a>SATC

Rosenberg、L.、Hammer、Shaw、、 (1998) 。 软件指标和可靠性 (软件可靠性工程设计) 上的 IEEE 国际研讨会的诉讼。 从 Microsoft 状态大学网站检索到5月14日2011： [http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.104.4041&rep=rep1&type=pdf](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.104.4041&rep=rep1&type=pdf)