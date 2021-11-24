---
description: 创建一个枚举器，其中包含与当前枚举器相同的枚举状态。
title: IDiaEnumSegments::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Clone method
ms.assetid: 93deaac6-72ab-4408-ba14-66174a618757
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: ecef9448b03df8238259bd8a9c5df8011e40c946
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832220"
---
# <a name="idiaenumsegmentsclone"></a>IDiaEnumSegments::Clone
创建一个枚举器，其中包含与当前枚举器相同的枚举状态。

## <a name="syntax"></a>语法

```C++
HRESULT Clone ( 
   IDiaEnumSegments** ppenum
);
```

#### <a name="parameters"></a>参数
 ppenum

[out] 返回包含枚举器副本的 [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md) 对象。 不会复制段，只会复制枚举器。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)
