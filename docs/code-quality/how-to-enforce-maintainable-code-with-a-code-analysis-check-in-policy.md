---
title: 使用代码分析签入策略
ms.date: 11/04/2016
description: 了解如何使用代码分析签入策略来验证代码是否符合继承、类耦合、可维护性和复杂性标准。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- code analysis, check-in policies
ms.assetid: d1b3b04f-4dd9-40e6-b2d4-b414d33fb647
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 4188a9d12daa5294e6771d3a1b4fc4a37b044521
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601301"
---
# <a name="how-to-enforce-maintainable-code-with-a-code-analysis-check-in-policy"></a>如何：使用代码分析签入策略强制实现代码的可维护性

开发人员可以使用代码指标工具来度量其代码的复杂性和可维护性，但不能在签入策略中调用代码指标。 但是，可以启用 Code Analysis 规则来验证代码是否符合代码指标标准，并通过签入策略强制实施规则。 有关代码指标的详细信息，请参阅[代码指标值](../code-quality/code-metrics-values.md)。

你可以启用“继承深度”、“类耦合度”、“可维护性索引”和“复杂性规则”，以通过 Code Analysis 签入策略强制实施可维护的代码。 所有这些规则均位于 Code Analysis 策略编辑器中的“可维护性规则”类下。

Team Foundation 的版本控制管理员可以将 Code Analysis 可维护性规则添加到签入策略要求。 这些签入策略要求开发人员在启动签入之前，基于这些规则更改运行 Code Analysis。

## <a name="to-open-the-code-analysis-policy-editor"></a>打开 Code Analysis 策略编辑器

1. 在“团队资源管理器”中，右键单击项目，单击“项目设置”，然后单击“源代码管理”  。

     这将显示“源代码管理”对话框。

2. 在“签入策略”选项卡上，单击“添加” 。

     这将显示“添加签入策略”对话框。

3. 在“签入策略”列表中，选中“Code Analysis”复选框，然后单击“确定”  。

     这将显示“Code Analysis 策略编辑器”对话框。

## <a name="to-enable-code-analysis-maintainability-rules"></a>启用代码分析可维护性规则

1. 在“规则设置”下的“Code Analysis 编辑器”对话框中，展开“可维护性规则”节点  。

2. 选中以下规则的复选框：

   - 继承深度：CA1501 AvoidExcessiveInheritance - 阈值：深度超过 5 个级别的警告

   - 复杂性：CA1502 AvoidExcessiveComplexity - 阈值：深度超过 25 个级别的警告

   - 可维护性索引：CA1505 AvoidUnmaintainableCode - 阈值：深度低于 20 个级别的警告

   - 类耦合：CA1506 AvoidExcessiveClassCoupling - 阈值：类的警告超过 80，方法的警告超过 30

     此外，如果希望规则冲突阻止成功的生成，请选中规则说明旁边的“将警告视为错误”复选框。

3. 单击 **“确定”** 。 新的签入策略现在适用于将来的签入。

## <a name="see-also"></a>另请参阅

- [代码度量值](../code-quality/code-metrics-values.md)
- [创建和使用代码分析签入策略](../code-quality/how-to-create-or-update-standard-code-analysis-check-in-policies.md)
