---
title: SuspendTracking | Microsoft Docs
description: 了解在当前上下文中暂停跟踪的 MSBuild SuspendTracking 的语法、要求和返回值。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- SuspendTracking
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- SuspendTracking
ms.assetid: f5e06e5a-8083-444c-99c1-07ba834226b5
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 7b1f9224eafe2e2186c87ba4d503e8a78f49abc4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122108234"
---
# <a name="suspendtracking"></a>SuspendTracking

在当前上下文中暂停跟踪。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI SuspendTracking(void);
```

## <a name="return-value"></a>返回值

 如果跟踪暂停，则返回带 SUCCEEDED 位集的 HRESULT 。

## <a name="requirements"></a>要求

 **标头：FileTracker.h** 

## <a name="see-also"></a>另请参阅

- [ResumeTracking](../msbuild/resumetracking.md)