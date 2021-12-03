---
title: 使用生成
description: 用于处理生成的使用技巧。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: f530c1ec5cbe10152f6877877f8886a98e4892d9
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515815"
---
# <a name="working-with-builds-in-visual-studio-extensions"></a>使用 Visual Studio 扩展中的生成 

下面是用于处理生成的不同方式的小代码示例的集合。

## <a name="build-solution"></a>生成解决方案
若要生成整个解决方案，请调用 `BuildAsync()` 方法。

```csharp
bool buildStarted = await VS.Build.BuildSolutionAsync(BuildAction.Build);
```

## <a name="build-project"></a>生成项目
可以通过将项目传递给方法来生成任何项目。

```csharp
Project project = await VS.Solutions.GetActiveProjectAsync();
await project.BuildAsync(BuildAction.Rebuild);
```

## <a name="set-build-property"></a>设置生成属性
演示如何设置项目的生成属性。

```csharp
Project project = await VS.Solutions.GetActiveProjectAsync();
bool succeeded = await project.TrySetAttributeAsync("propertyName", "value");
```

## <a name="get-build-property"></a>获取生成属性
演示如何获取任何项目或项目项的生成属性。

```csharp
Project item = await VS.Solutions.GetActiveProjectAsync();
string value = await item.GetAttributeAsync("propertyName");
```
