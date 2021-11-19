---
description: IDiaStackFrame：： get_systemExceptionHandling 检索一个标志，该标志指示系统异常处理是否有效。
title: IDiaStackFrame::get_systemExceptionHandling | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_systemExceptionHandling
ms.assetid: c76cf265-dea0-4159-883f-32b50bbef044
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: c8b5e0966465d807e6fac26c98fd9fb5d922abba
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831813"
---
# <a name="idiastackframeget_systemexceptionhandling"></a>IDiaStackFrame::get_systemExceptionHandling
检索一个标志，该标志指示系统异常处理是否有效。

## <a name="syntax"></a>语法

```C++
HRESULT get_systemExceptionHandling ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄 `TRUE` 如果系统异常处理对此帧有效，则返回; 否则返回 `FALSE` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 `S_FALSE`如果该属性不受支持，则返回。 否则，返回错误代码。

## <a name="remarks"></a>备注
 系统异常处理也称为结构化异常处理。 这与 c + + 异常处理不同。

 若要确定 c + + 异常处理是否有效，请调用 [IDiaStackFrame：： get_cplusplusExceptionHandling](../../debugger/debug-interface-access/idiastackframe-get-cplusplusexceptionhandling.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
- [IDiaStackFrame::get_cplusplusExceptionHandling](../../debugger/debug-interface-access/idiastackframe-get-cplusplusexceptionhandling.md)
