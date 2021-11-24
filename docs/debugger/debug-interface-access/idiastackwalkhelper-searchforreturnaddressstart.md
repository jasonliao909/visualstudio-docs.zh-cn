---
description: 在指定堆栈地址处或附近搜索返回地址的指定堆栈帧。
title: IDiaStackWalkHelper::searchForReturnAddressStart | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper::searchForReturnAddressStart method
ms.assetid: 0a33142e-5d31-44ea-874a-a2e94d95cbd2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: f556ec473053e7a8ebba5c90760104d65fa76983
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831766"
---
# <a name="idiastackwalkhelpersearchforreturnaddressstart"></a>IDiaStackWalkHelper::searchForReturnAddressStart
在指定堆栈地址处或附近搜索返回地址的指定堆栈帧。

## <a name="syntax"></a>语法

```C++
HRESULT searchForReturnAddressStart( 
   IDiaFrameData*  frame,
   ULONGLONG       startAddress,
   ULONGLONG*      returnAddress
);
```

#### <a name="parameters"></a>参数
 `frame`

[in] 表示当前堆栈帧的 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) 对象。

 `startAddress`

[in] 从此处开始搜索的虚拟内存地址。

 `ReturnAddress`

[out] 将最近函数返回地址返回到 `startAddress`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
