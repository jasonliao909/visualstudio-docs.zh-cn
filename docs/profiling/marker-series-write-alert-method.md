---
description: 向并发可视化工具跟踪文件写入一个警报。
title: marker_series::write_alert 方法 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersobj/Concurrency, diagnostic:marker_series::write_alert
helpviewer_keywords:
- Concurrency, diagnostic:marker_series::write_alert method
ms.assetid: 9d5465c7-f862-47a7-b249-4116605075a6
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: ed095929201176cbfc86f9810a5d089dce52216c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126735696"
---
# <a name="marker_serieswrite_alert-method"></a>marker_series::write_alert 方法
向并发可视化工具跟踪文件写入一个警报。

## <a name="syntax"></a>语法

```cpp
void write_alert(
   _In_ LPCTSTR _Format,
   ...
);
```

#### <a name="parameters"></a>参数
 `_Format` 一个复合格式字符串，其中包含与零个或多个格式项混合的文本，这些格式项对应于参数列表中的对象。

## <a name="requirements"></a>要求
 **标头：cvmarkersobj.h** 

 **命名空间：** Concurrency::diagnostic

## <a name="see-also"></a>另请参阅
- [marker_series 类](../profiling/marker-series-class.md)
