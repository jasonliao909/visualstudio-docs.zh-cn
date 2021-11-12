---
title: 代码度量 - 可维护性指数范围和含义
ms.date: 1/8/2021
description: 了解 Visual Studio 中代码度量的可维护性指数范围指标。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 8ab6115dd0c0a17bf6bb302d7c160e969d11773e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601335"
---
# <a name="code-metrics---maintainability-index-range-and-meaning"></a>代码度量 - 可维护性指数范围和含义

问：可维护性指数已被重置为介于 0 到 100 之间。 这样做的方式和原因是什么？

最初计算代码度量的方法如下所示：`Maintainability Index = 171 - 5.2 * ln(Halstead Volume) - 0.23 * (Cyclomatic Complexity) - 16.2 * ln(Lines of Code)`

使用此公式意味着值的范围是从 171 到无限负数。  当代码趋向于 0 时，显然很难维护代码，并且值为 0 的代码和为某个负值的代码之间的差异没什么用处。  由于负数的用处很低，并且我们希望让指标尽可能清晰，我们决定将所有 0 或更小的指数都视为 0，然后重新定义 171 或定义成更小的范围，即 0 到 100。 出于此原因，我们使用的公式是：

   `Maintainability Index = MAX(0,(171 - 5.2 * ln(Halstead Volume) - 0.23 * (Cyclomatic Complexity) - 16.2 * ln(Lines of Code))*100 / 171)`

除此之外，我们还决定了对阈值采取保守策略。  理想情况是，如果指数显示为红色，我们可以十分确定地表示代码存在问题。  由此阈值情况如下所示：

对于阈值，我们决定将这个 0-100 的范围分解为 80-20，以维持干扰的低级别，并且只标记可疑的代码。 我们使用了以下阈值：

- 0-9 = 红色
- 10-19 = 黄色
- 20-100 = 绿色
