---
title: 代码分析规则集参考
ms.date: 04/04/2018
description: 了解 Visual Studio 传统代码分析中的内置规则集。 请参阅有关规则集的资源。 了解如何在自定义规则集中使用这些集。
ms.custom: SEO-VS-2020
ms.topic: reference
helpviewer_keywords:
- code analysis, rule sets reference
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: c6f23dcc5646d4516f9e00e50f8bf742b94502a2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601261"
---
# <a name="code-analysis-rule-set-reference"></a>代码分析规则集参考

当在 Visual Studio 中为托管代码项目配置传统分析时，可以从内置“规则集”列表中进行选择。 某些规则包含在多个内置规则集中，例如，基本正确性规则规则集中包含托管建议规则规则集中的规则。

> [!NOTE]
> 本部分中的规则集与传统分析有关。 有关可用于代码分析器包的规则集的信息，请参阅[将规则集用于代码分析器](/dotnet/fundamentals/code-analysis/code-quality-rule-options)。

可以使用某一内置规则集，也可以[自定义规则集](../code-quality/how-to-create-a-custom-rule-set.md)，以满足你的项目要求。 如果包含在自定义规则集中包含相同规则的多个规则集，则该规则仅在自定义规则集中出现一次。

本部分主题介绍内置规则集及其包含的规则（或警告）。

| 规则集 | 包含的规则 |
| - | - |
| [所有规则](all-rules-rule-set.md) | 包含所有可用的托管和 C++ 规则 |
| [基本更正规则](basic-correctness-rules-rule-set-for-managed-code.md) | 包括托管建议规则以及关于逻辑错误和框架用法的规则 |
| [扩展的更正规则](extended-correctness-rules-rule-set-for-managed-code.md) | 包括基本正确性规则（其中包括托管建议规则）以及关于逻辑错误和框架用法的更多规则 |
| [基本设计指南规则](basic-design-guideline-rules-rule-set-for-managed-code.md) | 包括托管建议规则以及用于确保代码易于读取、理解和维护的规则 |
| [扩展的设计指南规则](extended-design-guidelines-rules-rule-set-for-managed-code.md) | 包括基本设计指南规则（其中包括托管建议规则）以及关于侧重于命名的更多可维护性规则 |
| [全球化规则](globalization-rules-rule-set-for-managed-code.md) | 包括关于全球化问题的规则 |
| [托管最低规则](managed-minimum-rules-rule-set-for-managed-code.md) | 包括关于关键托管代码问题的四个规则 |
| [托管建议规则](managed-recommended-rules-rule-set-for-managed-code.md) | 包括托管最低规则以及关于关键托管代码问题的更多规则 |
| [混合最低规则](mixed-minimum-rules-rule-set.md) | 包括关于 CLR 的 C++ 代码中关键问题的规则 |
| [混合建议规则](mixed-recommended-rules-rule-set.md) | 包括混合最低规则以及关于 CLR 的 C++ 代码中关键问题的更多规则 |
| [本机最低规则](native-minimum-rules-rule-set.md) | 包括关于本机代码中关键问题的规则 |
| [本机建议规则](native-recommended-rules-rule-set.md) | 包括本机最低规则以及关于本机代码中关键问题的更多规则 |
| [安全性规则](security-rules-rule-set-for-managed-code.md) | 包括用于查找安全漏洞的规则 |