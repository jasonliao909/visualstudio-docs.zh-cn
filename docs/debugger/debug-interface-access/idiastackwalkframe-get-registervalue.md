---
description: IDiaStackWalkFrame::get_registerValue 检索寄存器的值。
title: IDiaStackWalkFrame::get_registerValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame::get_registerValue method
ms.assetid: ca3c20a9-934a-4b2c-a7f6-7d06e8611ff2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 925efe875143a920188cd3d0cb4b387b45789475
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832461"
---
# <a name="idiastackwalkframeget_registervalue"></a>IDiaStackWalkFrame::get_registerValue
检索寄存器的值。

## <a name="syntax"></a>语法

```C++
HRESULT get_registerValue ( 
   DWORD      index,
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `index`

[in] 一个来自 [CV_HREG_e 枚举](../../debugger/debug-interface-access/cv-hreg-e.md)的值，指定要获取其值的寄存器。

 `pRetVal`

[out] 返回寄存器的当前值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
- [CV_HREG_e 枚举](../../debugger/debug-interface-access/cv-hreg-e.md)
