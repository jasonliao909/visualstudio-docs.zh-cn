---
title: EndTrackingContext | Microsoft Docs
description: 了解使用 MSBuild EndTrackingContext 结束当前跟踪上下文的语法、返回值和要求。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- EndTrackingContext
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- EndTrackingContext
ms.assetid: c2c5d794-8dc8-4594-8717-70dc79a0e75d
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 4f4a0cd1b327f9be99b07e90bc7564a17ec13472
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736028"
---
# <a name="endtrackingcontext"></a>EndTrackingContext

结束当前跟踪上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI EndTrackingContext();
```

## <a name="return-value"></a>返回值

如果跟踪上下文结束，返回带 SUCCEEDED 位组的 HRESULT。

## <a name="requirements"></a>要求

**标头：FileTracker.h** 

## <a name="see-also"></a>另请参阅

- [StartTrackingContext](../msbuild/starttrackingcontext.md)
