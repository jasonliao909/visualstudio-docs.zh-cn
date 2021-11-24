---
description: 检索调试流枚举器的 System.Runtime.InteropServices.ComTypes.IEnumVARIANT 版本。
title: IDiaEnumDebugStreams::get__NewEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreams::get__NewEnum method
ms.assetid: 972372ff-abfc-4987-a302-7788fab90348
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 887fe67dcb135e2bf1ea02690099356682e56403
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832302"
---
# <a name="idiaenumdebugstreamsget__newenum"></a>IDiaEnumDebugStreams::get__NewEnum
检索该枚举器的 <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> 版本。

## <a name="syntax"></a>语法

```C++
HRESULT get__NewEnum ( 
   IUnknown** pRetVal
);
```

#### <a name="parameters"></a>参数
 pRetVal

[out] 返回表示该枚举器 <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> 版本的 `IUnknown` 接口。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)
