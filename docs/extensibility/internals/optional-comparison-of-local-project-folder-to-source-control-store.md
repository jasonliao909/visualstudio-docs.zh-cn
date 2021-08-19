---
title: 比较Project文件夹与源代码管理存储|Microsoft Docs
description: 在源代码管理插件 API 中，本地项目文件夹与源代码管理之间的比较通过使用 SccDirQueryInfo 和 SccDirDiff 完成。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, comparing versions
- source control plug-ins, local project folders
ms.assetid: 65217e8b-15a6-4446-92b0-4cff1c6220f5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 76d57b288a221b2b7e89494605aaccd4df752821
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122063104"
---
# <a name="optional-comparison-of-local-project-folder-to-source-control-store"></a>本地项目文件夹与源代码管理存储之间的可选比较
在源代码管理插件 API 1.2 中，使用 [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md) 和 [SccDirDiff](../../extensibility/sccdirdiff-function.md)函数完成本地项目文件夹与源代码管理之间的比较。

 在 **解决方案资源管理器** 中，如果选择了文件夹而不是单个文件，"比较版本"快捷菜单将调用源代码管理插件中的新 [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)和 [SccDirDiff。](../../extensibility/sccdirdiff-function.md)

## <a name="new-capability-flags"></a>新功能标志
 `SCC_CAP_DIRECTORYDIFF`

 `SCC_CAP_DIRECTORYCHECKOUT`

## <a name="new-functions"></a>新函数
- [SccDirDiff](../../extensibility/sccdirdiff-function.md)

- [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)

 `SccDirQueryInfo`在 之前调用 函数 `SccDirDiff` ，以确定工作目录是否受源代码管理。 `SccDirDiff`函数显示当前本地目录与相应源代码管理文件夹之间的差异。 此命令要求源代码管理插件显示目录的更改列表。 源代码管理插件提供其自己的 UI 来显示差异。

> [!NOTE]
> 此函数使用与 [SccDiff 相同的命令标志](../../extensibility/sccdiff-function.md)。 作为源代码管理插件提供程序，可以选择不支持目录的"快速差异"操作。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
