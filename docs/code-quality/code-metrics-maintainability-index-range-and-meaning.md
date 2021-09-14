---
title: 代码指标 - 可维护性索引范围和含义
ms.date: 1/8/2021
description: 了解代码中代码指标的可维护性索引范围Visual Studio。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 8ab6115dd0c0a17bf6bb302d7c160e969d11773e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601335"
---
# <a name="code-metrics---maintainability-index-range-and-meaning"></a>代码指标 - 可维护性索引范围和含义

问：可维护性索引已重置为介于 0 和 100 之间。 如何以及为何这样做？

该指标最初的计算方式如下： `Maintainability Index = 171 - 5.2 * ln(Halstead Volume) - 0.23 * (Cyclomatic Complexity) - 16.2 * ln(Lines of Code)`

使用此公式意味着它的范围为 171 到无限负数。  由于代码倾向于 0，因此明显难以维护代码，并且代码 0 和某些负值之间的差没有用。  由于负数的有用性降低，并且希望使指标尽可能清晰，我们决定将所有 0 个或更少的索引视为 0，然后将 171 或更少的范围从 0 变基为 0 到 100。 因此，我们使用的公式是：

   `Maintainability Index = MAX(0,(171 - 5.2 * ln(Halstead Volume) - 0.23 * (Cyclomatic Complexity) - 16.2 * ln(Lines of Code))*100 / 171)`

除此之外，我们决定对阈值采取保守策略。  需要的是，如果索引显示红色，我们将以高度的置信度表示代码出现了问题。  这为我们提供了以下阈值：

对于阈值，我们决定分解此 0-100 范围 80-20，以保持干扰级别较低，并且仅标记可疑代码。 我们使用了以下阈值：

- 0-9 = 红色
- 10-19 = 黄色
- 20-100 = 绿色
