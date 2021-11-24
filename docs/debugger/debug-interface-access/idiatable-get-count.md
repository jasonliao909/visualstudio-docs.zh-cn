---
description: 检索表中的项数。
title: IDiaTable::get_Count | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable::get_Count method
ms.assetid: bb47abe8-6706-4679-bc52-79f6444dae7e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: f9f3a73d221786b08ea5fa989d5a623536ade3dd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832740"
---
# <a name="idiatableget_count"></a>IDiaTable::get_Count
检索表中的项数。

## <a name="syntax"></a>语法

```C++
HRESULT get_Count ( 
   LONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回表中的项数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
- [IDiaTable::Item](../../debugger/debug-interface-access/idiatable-item.md)
