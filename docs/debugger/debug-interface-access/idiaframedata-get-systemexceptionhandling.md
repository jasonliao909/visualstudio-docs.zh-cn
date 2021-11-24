---
description: IDiaFrameData::get_systemExceptionHandling 检索一个标记，该标记指示系统异常处理是否有效。
title: IDiaFrameData::get_systemExceptionHandling | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_systemExceptionHandling method
ms.assetid: e8df1972-913c-446c-9779-775575b0caa9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: e6ac56cb23c47ee1378b8ae5eb1d2a50a1c30c50
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832106"
---
# <a name="idiaframedataget_systemexceptionhandling"></a>IDiaFrameData::get_systemExceptionHandling
检索指示系统异常处理是否有效的标记。

## <a name="syntax"></a>语法

```C++
HRESULT get_systemExceptionHandling ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 pRetVal

[out] 如果系统异常处理有效，则返回 `TRUE`；否则返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 系统异常处理通常称为结构化异常处理。

 若要确定 C++ 异常处理是否有效，请调用 [IDiaFrameData::get_cplusplusExceptionHandling](../../debugger/debug-interface-access/idiaframedata-get-cplusplusexceptionhandling.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaFrameData::get_cplusplusExceptionHandling](../../debugger/debug-interface-access/idiaframedata-get-cplusplusexceptionhandling.md)
