---
title: 代码指标 - 继承深度
ms.date: 1/8/2021
description: 了解代码中代码指标的继承指标Visual Studio。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 6b212f349435f395df9e3acb8a802f51de949f63ae2c494dc30fb08c7091c517
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121405541"
---
# <a name="code-metrics---depth-of-inheritance-dit"></a>代码指标 - DIT (继承) 

本文介绍专为面向对象的分析而设计的指标之一：继承深度。 继承深度（也称为继承树深度 (DIT) ）定义为"从节点到树根的最大长度["CK。](#ck) 可以通过一个简单的示例来查看这一点。 创建新的类库项目，在编写任何代码之前，通过选择"分析">为解决方案计算代码指标"来计算 **代码指标**。

![继承深度示例 1](media/depth-of-inheritance-example-1.png)

由于所有类都继承自 `System.Object` ，因此深度当前为 1。 如果从此类继承并检查新类，则可以看到结果：

![继承深度示例 2](media/depth-of-inheritance-example-2.png)

请注意，树中节点的下 (`Class2` 在这种情况下) ，继承深度越高。 你可以继续创建子项目，使深度增加，只要愿意。

## <a name="assumptions"></a>假设

继承深度基于 [CK](#ck)的三个基本假设：

1. 层次结构中的类越深，它可能继承的方法就越大，因此很难预测其行为。

2. 深度树涉及更大的设计复杂性，因为涉及更多的类和方法。

3. 树中的更深层类具有更大的重新使用继承方法的可能性。

假设 1 和 2 告诉你，深度数字越高，则错误。 如果这是它的结束位置，则你会状态良好;但是，假设 3 表示深度数字越高，就适合重用代码。

## <a name="analysis"></a>分析

下面是读取深度指标的一些说明：

- 深度的低数字

  深度数字低意味着复杂性较低，但通过继承减少代码重用的可能性。

- 深度数字较高

  深度数字较高意味着通过继承重用代码的可能性更大，但复杂性更高，代码中的错误概率较高。

## <a name="code-analysis"></a>代码分析

代码分析包括可维护性规则的类别。 有关详细信息，请参阅可 [维护性规则](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings)。 使用旧代码分析时，扩展设计准则规则集包含可维护性区域：

![继承设计准则规则集的深度](media/depth-of-inheritance-design-guidelines.png)

在可维护性区域中，是继承规则：

![继承可维护性规则的深度](media/depth-of-inheritance-maintainability-rule.png)

此规则在继承深度达到或大于 6 时发出警告，因此，这是一个有助于防止过度继承的好规则。 若要详细了解规则，请参阅 [CA1501](/dotnet/fundamentals/code-analysis/quality-rules/ca1501)。

## <a name="putting-it-all-together"></a>全部放在一起

DIT 值高意味着出错的可能性也很高，低值会降低出错的可能性。 DIT 的高值表示通过继承重用代码的可能性更大，低值表示利用继承可以减少代码重用。 由于缺少足够的数据，当前没有接受的 DIT 值标准。 即使是最近所做的研究也找不到足够的数据来确定一个可行的数字，该数字可以用作此指标 [Shatnawi](#shatnawi)的标准数字。 尽管没有经验证据支持它，但一些资源建议 DIT 的上限应为 5 或 6 左右。 例如，请参阅 [http://www.devx.com/architect/Article/45611](http://www.devx.com/architect/Article/45611) 。

## <a name="citations"></a>引文

### <a name="ck"></a>CK

Chidamber， S. R. & Kemerer， C. F.  (1994) 。 面向面向对象的设计的指标套件 (软件工程上的 IEEE 事务，Vol. 20， No. 6) 。 检索时间：2011 年 5 月 14 日，来自美国大学网站： [http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf](http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf)

### <a name="krishnan"></a>Krishnan

Subramanyam， R. & Krishnan， M. S. (2003). 设计复杂性的 CK 指标的经验分析Object-Oriented：软件工程上的软件缺陷 (IEEE 事务的影响，Vol. 29， No. 4) 。 检索时间：2011 年 5 月 14 日，最初从北维萨大学（美国）网站获取 [https://ieeexplore.ieee.org/abstract/document/1191795](https://ieeexplore.ieee.org/abstract/document/1191795)

### <a name="shatnawi"></a>Shatnawi

Shatnawi， R. (2010) . 对软件 Object-Oriented工程上 Open-Source Systems (IEEE 事务中可接受指标的可接受风险级别的定量调查，Vol. 36， No. 2) 。