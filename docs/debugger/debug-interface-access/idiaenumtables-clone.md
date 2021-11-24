---
description: 创建一个枚举器，其中包含与当前表枚举器相同的枚举状态。
title: IDiaEnumTables::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Clone method
ms.assetid: beb21109-b12c-44d8-8c1f-a332216b3713
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 19922dcb8c8f280ce57dd32d02bd8dcf6737698b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832152"
---
# <a name="idiaenumtablesclone"></a>IDiaEnumTables::Clone
创建一个枚举器，其中包含与当前枚举器相同的枚举状态。

## <a name="syntax"></a>语法

```C++
HRESULT Clone ( 
   IDiaEnumTables** ppenum
);
```

#### <a name="parameters"></a>参数
 `ppenum`

[out] 返回包含枚举器副本的 [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md) 对象。 不会复制表，只会复制枚举器。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
