---
description: 使客户端应用程序能够按文件位置指定提供可执行文件的字节。
title: IDiaReadExeAtOffsetCallback | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtOffsetCallback interface
ms.assetid: 3c961641-3ce3-4bc3-bd6e-a802fa3bec49
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9d8ca962425742304a215512abd10b7aed755feb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832002"
---
# <a name="idiareadexeatoffsetcallback"></a>IDiaReadExeAtOffsetCallback
使客户端应用程序能够按文件位置指定提供可执行文件的字节。

## <a name="syntax"></a>语法

```
IDiaReadExeAtOffsetCallback : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 `IDiaReadExeAtOffsetCallback` 方法。

|方法|说明|
|------------|-----------------|
|[IDiaReadExeAtOffsetCallback::ReadExecutableAt](../../debugger/debug-interface-access/idiareadexeatoffsetcallback-readexecutableat.md)|从可执行文件的指定偏移量开始读取指定数量的字节。|

## <a name="remarks"></a>备注
 客户端应用程序实现此接口，以便使用可执行文件的绝对偏移量提供可执行文件的字节。 若要使用相对虚拟地址，请实现 [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md) 接口。

## <a name="notes-for-callers"></a>对调用者的说明
 此方法由客户端应用程序实现，并作为读取文件的替代方法传递给 [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) 方法。

## <a name="requirements"></a>要求
 标头：Dia2.h

 库：diaguids.lib

 DLL：msdia80.dll

## <a name="see-also"></a>另请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
