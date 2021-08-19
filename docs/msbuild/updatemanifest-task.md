---
title: UpdateManifest 任务 | Microsoft Docs
description: 了解 MSBuild 如何使用 UpdateManifest 任务来更新清单中的选定属性并重新签名。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, UpdateManifest task
- UpdateManifest task [MSBuild]
ms.assetid: 1291fd33-b89e-4e15-8fb1-69f9625cf2d2
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 8cde4f2fcc9b226aeda9066da083a1a37979dfe9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122142593"
---
# <a name="updatemanifest-task"></a>UpdateManifest 任务

更新清单中所选的属性并重新签名。

## <a name="parameters"></a>参数

 下表描述了 `UpdateManifest` 任务的参数。

|参数|描述|
|---------------|-----------------|
|`ApplicationManifest`|必选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定应用程序清单。|
|`ApplicationPath`|必选 `String` 参数。<br /><br /> 指定应用程序清单的路径。|
|`InputManifest`|必选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定要更新的清单。|
|`OutputManifest`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 输出参数。<br /><br /> 指定包含更新的属性的清单。|

## <a name="remarks"></a>注解

 除了具有表中列出的参数外，此任务还将从 <xref:Microsoft.Build.Utilities.Task> 类继承参数。 有关这些其他参数的列表及其说明，请参阅[任务基类](../msbuild/task-base-class.md)。

## <a name="see-also"></a>另请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)