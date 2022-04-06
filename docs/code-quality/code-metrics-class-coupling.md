---
title: 代码度量 - 类耦合
ms.date: 1/8/2021
description: 了解 Visual Studio 中代码度量的类耦合度量。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: d655878ac1a2630d0670c56c4d0122917b8374d9
ms.sourcegitcommit: 9bac2e4017d909e6823c09a0ce59513b0f8bbb54
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2022
ms.locfileid: "141483558"
---
# <a name="code-metrics---class-coupling"></a>代码度量 - 类耦合

类耦合也称为对象间耦合 (CBO)，最初由 [CK94](#ck94) 定义。 基本上，类耦合是衡量单个类使用多少类的指标。 对于该度量，数字大表示不佳，数字小则通常表示良好。 类耦合经证明是可准确预测软件故障的指标，最新研究表明，上限值 9 是最有效的 [S2010](#s2010)。

根据 Microsoft 的文档，类耦合“通过参数、本地变量、返回类型、方法调用、泛型实例化或模板实例化、基类、接口实现、在外部类型上定义的字段和特性修饰来度量与唯一类的耦合度。 良好的软件设计要求类型和方法应具有高内聚和低耦合度。 高耦合度表明设计与其他类型存在许多相互依存关系，难以重用和维护。”

耦合与内聚的概念明显相关。 为确保本次讨论切题，我们不会深入讨论内聚，仅给出 [KKLS2000](#kkls2000) 中的简要定义：

“模块内聚由 Yourdon 和 Constantine 引入，表示‘模块的内部元素彼此之间的联系或关联程度’[YC79](#yc79)。 如果一个模块代表一个任务 […]，并且其中的所有元素都为该单一任务助力，则该模块为高内聚。 他们将内聚描述为设计属性而不是代码，并且是一个可用于预测可重用性、可维护性和可变性的属性。”

## <a name="class-coupling-example"></a>类耦合示例

接下来看看实践中的类耦合。 首先，新建控制台应用程序并新建名为 Person 且包含一些属性的类，然后立即计算代码度量：

![类耦合示例 1](media/class-coupling-example-1.png)

请注意类耦合为 0，因为该类不使用任何其他类。 现在以创建 Person 实例并设置属性值的方式，创建另一个名为 PersonStuff 的类。 再次计算代码度量：

![类耦合示例 2](media/class-coupling-example-2.png)

了解类耦合值的增加原理。 另请注意，无论设置多少个属性，类耦合值只会增加 1，而不是其他值。 对于这个度量，无论每个类使用多么频繁，类耦合只对每个类进行一次度量。 此外，你是否注意到 `DoSomething()` 的值为 1，构造函数 `PersonStuff()` 的值为 0？ 目前，构造函数中没有使用另一个类的代码。

如果将使用另一个类的代码输入构造函数中会怎么样？ 以下就是示例：

![类耦合示例 3](media/class-coupling-example-3.png)

现在，构造函数显然具有使用另一个类的代码，并且类耦合度量说明了这一点。 同样，可以看到 `PersonStuff()` 的整体类耦合为 1，`DoSomething()` 也为 1，这表明无论多少内部代码使用某一外部类，对整体而言，仅在使用这一个外部类。

接下来，创建另一个新类。 为这个类命名并为其创建一些属性：

![类耦合示例 - 添加新类](media/class-coupling-example-add-new-class.png)

现在，在 `PersonStuff` 类中的 `DoSomething()` 方法中使用该类并再次计算代码度量：

![类耦合示例 4](media/class-coupling-example-4.png)

如你所见，PersonStuff 类的类耦合上升为 2，如果深入研究该类，你会发现 `DoSomething()` 方法的耦合度最高，而构造函数仍然仅使用 1 个类。  通过这些度量，可以查看指定类的整体最大数，并深入了解每个成员的详细信息。

## <a name="the-magic-number"></a>幻数

与圈复杂度一样，对所有组织均不存在限制。 但 [S2010](#s2010) 确实表明限制为 9 是最佳方案：

“因此，我们认为阈值 [...] 最有效。 这些阈值（对于单个成员）为 CBO = 9[...]。” （着重强调）

## <a name="code-analysis"></a>代码分析

代码分析包括可维护性规则的类别。 有关详细信息，请参阅[可维护性规则](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings)。 使用旧式代码分析时，扩展设计指南规则集包含一个可维护性区域：

![类耦合扩展设计指南规则](media/class-coupling-extended-design-guideline-rules.png)

可维护性区域内是类耦合的规则：

![类耦合规则](media/class-coupling-maintainability-area-rules.png)

类耦合过高时，此规则会发出警告。 有关详细信息，请参阅 [CA1506：避免类耦合过高](/dotnet/fundamentals/code-analysis/quality-rules/ca1506)。

## <a name="citations"></a>引文

### <a name="ck94"></a>CK94

Chidamber, S. R. 和 Kemerer, C. F. 1994。 面向对象设计的度量套件（《IEEE 软件工程汇刊》，第 20 卷， 第 6 期）。 于 2011 年 5 月 14 日检索自匹兹堡大学网站：[http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf](http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf)

### <a name="kkls2000"></a>KKLS2000

Kabaili, H.、Keller, R.、Lustman, F. 和 Saint-Denis, G. (2000)。 类内聚回顾：对工业系统的实证研究（关于面向对象软件工程中的定量方法的研讨会记录）。 于 2011 年 5 月 20 日检索自蒙特利尔大学网站 [http://www.iro.umontreal.ca/~sahraouh/qaoose/papers/Kabaili.pdf](http://www.iro.umontreal.ca/~sahraouh/qaoose/papers/Kabaili.pdf)

### <a name="sk2003"></a>SK2003

Subramanyam, R. 和 Krishnan, M. S. (2003). 面向对象设计复杂度的 CK 度量的实证分析：软件缺陷的影响（《IEEE 软件工程汇刊》，第 29 卷， 第 4 期）。

### <a name="s2010"></a>S2010

Shatnawi, R. (2010)。 开源系统中面向对象度量的可接受风险级别的定量研究（《IEEE 软件工程汇刊》，第 36 卷， 第 2 期）。

### <a name="yc79"></a>YC79

Edward Yourdon 和 Larry L. Constantine。 结构化设计。 1979 年，新泽西州恩格尔伍德克利夫斯，普伦蒂斯·霍尔出版社。
