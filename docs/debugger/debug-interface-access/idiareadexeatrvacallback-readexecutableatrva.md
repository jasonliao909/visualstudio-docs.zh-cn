---
description: 从可执行文件读取 RVA (指定相对虚拟地址) 字节数。
title: IDiaReadExeAtRVACallback::ReadExecutableAtRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtRVACallback::ReadExecutableAtRVA method
ms.assetid: 3c1e965f-8f05-41a8-86d8-01830b2377c9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: d98eb6f6a50b7dace957b7012775746e90564bbd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832000"
---
# <a name="idiareadexeatrvacallbackreadexecutableatrva"></a>IDiaReadExeAtRVACallback::ReadExecutableAtRVA
从可执行文件读取 RVA (指定相对虚拟地址) 字节数。

## <a name="syntax"></a>语法

```C++
HRESULT ReadExecutableAtRVA ( 
   DWORD  relativeVirtualAddress,
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[]
);
```

#### <a name="parameters"></a>参数
 `relativeVirtualAddress`

[in]可执行文件中要开始读取的 RVA。

 `cbData`

[in]要读取的字节数。

 `pcbData`

[out]返回读取的字节数。

 `data[]`

[in， out]用从文件中读取的字节填充的数组。

## <a name="remarks"></a>备注
 DIA 支持代码调用此方法，以使用相对虚拟地址从可执行文件加载数据字节。 调用此方法以支持 [IDiaDataSource：：loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
