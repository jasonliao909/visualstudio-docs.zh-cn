---
title: ResumeTracking | Microsoft Docs
description: 了解在当前上下文中恢复跟踪的 MSBuild ResumeTracking 的语法、要求和返回值。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- ResumeTracking
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- ResumeTracking
ms.assetid: d637e019-7c50-4b0a-812e-bc822001e697
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 6b2d7b4bd0bdbdf60864344edb552c884482a93e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122143048"
---
# <a name="resumetracking"></a>ResumeTracking

在当前上下文中恢复跟踪。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI ResumeTracking();
```

## <a name="return-value"></a>返回值

 如果跟踪恢复，则返回带 SUCCEEDED 位集的 HRESULT 。 如果因为上下文不可用而无法恢复跟踪，将返回“E_FAIL”。

## <a name="requirements"></a>要求

 **标头：FileTracker.h** 

## <a name="see-also"></a>另请参阅

- [SuspendTracking](../msbuild/suspendtracking.md)