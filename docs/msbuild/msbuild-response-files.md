---
title: MSBuild 响应文件 | Microsoft Docs
description: 了解 MSBuild 响应或 .rsp 文件，这是包含 MSBuild.exe 命令行开关的文本文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- response files, MSBuild
- MSBuild, response files
- MSBuild, .rsp files
- .rsp files
ms.assetid: 9f53987b-20ee-470a-ab62-fce997bb5e15
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: abe7882e18936b169cfcd0b02e7eaa66c891f5a2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126737400"
---
# <a name="msbuild-response-files"></a>MSBuild 响应文件

响应 (.rsp) 文件是包含 MSBuild.exe 命令行开关的文本文件。 每个开关可以单独占一行，或者所有开关仅占一行。 注释行以 # 符号开头。 @ 开关用于将另一个响应文件传递给 MSBuild.exe。

## <a name="msbuildrsp"></a>MSBuild.rsp

自动响应文件是在生成项目时 MSBuild.exe 自动使用的特殊 .rsp 文件。 MSBuild.rsp 文件必须位于 MSBuild.exe 所在的目录中，否则无法找到该文件。 可以将此文件编辑为，向 MSBuild.exe 指定默认命令行开关。 例如，如果每次生成项目时都使用相同的记录器，可以将 -logger 开关添加到 MSBuild.rsp 中，这样 MSBuild.exe 在每次项目生成后都会使用记录器。

## <a name="directorybuildrsp"></a>Directory.Build.rsp

在版本 15.6 及更高版本中，MSBuild 会在该项目的父级目录中搜索名为 Directory.Build.rsp 的文件。  这可以帮助源代码存储库在命令行生成过程中提供默认参数。  此外，它还可以用于指定托管生成的命令行参数。

## <a name="see-also"></a>请参阅

- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [命令行参考](../msbuild/msbuild-command-line-reference.md)
