---
title: 自定义 VSTU 创建的项目文件 | Microsoft Docs
description: 了解如何自定义 Visual Studio Tools for Unity (VSTU) 创建的项目文件。 查看 C# 代码示例。
ms.date: 04/19/2021
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: conceptual
ms.assetid: 60b8cc1d-cacc-404d-b768-77e81bc354f8
author: conceptdev
ms.author: crdun
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: db8d09f5b181796b3cb333963bec2772394728ff
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129972799"
---
# <a name="customize-project-files-created-by-vstu"></a>自定义 VSTU 创建的项目文件
Unity 在项目文件生成期间提供回调。 使用 [`AssetPostprocessor`](https://docs.unity3d.com/ScriptReference/AssetPostprocessor.html) 实现 `OnGeneratedSlnSolution` 和 `OnGeneratedCSProject` 方法，以在重新生成项目或解决方案文件时对其进行修改。

## <a name="demonstrates"></a>演示
如何自定义由 Visual Studio Tools for Unity 生成的 Visual Studio 项目文件。

## <a name="example"></a>示例

```csharp
using System;
using UnityEditor;
using UnityEngine;

public class ProjectFilePostprocessor : AssetPostprocessor
{
  public static string OnGeneratedSlnSolution(string path, string content)
  {
    // TODO: process solution content
    return content;
  }

  public static string OnGeneratedCSProject(string path, string content)
  {
    // TODO: process project content
    return content;
  }
}
```
