---
title: 代码指标 - 继承深度
ms.date: 1/8/2021
description: 了解代码中代码指标的继承指标的深度Visual Studio。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1d6ac085463087fc73aac4429488ab475e91c10f
ms.sourcegitcommit: cc66c898ce82f9f1159bd505647f315792cac9fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2021
ms.locfileid: "109682545"
---
# <a name="code-metrics---depth-of-inheritance-dit"></a>代码指标 - DIT (继承) 

本文介绍专为面向对象的分析而设计的指标之一：继承深度。 继承深度（也称为继承树深度 (DIT) ）定义为"从节点到树根的最大长度["CK。](#ck) 可以通过一个简单的示例来查看这一点。 创建新的类库项目，在编写任何代码之前，通过选择"分析">为解决方案计算代码指标"来计算 **代码指标**。

![继承深度示例 1](media/depth-of-inheritance-example-1.png)

由于所有类都继承自 `System.Object` ，因此深度当前为 1。 如果从此类继承并检查新类，则可以看到结果：

![继承深度示例 2](media/depth-of-inheritance-example-2.png)

请注意，树中的节点 `Class2` (，在这种情况下) ，继承深度越高。 你可以继续创建子项目，使深度增加，只要需要。

## <a name="assumptions"></a>假设

继承深度基于 [CK](#ck)的三个基本假设：

1. 层次结构中的类越深，它可能继承的方法就越大，因此很难预测其行为。

2. 深度树涉及更大的设计复杂性，因为涉及更多的类和方法。

3. 树中的更深层类具有更大的重新使用继承方法的可能性。

假设 1 和 2 告诉你，深度数字越高，则错误。 如果这是它的结束位置，则你会状态良好;但是，假设 3 表示深度数字越高，就适合重用代码。

## <a name="analysis"></a>分析

下面是读取深度指标的一些说明：

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

Chidamber， S. R. & Kemerer， C. F.  (1994) 。 面向面向对象的设计的指标套件 (软件工程上的 IEEE 事务，Vol. 20， No. 6) 。 检索时间：2011 年 5 月 14 日，来自以下大学网站： [http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf](http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf)

### <a name="krishnan"></a>Krishnan

Subramanyam， R. & Krishnan， M. S. (2003). 设计复杂性的 CK 指标的经验分析Object-Oriented：软件工程上的软件缺陷 (IEEE 事务的影响，Vol. 29， No. 4) 。 检索时间：2011 年 5 月 14 日，最初从北维萨大学）网站获取 [https://ieeexplore.ieee.org/abstract/document/1191795](https://ieeexplore.ieee.org/abstract/document/1191795)

### <a name="shatnawi"></a>Shatnawi

Shatnawi， R. (2010) . 软件工程上的 Object-Oriented Systems Open-Source IEEE (指标可接受的风险级别的定量调查，Vol. 36， No. 2) 。