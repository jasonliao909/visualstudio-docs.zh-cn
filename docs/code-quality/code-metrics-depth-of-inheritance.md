---
title: 代码度量-继承深度
ms.date: 1/8/2021
description: 了解 Visual Studio 中代码度量值的继承深度。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: c08a35a622eeb30a51b4dea2ab4914b0105b01cd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601336"
---
# <a name="code-metrics---depth-of-inheritance-dit"></a>代码度量- (DIT 的继承深度) 

本文介绍专用于面向对象分析的度量值之一：继承深度。 继承深度（也称为继承树 (DIT) ）定义为 "从节点到树根的最大长度" 的 [CK](#ck)。 您可以使用一个简单的示例来了解这一点。 创建新的类库项目，并在编写任何代码之前，通过选择 " **分析 > 为解决方案计算代码度量值**" 来计算代码度量值。

![继承深度示例1](media/depth-of-inheritance-example-1.png)

由于所有类都继承自 `System.Object` ，因此当前深度为1。 如果从此类继承并检查新类，则可以查看结果：

![继承深度示例2](media/depth-of-inheritance-example-2.png)

请注意，在这种情况下，树中的节点越低 (`Class2`) ，继承深度越多。 您可以继续创建子级，并使深度增加所需的数量。

## <a name="assumptions"></a>假设

继承深度依据三个基本假设 [CK](#ck)：

1. 层次结构中的类越多，它可能会继承的方法越多，这使得预测其行为变得更加困难。

2. 更深层的树涉及到更大的设计复杂性，因为涉及到更多的类和方法。

3. 树中的更深层类更有可能重复使用继承的方法。

假设 "1" 和 "2" 会告诉你深度较高的数字已损坏。 如果是这样，则您的工作方式不错;但是，假设值为3表示较高的深度数值适用于可能的代码重用。

## <a name="analysis"></a>分析

下面是读取深度指标的方式：

- 深度下限

  深度较低意味着降低了复杂性，同时也减少了通过继承更少的代码重用。

- 深度较高

  如果深度较高，则表示更有可能通过继承进行代码重用，同时也增加了复杂性，代码中出现错误的可能性更高。

## <a name="code-analysis"></a>代码分析

代码分析包括一类可维护性规则。 有关详细信息，请参阅可 [维护性规则](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings)。 使用旧代码分析时，扩展的设计准则规则集包含可维护性区域：

![继承深度设计准则规则集](media/depth-of-inheritance-design-guidelines.png)

可维护性区域内是继承规则：

![继承可维护性规则深度](media/depth-of-inheritance-maintainability-rule.png)

当继承深度达到6或更大时，此规则会发出警告，因此，这是一个很好的规则，有助于防止过度继承。 若要了解有关规则的详细信息，请参阅 [CA1501](/dotnet/fundamentals/code-analysis/quality-rules/ca1501)。

## <a name="putting-it-all-together"></a>将其全部放在一起

DIT 的高值表示可能出现错误，也可能是低值，这会减少出现错误的可能性。 DIT 的高值通过继承指示更好的代码重用，较低的值建议使用继承来更少地重用代码。 由于没有足够的数据，当前不接受 DIT 值标准。 甚至最近完成的研究没有找到足够的数据来确定可用作此指标 [Shatnawi](#shatnawi)标准数字的有效数字。 尽管没有用于支持它的经验证明，但有几个资源表明大约5或6的 DIT 应为上限。 有关示例，请参阅 [http://www.devx.com/architect/Article/45611](http://www.devx.com/architect/Article/45611) 。

## <a name="citations"></a>引文

### <a name="ck"></a>CK

Chidamber，S. R。 & Kemerer，c。  (1994) 。 用于面向对象的设计的指标套件 (软件工程上的 IEEE 事务， 6) 。 从 Pittsburgh 网站的大学检索到5月14日2011： [http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf](http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf)

### <a name="krishnan"></a>Krishnan

Subramanyam、& Krishnan、M. S。 (2003). Object-Oriented 设计复杂性的 CK 指标的经验分析：软件设计 (IEEE 事务上的软件缺陷的影响， 4) 。 检索到的可能为14，2011，最初从马萨诸塞州 Dartmouth 网站获得 [https://ieeexplore.ieee.org/abstract/document/1191795](https://ieeexplore.ieee.org/abstract/document/1191795)

### <a name="shatnawi"></a>Shatnawi

Shatnawi、 (2010) 。 调查 Open-Source 系统中的 Object-Oriented 指标的可接受风险级别， (软件工程，36，无。 2) 。