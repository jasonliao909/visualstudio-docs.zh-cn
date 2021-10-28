---
title: WPF .Targets 文件 | Microsoft Docs
description: 了解 Windows Presentation Foundation (WPF) 如何通过添加特殊的 .targets 文件（即 Microsoft.WinFX.targets）中的一组特定于 WPF 的任务来扩展 MSBuild。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- combining tasks into a .targets file to build an MSBuild project [WPF MSBuild]
- WPF .targets files [WPF MSBuild], introduction
- WPF .targets files [WPF MSBuild]
ms.assetid: e85a3ff4-dedd-4ff4-9b22-3a1e94755362
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: c1e7fde5440859f76cef6fe1ca0b41122f2e932b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126642047"
---
# <a name="wpf-targets-files"></a>WPF .targets 文件

Windows Presentation Foundation (WPF) 通过添加一组特定于 WPF 的任务（任务被合并到一个特殊的 .targets 文件 Microsoft.WinFX.targets）来扩展 MSBuild。 此文件合并了在 WP 中生成 MSBuild 项目所需的一组 MSBuild 任务。

## <a name="see-also"></a>另请参阅

- [MSBuild .targets 文件](../msbuild/msbuild-dot-targets-files.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [生成 WPF 应用程序 (WPF)](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)