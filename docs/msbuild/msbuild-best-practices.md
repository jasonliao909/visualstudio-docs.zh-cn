---
title: MSBuild 最佳做法 | Microsoft Docs
description: 了解 MSBuild 脚本编写最佳做法（如使用 Condition 特性，而不使用通配符）。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- best practices, MSBuild
- MSBuild, best practices
ms.assetid: 90ef8693-e921-410a-a377-fe4d13f58c48
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: b96ed3b0e2ece6c8b0cd27c5733c863d4204c513
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122115754"
---
# <a name="msbuild-best-practices"></a>MSBuild 最佳做法

我们建议下列编写 MSBuild 脚本的最佳做法：

- 默认属性值的最佳处理方式是使用 `Condition` 特性，而不是声明可在命令行中重写其默认值的属性。 例如，使用

```xml
<MyProperty Condition="'$(MyProperty)' == ''">
   MyDefaultValue
</MyProperty>
```

- 通常，选择项时，请避免使用通配符。 而应显式指定文件。 这是因为在大多数项目类型中，MSBuild 会在不同时间展开通配符，如添加或删除项时，这可能会导致意外行为。 在 .NET Core SDK 样式项目中有一个例外，该项目可以正确处理通配符。

## <a name="see-also"></a>请参阅

- [高级概念](../msbuild/msbuild-advanced-concepts.md)
