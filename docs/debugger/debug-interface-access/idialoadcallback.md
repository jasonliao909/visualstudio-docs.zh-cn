---
description: 从 DIA 符号定位过程接收回调，从而使用户界面能够报告定位尝试的进度。
title: IDiaLoadCallback | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback interface
ms.assetid: 2f18c64c-2cf0-43fc-a447-21e82702ca2a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9b5ef4523aa2b8acd098f8a9e46d5aa0009f9b37
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832039"
---
# <a name="idialoadcallback"></a>IDiaLoadCallback
从 DIA 符号定位过程接收回调，从而使用户界面能够报告定位尝试的进度。

## <a name="syntax"></a>语法

```
IDiaLoadCallback : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 此接口公开了以下方法：

|方法|说明|
|------------|-----------------|
|[IDiaLoadCallback::NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md)|在 .exe 文件中找到调试目录时调用。|
|[IDiaLoadCallback::NotifyOpenDBG](../../debugger/debug-interface-access/idialoadcallback-notifyopendbg.md)|在已打开候选 .dbg 文件时调用。|
|[IDiaLoadCallback::NotifyOpenPDB](../../debugger/debug-interface-access/idialoadcallback-notifyopenpdb.md)|在已打开候选 .pdb 文件时调用。|
|[IDiaLoadCallback::RestrictRegistryAccess](../../debugger/debug-interface-access/idialoadcallback-restrictregistryaccess.md)|确定是否可以使用注册表查询来查找符号搜索路径。|
|[IDiaLoadCallback::RestrictSymbolServerAccess](../../debugger/debug-interface-access/idialoadcallback-restrictsymbolserveraccess.md)|确定是否允许访问符号服务器来解析符号。|

## <a name="remarks"></a>备注
 客户端应用程序实现此接口，并在对 [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) 方法的调用中提供对它的引用。

 有关可对加载过程施加的其他限制，请参阅 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md) 接口。

## <a name="requirements"></a>要求
 标头：Dia2.h

 库：diaguids.lib

 DLL：msdia80.dll

## <a name="see-also"></a>另请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
