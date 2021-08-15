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
ms.openlocfilehash: ac8c88423af7d994b4e9ba29a4dede791312d12e2cdf441c990096190858a084
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121423509"
---
# <a name="customize-project-files-created-by-vstu"></a>自定义 VSTU 创建的项目文件
Unity 在项目文件生成期间提供回调。 实现 `OnGeneratedSlnSolution` `OnGeneratedCSProject` 和 方法， [`AssetPostprocessor`](https://docs.unity3d.com/ScriptReference/AssetPostprocessor.html) 使用 在重新生成项目或解决方案文件时对其进行修改。

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
