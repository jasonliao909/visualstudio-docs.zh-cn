---
title: 代码度量 - 继承深度
ms.date: 1/8/2021
description: 了解 Visual Studio 中代码度量的继承度量深度。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 7abe3c943a90a4e5b93be5a43615c0dec916ca78
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139551776"
---
# <a name="code-metrics---depth-of-inheritance-dit"></a>代码度量 - 继承深度 (DIT)

本文介绍专为面向对象分析设计的度量之一：继承深度。 继承深度（也称为继承树深度 (DIT)）定义为“从节点到树根的最大长度”[CK](#ck)。 可以通过一个简单的示例来了解这一点。 创建一个新的类库项目，并在编写任何代码之前，通过选择“分析”>“计算解决方案的代码度量”来计算代码度量。

![继承深度示例 1](media/depth-of-inheritance-example-1.png)

由于所有类都从 `System.Object` 继承，因此当前深度为 1。 如果从该类继承并查看新类，可以看到结果：

![继承深度示例 2](media/depth-of-inheritance-example-2.png)

请注意，树中的节点越低（在本例中为 `Class2`），继承深度就越高。 可以继续创建子元素并根据需要增加深度。

## <a name="assumptions"></a>假设

继承深度基于三个基本假设 [CK](#ck)：

1. 层次结构中的类越深，它可能继承的方法数量就越多，这使得预测其行为变得更加困难。

2. 由于涉及到更多的类和方法，因此更深的树具有更大的设计复杂性。

3. 树中更深的类更有可能重用继承方法。

通过假设 1 和 2 可知，深度数字越小越好。 如果只是这样，就很好；然而，假设 3 表明深度数字越大，就越适合重用代码。

## <a name="analysis"></a>分析

下面是阅读深度度量的方法：

- 深度低

  深度数字越小意味着复杂性越低，但也意味着通过继承重用代码的可能性越小。

- 深度高

  深度数字越大意味着通过继承重用代码的可能性越大，但也意味着复杂性更高并且代码错误率更高。

## <a name="code-analysis"></a>代码分析

代码分析包括可维护性规则的类别。 有关详细信息，请参阅[可维护性规则](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings)。 使用旧式代码分析时，扩展设计指南规则集包含一个可维护性区域：

![继承深度设计指南规则集](media/depth-of-inheritance-design-guidelines.png)

可维护性区域内是继承规则：

![继承深度可维护性规则](media/depth-of-inheritance-maintainability-rule.png)

此规则将在继承深度达到 6 或更大时发出警告，因此该规则非常有助于防止过度继承。 若要详细了解此规则，请参阅 [CA1501](/dotnet/fundamentals/code-analysis/quality-rules/ca1501)。

## <a name="putting-it-all-together"></a>总结

DIT 的高值意味着错误率也更高，低值表示错误率也更低。 DIT 的高值表示通过继承重用代码的可能性更大，低值表示通过继承重用代码的可能性更低。 由于缺乏足够的数据，目前没有公认的 DIT 值标准。 即使是最近进行的研究，也没有找到足够的数据来确定可用作该度量标准数字的有效数字 [Shatnawi](#shatnawi)。 虽然没有实证为其佐证，但有一些资源表明 DIT 值的上限约为 5 或 6。 有关示例，请参阅 [https://www.devx.com/architecture-zone/45611/](https://www.devx.com/architecture-zone/45611/)。

## <a name="citations"></a>引文

### <a name="ck"></a>CK

Chidamber, S. R. 和 Kemerer, C. F. 1994。 面向对象设计的度量套件（《IEEE 软件工程汇刊》，第 20 卷， 第 6 期）。 于 2011 年 5 月 14 日检索自匹兹堡大学网站：[http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf](http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf)

### <a name="krishnan"></a>Krishnan

Subramanyam, R. 和 Krishnan, M. S. (2003). 面向对象设计复杂度的 CK 度量的实证分析：软件缺陷的影响（《IEEE 软件工程汇刊》，第 29 卷， 第 4 期）。 检索于 2011 年 5 月 14 日，最初源自马萨诸塞大学达特茅斯分校网站 [https://ieeexplore.ieee.org/abstract/document/1191795](https://ieeexplore.ieee.org/abstract/document/1191795)

### <a name="shatnawi"></a>Shatnawi

Shatnawi, R. (2010)。 开源系统中面向对象度量的可接受风险级别的定量研究（《IEEE 软件工程汇刊》，第 36 卷， 第 2 期）。
