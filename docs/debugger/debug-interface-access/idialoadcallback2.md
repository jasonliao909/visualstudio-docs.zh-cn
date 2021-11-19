---
description: 从 DIA 符号定位过程接收回调，从而允许对定位过程施加限制。
title: IDiaLoadCallback2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback2 interface
ms.assetid: 9a44277d-cbed-4811-9bad-5a2aa0f09323
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: adf24a1790e40e9ebdd885e6eaec73e152013b5f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832026"
---
# <a name="idialoadcallback2"></a>IDiaLoadCallback2
从 DIA 符号定位过程接收回调，从而允许对定位过程施加限制。

## <a name="syntax"></a>语法

```
IDiaLoadCallback2 : IDiaLoadCallback
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了 [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md) 接口中的方法外，此接口还公开以下方法：

|方法|说明|
|------------|-----------------|
|[IDiaLoadCallback2::RestrictOriginalPathAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictoriginalpathaccess.md)|确定是否在原始调试目录中查找 .pdb 文件。|
|[IDiaLoadCallback2::RestrictReferencePathAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictreferencepathaccess.md)|确定是否允许在 .exe 文件所在的路径中查找 .pdb 文件。|
|[IDiaLoadCallback2::RestrictDBGAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictdbgaccess.md)|确定是否允许从 .dbg 文件中查找调试信息。|
|[IDiaLoadCallback2::RestrictSystemRootAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictsystemrootaccess.md)|确定是否允许在系统根目录中搜索 .pdb 文件。|

## <a name="remarks"></a>备注
 客户端应用程序实现此接口，并在对 [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) 方法的调用中提供对它的引用。 请记得同时也在 [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md) 接口中实现所有方法。

## <a name="requirements"></a>要求
 标头：Dia2.h

 库：diaguids.lib

 DLL：msdia80.dll

## <a name="see-also"></a>另请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)
