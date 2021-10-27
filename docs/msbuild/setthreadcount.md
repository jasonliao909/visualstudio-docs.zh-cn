---
title: SetThreadCount | Microsoft Docs
description: 了解 MSBuild 如何使用 SetThreadCount 设置全局线程计数，并将此计数分配给当前线程。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
apiname:
- SetThreadCount
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- SetThreadCount
ms.assetid: 335335a5-8ca0-4e18-95f5-62aa6a691386
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 35649f2ae7c0aec8b713573fc5b9f8f29e86ac2f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640578"
---
# <a name="setthreadcount"></a>SetThreadCount

设置全局线程计数，并将该计数分配给当前线程。

## <a name="syntax"></a>语法

```cmd
HRESULT WINAPI SetThreadCount(int threadCount);
```

#### <a name="parameters"></a>参数

[in] `threadCount`

 要使用的线程数。

## <a name="return-value"></a>返回值

 线程数更新后，则返回带 SUCCEEDED 位集的 HRESULT 。

## <a name="requirements"></a>要求

 **标头：FileTracker.h** 