---
title: StopTrackingAndCleanup | Microsoft Docs
description: 了解 MSBuild 如何使用 StopTrackingAndCleanup 停止所有跟踪，并释放跟踪会话使用的任何内存。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- StopTrackingAndCleanup
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- StopTrackingAndCleanup
ms.assetid: 9f8c5994-2dfc-43c3-a5fb-89b2f8990429
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: c076f0f5fbf591e0ca7ca6f91a7700185a2aea05
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640559"
---
# <a name="stoptrackingandcleanup"></a>StopTrackingAndCleanup

停止所有跟踪，并释放跟踪会话使用的任何内存。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI StopTrackingAndCleanup(void);
```

## <a name="return-value"></a>返回值

 如果跟踪停止，则返回带 SUCCEEDED 位集的 HRESULT。

## <a name="requirements"></a>要求

 **标头：FileTracker.h** 

## <a name="see-also"></a>另请参阅

- [StartTrackingContext](../msbuild/starttrackingcontext.md)