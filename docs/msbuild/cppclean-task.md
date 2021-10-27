---
title: CPPClean 任务 | Microsoft Docs
description: 本文介绍 CPPClean 任务，该任务用于删除生成 C++ 项目时 MSBuild 创建的临时文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vc.task.cppclean
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), CPPClean task
- CPPClean task (MSBuild (C++))
ms.assetid: b62a482e-8fb5-4999-b50b-6605a078e291
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 65437104a04de8fe08f21b077a093483ec3209df
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736060"
---
# <a name="cppclean-task"></a>CPPClean 任务

删除生成 C++ 项目时 MSBuild 创建的临时文件。 删除生成文件的过程称为“清除”。

## <a name="parameters"></a>参数

 下表描述了 CPPClean 任务的参数。

|参数|说明|
|---------------|-----------------|
|DeletedFiles|可选 `ITaskItem[]` 输出参数。<br /><br /> 定义可由任务使用和发出的 MSBuild 输出文件项的数组。|
|DoDelete|可选 **Boolean** 参数。<br /><br /> 如果为 `true`，则清除临时生成文件。|
|FilePatternsToDeleteOnClean|必选 `String` 参数。<br /><br /> 指定要清除的文件的文件扩展名列表（以分号分隔）。|
|FilesExcludedFromClean|可选 `String` 参数。<br /><br /> 指定不会清除的文件的列表（以分号分隔）。|
|FoldersToClean|必选 `String` 参数。<br /><br /> 指定要清除的目录的列表（以分号分隔）。 可指定完整路径或相对路径，并且路径可包含通配符 (*)。|

## <a name="see-also"></a>另请参阅

- [任务参考](../msbuild/msbuild-task-reference.md)
