---
title: 自定义 VSTU 创建的项目文件 | Microsoft Docs
description: 了解如何自定义 Visual Studio Tools for Unity (VSTU) 创建的项目文件。 查看 C# 代码示例。
ms.custom: ''
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
ms.openlocfilehash: a4a5973863877db2d071f9be8d4689928b21a689
ms.sourcegitcommit: 3e1ff87fba290f9e60fb4049d011bb8661255d58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2021
ms.locfileid: "107879312"
---
# <a name="customize-project-files-created-by-vstu"></a>自定义 VSTU 创建的项目文件
Unity 在项目文件生成期间提供回调。 实现 `OnGeneratedSlnSolution` 和 `OnGeneratedCSProject` 方法，以便在重新 [`AssetPostprocessor`](https://docs.unity3d.com/ScriptReference/AssetPostprocessor.html) 生成项目或解决方案文件时对其进行修改。

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
