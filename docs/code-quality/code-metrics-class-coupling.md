---
title: 代码指标 - 类耦合
ms.date: 1/8/2021
description: 了解代码中代码指标的类耦合Visual Studio。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0853b807d3287eb584e76d9640ac98f930edb1a7
ms.sourcegitcommit: cc66c898ce82f9f1159bd505647f315792cac9fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2021
ms.locfileid: "109666804"
---
# <a name="code-metrics---class-coupling"></a>代码指标 - 类耦合

类耦合还按名称"对象之间的耦合 (CBO) 最初由 [CK94 定义](#ck94)。 基本上，类耦合是单个类使用的类数的度量值。 数字高则错误，而低数字通常很符合此指标。 类耦合已证明是软件故障的准确预测器，最近的研究表明，上限值 9 是最高效的[S2010。](#s2010)

根据 Microsoft 文档，类耦合"通过参数、局部变量、返回类型、方法调用、泛型或模板实例化、基类、接口实现、在外部类型上定义的字段以及属性修饰来测量与唯一类的耦合。 良好的软件设计规定类型和方法应具有高内聚和低耦合性。 高耦合表示设计难以重用和维护，因为它与其他类型存在许多相互依赖关系。"

耦合和内聚的概念明显相关。 为了继续此主题讨论，除了提供 [CLLS2000](#kkls2000)的简要定义外，我们不会深入探讨内聚：

"模块内聚由 Yourdon 和 Constantine 引入为"模块的内部元素彼此紧密绑定或相关["YC79。](#yc79) 如果模块只表示一个任务 ，则模块具有强内聚性 ，并且其所有元素都参与此单个任务。 它们将内聚描述为设计属性而不是代码，以及可用于预测可重复性、可维护性和可更改性的属性。"

## <a name="class-coupling-example"></a>类耦合示例

让我们看一下类耦合在操作中。 首先，创建新的控制台应用程序，并创建一个包含一些属性的名为 Person 的新类，然后立即计算代码指标：

![类耦合示例 1](media/class-coupling-example-1.png)

请注意，类耦合为0，因为该类不使用任何其他类。 现在，创建另一个名为 PersonStuff 的类，该方法具有创建 Person 实例并设置属性值的方法。 再次计算代码度量值：

![类耦合示例2](media/class-coupling-example-2.png)

了解类耦合值如何呢？ 另请注意，无论你设置的属性有多少，类耦合值只会向上提升1而不是其他值。 类耦合仅针对此指标测量一次每个类，而不管使用的数量是多少。 此外，你是否可以看到 `DoSomething()` 有1个，但构造函数的 `PersonStuff()` 值为0？ 当前构造函数中没有使用其他类的代码。

如果使用其他类将代码放入构造函数中，该怎么办？ 下面是你获取的内容：

![类耦合示例3](media/class-coupling-example-3.png)

现在构造函数清楚地包含了使用其他类的代码，类耦合指标显示了这一事实。 同样，你可以查看的整体类耦合为 `PersonStuff()` 1， `DoSomething()` 也可以显示为1，表明无论你使用它的内部代码有多少，都只有一个外部类在使用中。

接下来，创建另一个新类。 为此类指定一个名称，并在其中创建一些属性：

![类耦合示例-添加新类](media/class-coupling-example-add-new-class.png)

现在，在 `DoSomething()` 类的方法中使用类 `PersonStuff` ，并再次计算代码度量值：

![类耦合示例4](media/class-coupling-example-4.png)

如您所见，PersonStuff 类的类耦合最多可达2个，并且，如果您钻取到类中，就会看到该 `DoSomething()` 方法的耦合最多，但构造函数仍只使用1个类。  使用这些指标，可以看到给定类的总体最大数量，并按成员向下钻取详细信息。

## <a name="the-magic-number"></a>幻数

与循环复杂性一样，没有适合所有组织的限制。 但是 [，S2010](#s2010) 确实指示限制为 9 是最佳限制：

"因此，我们考虑阈值 [...]作为最有效的 。 对于单个成员 (，这些阈值) CBO = 9[...]"。  (添加了) 

## <a name="code-analysis"></a>代码分析

代码分析包括可维护性规则的类别。 有关详细信息，请参阅可 [维护性规则](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings)。 使用旧代码分析时，扩展设计准则规则集包含可维护性区域：

![类耦合扩展设计准则规则](media/class-coupling-extended-design-guideline-rules.png)

在可维护性区域中，是类耦合的规则：

![类耦合规则](media/class-coupling-maintainability-area-rules.png)

当类耦合过多时，此规则发出警告。 有关详细信息，请参阅 [CA1506：避免过度类耦合](/dotnet/fundamentals/code-analysis/quality-rules/ca1506)。

## <a name="citations"></a>引文

### <a name="ck94"></a>CK94

Chidamber， S. R. & Kemerer， C. F.  (1994) 。 用于面向对象的设计的指标套件 (软件工程上的 IEEE 事务， 6) 。 从 Pittsburgh 网站的大学检索到5月14日2011： [http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf](http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf)

### <a name="kkls2000"></a>KKLS2000

Kabaili、H.、Keller、R.、Lustman、、Denis (2000) 。 类聚合再次检查：有关工业系统的实践调查，请 (《 Object-Oriented 软件工程) 的定量方法的调查。 从 Université de Montréal 网站检索到年5月20日2011 [http://www.iro.umontreal.ca/~sahraouh/qaoose/papers/Kabaili.pdf](http://www.iro.umontreal.ca/~sahraouh/qaoose/papers/Kabaili.pdf)

### <a name="sk2003"></a>SK2003

Subramanyam、& Krishnan、M. S。 (2003). Object-Oriented 设计复杂性的 CK 指标的经验分析：软件设计 (IEEE 事务上的软件缺陷的影响， 4) 。 从马萨诸塞州 Dartmouth 网站的大学那里检索5月14日2011 [http://moosehead.cis.umassd.edu/cis580/readings/OO_Design_Complexity_Metrics.pdf](http://moosehead.cis.umassd.edu/cis580/readings/OO_Design_Complexity_Metrics.pdf)

### <a name="s2010"></a>S2010

Shatnawi、 (2010) 。 调查 Open-Source 系统中的 Object-Oriented 指标的可接受风险级别， (软件工程，36，无。 2) 。

### <a name="yc79"></a>YC79

Edward Yourdon 和 Larry Constantine。 结构化设计。 Prentice 厅、Englewood Cliffs、N.J.、1979。