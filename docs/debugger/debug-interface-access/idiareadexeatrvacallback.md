---
description: 使客户端应用程序能够提供由相对虚拟地址指定的可执行文件的字节。
title: IDiaReadExeAtRVACallback | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtRVACallback interface
ms.assetid: b2892513-3952-4f99-9b98-60cb9b1fdc91
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: ca3261998ae754b637c8adb412850676cb93532f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831997"
---
# <a name="idiareadexeatrvacallback"></a>IDiaReadExeAtRVACallback
使客户端应用程序能够提供由相对虚拟地址指定的可执行文件的字节。

## <a name="syntax"></a>语法

```
IDiaReadExeAtRVACallback : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDiaReadExeAtRVACallback` 。

|方法|说明|
|------------|-----------------|
|[IDiaReadExeAtRVACallback::ReadExecutableAtRVA](../../debugger/debug-interface-access/idiareadexeatrvacallback-readexecutableatrva.md)|从可执行文件读取 RVA (指定相对虚拟地址) 字节数。|

## <a name="remarks"></a>备注
 客户端应用程序实现此接口，以便使用相对虚拟地址在可执行文件的 文件中提供可执行文件的字节。 若要使用绝对文件偏移量，请实现 [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md) 接口。

## <a name="notes-for-callers"></a>调用方说明
 此方法由客户端应用程序实现，并作为读取文件的替代方法传递给 [IDiaDataSource：：loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) 方法。

## <a name="requirements"></a>要求
 标头：Dia2.h

 库：diaguids.lib

 DLL：msdia80.dll

## <a name="see-also"></a>另请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
