---
title: 设置瀑布图 | Microsoft IntelliTest 开发人员测试工具
description: 了解设置瀑布图，该瀑布图在“程序集”、“固定例程”和“探索”级别组织设置。
ms.custom: SEO-VS-2020
ms.date: 05/02/2017
ms.topic: conceptual
helpviewer_keywords:
- IntelliTest, Settings waterfall
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 88d8ed6df537c46f810f765c3b7d1b23eab9a3e4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122139915"
---
# <a name="settings-waterfall"></a>设置瀑布图

设置瀑布图的概念意味着用户可以在“程序集”、“装置”和“浏览”级别指定设置  ：

* 程序集 - [PexAssemblySettings](attribute-glossary.md#pexassemblysettings)
* 装置 - [PexClass](attribute-glossary.md#pexclass)
* 浏览 - [PexExplorationAttributeBase](attribute-glossary.md#pexexplorationattributebase)

在“程序集”级别上指定的设置会影响该程序集下的所有装置和浏览。 在“装置”级别上指定的设置会影响该装置下的所有浏览。 采用子设置的情况&mdash;如果在程序集和装置级别上定义了设置，则会使用装置中的设置。

请注意，某些设置特定于程序集级别或装置级别。

**示例**

```csharp
using Microsoft.Pex.Framework;

[assembly: PexAssemblySettings(MaxBranches = 1000)] // we override the default value of maxbranches

namespace MyTests
{
    [PexClass(MaxBranches = 500)] // we override the 1000 value and set maxbranches to 500
    public partial class MyTests
    {
        [PexMethod(MaxBranches = 100)] // we override again, maxbranches = 100
        public void MyTest(...) { ... }
    }
}
```

## <a name="got-feedback"></a>有反馈？

在[开发人员社区](https://aka.ms/feedback/suggest?space=8)上发布想法和功能请求。
