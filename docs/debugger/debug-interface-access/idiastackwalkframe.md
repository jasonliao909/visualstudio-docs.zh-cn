---
description: 维护调用 IDiaFrameData::execute) 方法之间的堆栈上下文。
title: IDiaStackWalkFrame | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame interface
ms.assetid: 42d82845-d6f6-4846-9ecd-9dd169216077
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 785766a8fb0de87b967ecebdae391a5167bca466
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831782"
---
# <a name="idiastackwalkframe"></a>IDiaStackWalkFrame
维护调用 [IDiaFrameData::execute](../../debugger/debug-interface-access/idiaframedata-execute.md) 方法之间的堆栈上下文。

## <a name="syntax"></a>语法

```
IDiaStackWalkFrame : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 `IDiaStackWalkFrame` 方法。

|方法|说明|
|------------|-----------------|
|[IDiaStackWalkFrame::get_registerValue](../../debugger/debug-interface-access/idiastackwalkframe-get-registervalue.md)|检索寄存器的值。|
|[IDiaStackWalkFrame::put_registerValue](../../debugger/debug-interface-access/idiastackwalkframe-put-registervalue.md)|设置寄存器的值。|
|[IDiaStackWalkFrame::readMemory](../../debugger/debug-interface-access/idiastackwalkframe-readmemory.md)|从映像读取内存。|
|[IDiaStackWalkFrame::searchForReturnAddress](../../debugger/debug-interface-access/idiastackwalkframe-searchforreturnaddress.md)|搜索最近函数返回地址的指定堆栈帧。|
|[IDiaStackWalkFrame::searchForReturnAddressStart](../../debugger/debug-interface-access/idiastackwalkframe-searchforreturnaddressstart.md)|在指定地址处或附近搜索返回地址的指定堆栈帧。|

## <a name="remarks"></a>备注
 此接口在程序执行期间用于读取和写入寄存器以及访问内存和查找返回地址。

## <a name="notes-for-callers"></a>对调用者的说明
 客户端应用程序实现此接口并将接口的实例传递给 [IDiaFrameData::execute](../../debugger/debug-interface-access/idiaframedata-execute.md) 方法。 此接口的相同实例重复使用，以便在每次调用 `execute` 方法时维护寄存器的状态。 `execute` 方法还使用此接口来确定返回地址。

## <a name="requirements"></a>要求
 标头：Dia2.h

 库：diaguids.lib

 DLL：msdia80.dll

## <a name="see-also"></a>另请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaFrameData::execute](../../debugger/debug-interface-access/idiaframedata-execute.md)
