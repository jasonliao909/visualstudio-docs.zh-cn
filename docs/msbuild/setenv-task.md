---
title: SetEnv 任务 | Microsoft Docs
description: 了解 MSBuild 如何使用 SetEnv 任务来设置或删除指定环境变量的值。
ms.custom: SEO-VS-2020
ms.date: 11/05/2018
ms.topic: reference
f1_keywords:
- vc.task.setenv
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), tasks
- SetEnv task (MSBuild (C++))
ms.assetid: fd9e4225-68cb-4608-8b27-468b0218c936
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: c760e22842a3063036d0e4f8c2945ddefc312900
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640579"
---
# <a name="setenv-task"></a>SetEnv 任务

设置或删除指定环境变量的值。

## <a name="parameters"></a>参数

 下表描述了 SetEnv 任务的参数。

|参数|说明|
|---------------|-----------------|
|**Name**|必需的 **String** 参数。<br /><br /> 环境变量名。|
|OutputEnvironmentVariable|可选的 **String** 输出参数。<br /><br /> 包含分配给 Name 参数指定的环境变量的值。|
|**Prefix**|必需的 `Boolean` 参数。<br /><br /> 如果为 `true`，则将 Value 参数的值连接到 Name 参数指定的环境变量的值之前，然后向环境变量分配结果。 如果为 `false`，则仅向环境变量分配 Value 参数的值。|
|**Target**|可选 **String** 参数。<br /><br /> 指定环境变量的存储位置。 指定“用户”或“计算机”。<br /><br /> 有关详细信息，请参阅 [EnvironmentVariableTarget 枚举](xref:System.EnvironmentVariableTarget)。|
|**值**|可选 **String** 参数。<br /><br /> 分配给 Name 参数指定的环境变量的值。 如果 Value 为空并且该变量存在，则删除该变量。 如果该变量不存在，即使无法执行该操作也不会出现任何错误。<br /><br /> 有关详细信息，请参阅 [Environment::SetEnvironmentVariable 方法](xref:System.Environment.SetEnvironmentVariable%2A)。|

## <a name="see-also"></a>另请参阅

- [任务参考](../msbuild/msbuild-task-reference.md)
