---
description: IDiaStackWalkHelper::searchForReturnAddress 搜索最近函数返回地址的指定堆栈帧。
title: IDiaStackWalkHelper::searchForReturnAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::searchForReturnAddress method
ms.assetid: 904223b1-6e26-4980-b310-d0b222cdbbbd
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: fe47a750625698f2fc930ed51ca9d8cedcec103b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831767"
---
# <a name="idiastackwalkhelpersearchforreturnaddress"></a>IDiaStackWalkHelper::searchForReturnAddress
搜索最近函数返回地址的指定堆栈帧。

## <a name="syntax"></a>语法

```C++
HRESULT searchForReturnAddress( 
   IDiaFrameData*  frame,
   ULONGLONG*      returnAddress
);
```

#### <a name="parameters"></a>参数
 `frame`

[in] 表示当前堆栈帧的 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) 对象。

 `returnAddress`

[out] 返回最近函数返回地址。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
