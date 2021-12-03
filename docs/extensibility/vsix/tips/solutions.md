---
title: 使用解决方案
description: 用于处理解决方案的使用技巧。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: 1e485fbc60ae0ff2d2c3e1e63a0e87caef482138
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515844"
---
# <a name="working-with-solutions-in-visual-studio-extensions"></a>使用 Visual Studio 扩展中的解决方案

下面是用来处理解决方案的不同方式的小代码示例的集合。

## <a name="solution-events"></a>解决方案事件
侦听任何解决方案事件。

```csharp
VS.Events.SolutionEvents.OnAfterOpenProject += OnAfterOpenProject;

...

private void OnAfterOpenProject(Project obj)
{
    // Handle the event
}
```

## <a name="is-a-solution-open"></a>解决方案是否已打开？
检查解决方案当前是否已打开或正在打开。

```csharp

bool isOpen = await VS.Solutions.IsOpenAsync();
bool isOpening = await VS.Solutions.IsOpeningAsync();
```

## <a name="get-all-projects-in-solution"></a>获取解决方案中的所有项目
获取解决方案中所有项目的列表。

```csharp
var projects = await VS.Solutions.GetAllProjectsAsync();
```
