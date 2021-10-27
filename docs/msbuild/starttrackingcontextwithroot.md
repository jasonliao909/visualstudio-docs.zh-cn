---
title: StartTrackingContextWithRoot | Microsoft Docs
description: 了解如何使用 MSBuild StartTrackingContextWithRoot 通过指定根标记的响应文件来启动跟踪上下文。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- StartTrackingContextWithRoot
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- StartTrackingContextWithRoot
ms.assetid: f6ef2b76-8035-4a14-8195-aa221c46ef48
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 62ecbb05d0fd129709345c23887aca1d9ed201be
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640560"
---
# <a name="starttrackingcontextwithroot"></a>StartTrackingContextWithRoot

使用指定根标记的响应文件启动跟踪上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI StartTrackingContextWithRoot(LPCTSTR intermediateDirectory, LPCTSTR taskName, LPCTSTR rootMarkerResponseFile);
```

#### <a name="parameters"></a>参数

[in] `intermediateDirectory`

 存储跟踪日志的目录。

[in] `taskName`

 标识跟踪上下文。 此名称用于创建日志文件名。

[in] `rootMarkerResponseFile`

 包含根标记的响应文件的路径名称。 根名称用于将上下文的所有跟踪聚集在一起。

## <a name="return-value"></a>返回值

 如果跟踪上下文创建完成，则返回带 SUCCEEDED 位集的 HRESULT 。

## <a name="requirements"></a>要求

 **标头：FileTracker.h** 

## <a name="see-also"></a>另请参阅

- [StartTrackingContext](../msbuild/starttrackingcontext.md)