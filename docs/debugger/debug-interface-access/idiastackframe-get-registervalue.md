---
description: 检索存储在堆栈帧中的指定寄存器的值。
title: IDiaStackFrame::get_registerValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_registerValue method
ms.assetid: cbe3d8ac-319a-40ac-bc3e-4eb81b2d7807
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: e58f03a45b1fe680644c1bbc320383d6e3ac44ef
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831817"
---
# <a name="idiastackframeget_registervalue"></a>IDiaStackFrame::get_registerValue
检索存储在堆栈帧中的指定寄存器的值。

## <a name="syntax"></a>语法

```C++
HRESULT get_registerValue(
   ULONG      registerIndex,
   ULONGLONG *pRetVal
);
```

#### <a name="parameters"></a>参数
 `registerIndex`

[in] [CV_HREG_e Enumeration](../../debugger/debug-interface-access/cv-hreg-e.md) 枚举值之一。

 `pRetVal`

[out] 存储在寄存器中的值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
- [CV_HREG_e 枚举](../../debugger/debug-interface-access/cv-hreg-e.md)
