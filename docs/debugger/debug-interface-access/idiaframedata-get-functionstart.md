---
description: IDiaFrameData：：get_functionStart检索一个标志，该标志指示块是否包含函数的入口点。
title: IDiaFrameData::get_functionStart | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_functionStart method
ms.assetid: 49fd24fb-65c2-4812-8303-56a968353e1b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: b33b08a00d62c89228346e5171219a801b0ad2a9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832125"
---
# <a name="idiaframedataget_functionstart"></a>IDiaFrameData::get_functionStart
检索一个标志，该标志指示 块是否包含函数的入口点。

## <a name="syntax"></a>语法

```C++
HRESULT get_functionStart ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]如果 `TRUE` 块包含入口点，则返回 ;否则返回 `FALSE` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果 `S_FALSE` 不支持此属性，则返回 。 否则，返回错误代码。

## <a name="remarks"></a>备注
 堆栈帧可能不是函数的开始，因为该帧表示插入到函数中的内联方法或函数。

## <a name="see-also"></a>另请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
