---
description: 在 .exe 文件中找到调试目录时调用。
title: IDiaLoadCallback::NotifyDebugDir | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::NotifyDebugDir method
ms.assetid: bd04e2f6-0dbf-4742-a556-96f2cd99aa19
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 48e87a968eea1ad35796a495d76584488bdac332
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832047"
---
# <a name="idialoadcallbacknotifydebugdir"></a>IDiaLoadCallback::NotifyDebugDir
在 .exe 文件中找到调试目录时调用。

## <a name="syntax"></a>语法

```C++
HRESULT NotifyDebugDir ( 
   BOOL  fExecutable,
   DWORD cbData,
   BYTE  data[]
);
```

#### <a name="parameters"></a>参数
 `fExecutable`

[in] `TRUE` 如果调试目录是从可执行文件中读取 (而不是) 的 dbg 文件中读取。

 `cbData`

中调试目录中数据的字节计数。

 `data[]`

中用调试目录填充的数组。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 通常会忽略返回代码。

## <a name="remarks"></a>备注
 当处理可执行文件时， [IDiaDataSource：： loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) 方法会调用此回调。

 此方法不再需要客户端对可执行文件和/或调试文件进行反向工程以支持除 .pdb 文件中找到的信息以外的调试信息。 使用此数据，客户端可以识别可用的调试信息的类型，以及它是位于可执行文件中还是在 dbg 文件中。

 大多数客户端不需要此回调，因为 `IDiaDataSource::loadDataForExe` 当需要为符号提供服务时，方法会以透明方式打开 .pdb 和 dbg 文件。

## <a name="see-also"></a>另请参阅
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
