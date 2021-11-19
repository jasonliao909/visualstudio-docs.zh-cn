---
description: IDiaFrameData::get_allocatesBasePointer 检索一个标记，该标记指示是否为此地址范围内的代码分配基指针。
title: IDiaFrameData::get_allocatesBasePointer | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_allocatesBasePointer method
ms.assetid: 8a33db5d-008c-4fe5-b64f-210c9b77f686
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: fb43d88fbe4bb607daaf6ed7e5b3c8641bbcf713
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832129"
---
# <a name="idiaframedataget_allocatesbasepointer"></a>IDiaFrameData::get_allocatesBasePointer
检索一个标记，该标记指示是否为此地址范围内的代码分配基指针。 不推荐使用此方法。

## <a name="syntax"></a>语法

```C++
HRESULT get_allocatesBasePointer ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 如果分配基指针，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此属性应仅由以前访问过 FPO_DATA 的代码使用，或在 [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md) 方法返回的程序字符串为 `NULL` 时使用。 否则，程序字符串将包含计算先前寄存器值所需的所有信息。

## <a name="see-also"></a>另请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)
