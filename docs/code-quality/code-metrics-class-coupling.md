---
title: 代码指标 - 类耦合
ms.date: 1/8/2021
description: 了解代码中代码指标的类耦合Visual Studio。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 6c9ff474cfdc8c572143145c642bc42e899b6516
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122129956"
---
# <a name="code-metrics---class-coupling"></a>代码指标 - 类耦合

类耦合还通过名称"对象之间的耦合 (CBO) 最初由 [CK94 定义](#ck94)。 基本上，类耦合是单个类使用的类数的度量值。 数字高则错误，而低数字通常很符合此指标。 类耦合已证明是软件故障的准确预测器，最近的研究表明，上限值 9 是最高效的[S2010。](#s2010)

根据 Microsoft 文档，类耦合"通过参数、局部变量、返回类型、方法调用、泛型或模板实例化、基类、接口实现、在外部类型上定义的字段以及属性修饰来测量与唯一类的耦合。 良好的软件设计规定类型和方法应具有高内聚和低耦合性。 高耦合指示设计难以重用和维护，因为它与其他类型存在许多相互依赖关系。"

耦合和内聚的概念明显相关。 为了继续此主题讨论，我们不会深入探讨，除了提供 [CLLS2000](#kkls2000)的简要定义外，我们将不会深入探讨：

"模块内聚由 Yourdon 和 Constantine 引入为"模块的内部元素彼此紧密绑定或相关["YC79。](#yc79) 如果模块只表示一个任务 ，则模块具有强内聚性 ，并且其所有元素都参与此单个任务。 它们将内聚描述为设计属性而不是代码，以及可用于预测可重复性、可维护性和可更改性的属性。"

## <a name="class-coupling-example"></a>类耦合示例

让我们看看类耦合在操作中。 首先，创建新的控制台应用程序，并创建一个包含一些属性的名为 Person 的新类，然后立即计算代码指标：

![类耦合示例 1](media/class-coupling-example-1.png)

请注意，类耦合为 0，因为此类不使用任何其他类。 现在，使用创建 Person 实例并设置属性值的方法创建另一个称为 PersonStuff 的类。 再次计算代码指标：

![类耦合示例 2](media/class-coupling-example-2.png)

了解类耦合值如何增加？ 另请注意，无论设置多少个属性，类耦合值只增加 1，而不是其他值。 无论使用多少类，类耦合都只测量此指标的每个类一次。 此外，你能否看到 具有 `DoSomething()` 1，但构造函数 的 值为 `PersonStuff()` 0？ 构造函数中当前没有使用另一个类的代码。

如果将代码放在使用了另一个类的构造函数中，该做什么？ 下面是你获得：

![类耦合示例 3](media/class-coupling-example-3.png)

现在，构造函数清楚地具有使用另一个类的代码，类耦合指标显示了这一事实。 同样，可以看到 的总体类耦合度为 1，也是 1，以表明无论使用多少内部代码，都只使用了一个 `PersonStuff()` `DoSomething()` 外部类。

接下来，创建另一个新类。 为此类指定一些名称，并在此名称内创建一些属性：

![类耦合示例 - 添加新类](media/class-coupling-example-add-new-class.png)

现在，在 类的 `DoSomething()` 方法中使用 `PersonStuff` 类，并再次计算代码指标：

![类耦合示例 4](media/class-coupling-example-4.png)

如你所见，PersonStuff 类的类耦合度最高为 2，如果钻取到 类，可以看到该方法的耦合度最高，但构造函数仍只使用 `DoSomething()` 1 个类。  使用这些指标，可以看到给定类的总体最大数量，并按成员向下钻取详细信息。

## <a name="the-magic-number"></a>幻数

与循环复杂性一样，没有适合所有组织的限制。 但是 [，S2010](#s2010) 确实指示限制为 9 是最佳限制：

"因此，我们考虑阈值 [...]作为最有效的 。 对于单个 (成员，这些阈值) CBO = 9[...]"。  (添加了) 

## <a name="code-analysis"></a>代码分析

代码分析包括可维护性规则的类别。 有关详细信息，请参阅可 [维护性规则](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings)。 使用旧代码分析时，扩展设计准则规则集包含可维护性区域：

![类耦合扩展设计准则规则](media/class-coupling-extended-design-guideline-rules.png)

在可维护性区域中，是类耦合的规则：

![类耦合规则](media/class-coupling-maintainability-area-rules.png)

当类耦合过多时，此规则发出警告。 有关详细信息，请参阅 [CA1506：避免过度类耦合](/dotnet/fundamentals/code-analysis/quality-rules/ca1506)。

## <a name="citations"></a>引文

### <a name="ck94"></a>CK94

Chidamber， S. R. & Kemerer， C. F.  (1994) 。 面向面向对象的设计的指标套件 (软件工程上的 IEEE 事务，Vol.20， No. 6) 。 检索时间：2011 年 5 月 14 日，来自以下大学网站： [http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf](http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf)

### <a name="kkls2000"></a>CALLS2000

Kabaili， H.， Keller， R.， Lustman， F.， and Saint-Denis， G. (2000) 。 类内聚重新访问：有关工业系统的经验 (软件工程领域定量方法研讨会Object-Oriented研讨会) 。 检索自 2011 年 5 月 20 日，来自州/省/市 [http://www.iro.umontreal.ca/~sahraouh/qaoose/papers/Kabaili.pdf](http://www.iro.umontreal.ca/~sahraouh/qaoose/papers/Kabaili.pdf)

### <a name="sk2003"></a>SK2003

Subramanyam， R. & Krishnan， M. S. (2003). 设计复杂性的 CK 指标的经验分析Object-Oriented：软件工程上的软件缺陷 (IEEE 事务的影响，Vol. 29， No. 4) 。 检索时间：2011 年 5 月 14 日，来自美国大学）的一个网站 [http://moosehead.cis.umassd.edu/cis580/readings/OO_Design_Complexity_Metrics.pdf](http://moosehead.cis.umassd.edu/cis580/readings/OO_Design_Complexity_Metrics.pdf)

### <a name="s2010"></a>S2010

Shatnawi， R. (2010) . 软件工程上的 Object-Oriented Systems Open-Source IEEE (中可接受指标风险级别的定量调查，Vol. 36， No. 2) 。

### <a name="yc79"></a>YC79

Edward Yourdon 和管理 L.Constantine。 结构化设计。 Prentice Hall， Englewood 一文，N.J.， 1979 年。