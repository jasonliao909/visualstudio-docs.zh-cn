---
title: '手动运行旧版代码分析 A0.NET) '
description: 了解如何检测源代码中可能的缺陷。 了解如何在托管代码中手动运行旧代码Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- code analysis, running
ms.assetid: 5086d228-f92e-4515-9708-c5b89b9e9a03
author: Mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- dotnet
ms.openlocfilehash: ff428f1a72812996a8217d4193deebe7393cbcc4a2fa9b0b870ab41f7094a0bf
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121392752"
---
# <a name="how-to-run-legacy-code-analysis-manually-for-managed-code"></a>如何：为托管代码手动运行旧代码分析

代码分析工具提供有关源代码中可能缺陷的信息。 可以随代码项目的每次生成自动运行代码分析，也可以手动运行代码分析。 运行代码分析时检查的规则在项目属性页Code Analysis页上指定。 有关详细信息，请参阅[如何：为托管Code Analysis配置Project。](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)

## <a name="to-run-code-analysis-manually"></a>手动运行代码分析

1. 如果使用 2019 Visual Studio 16.5 或更高版本，在命令提示符下执行以下命令，然后Visual Studio：

```
setx EnableLegacyCodeAnalysis true
```

2. 在 **解决方案资源管理器** 中，单击项目。

3. 在"**分析"** 菜单上，单击"Code Analysis **名称***Project"。*
