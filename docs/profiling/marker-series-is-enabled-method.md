---
description: 确定是否有任何会话启用了该提供程序。
title: marker_series::is_enabled 方法 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersobj/Concurrency, diagnostic::marker_series::is_enabled
helpviewer_keywords:
- Concurrency, diagnostic::marker_series::is_enabled method
ms.assetid: 8ce4dd50-ca29-4c72-98d6-582693f7d501
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0ce01d71b3fac63062a3f823f1862fd199fa39be
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223571"
---
# <a name="marker_seriesis_enabled-method"></a>marker_series::is_enabled 方法
确定是否有任何会话启用了该提供程序。

## <a name="syntax"></a>语法

```cpp
bool is_enabled();
bool is_enabled(
   marker_importance _Importance,
   int _Category
);
```

#### <a name="parameters"></a>参数
 `_Importance` 重要性级别。

 `_Category` 类别。

## <a name="return-value"></a>返回值

## <a name="requirements"></a>要求
 **标头：cvmarkersobj.h** 

 **命名空间：** Concurrency::diagnostic

## <a name="see-also"></a>另请参阅
- [marker_series 类](../profiling/marker-series-class.md)
