---
title: 为负载测试添加阈值规则
description: 了解负载测试中的阈值规则，它可将一个性能计数器值与一个常数值或另一个性能计数器值进行比较。
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, monitoring
- load tests, thresholds
- load tests, analyzing
- thresholds in load tests
ms.assetid: 3d8fac8f-426f-4155-9ced-f7cd4c79792c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.openlocfilehash: fb6d40558acac6c51f353925b7e8a5b5453f611a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641419"
---
# <a name="how-to-add-a-threshold-rule-using-the-load-test-editor"></a>如何：使用负载测试编辑器添加阈值规则

负载测试中的阈值规则将一个性能计数器值与一个常数值或另一个性能计数器值进行比较。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-add-a-threshold-rule"></a>添加阈值规则

1. 打开一个负载测试。

2. 在负载测试编辑器中展开“计数器集”节点。

3. 在其中一个计数器集中展开一种“计数器类别”。 例如，可以选择“LoadTest:Scenario”。 展开该节点。

4. 右键单击其中一个计数器，例如“LoadTest:Scenario”下的“用户负载”。 选择“添加阈值规则”。

     “添加阈值规则”对话框随即显示。

5. 可以从两类规则中进行选择：“比较常数”规则和“比较计数器”规则。 选择适当的类型并对值进行设置。

    > [!NOTE]
    > 将“如果超过则发出警报”属性设置为“True”，指示高于阈值会出现问题；或者设为“False”，指示低于阈值会出现问题。

## <a name="see-also"></a>另请参阅

- [分析阈值规则冲突](../test/analyze-threshold-rule-violations-in-load-tests.md)
- [为负载测试中的计算机指定计数器集和阈值规则](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
