---
description: IDiaStackWalkHelper::put_registerValue 设置寄存器的值。
title: IDiaStackWalkHelper::put_registerValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::put_registerValue method
ms.assetid: 8f02ce54-ef59-455f-8aa6-dc26761c7aff
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: a93a21b10f6793cd75c6999998bc21b923ce69d7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831770"
---
# <a name="idiastackwalkhelperput_registervalue"></a>IDiaStackWalkHelper::put_registerValue
设置寄存器的值。

## <a name="syntax"></a>语法

```C++
HRESULT put_registerValue ( 
   DWORD     index,
   ULONGLONG NewVal
);
```

#### <a name="parameters"></a>参数
 `index`

[in] [CV_HREG_e Enumeration](../../debugger/debug-interface-access/cv-hreg-e.md) 枚举的一个值，指定要写入的寄存器。

 `NewVal`

[in] 新寄存器值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="remarks"></a>备注
 无论值的大小如何，实现应该只存储寄存器通常保留的内容。 例如，8 位寄存器将只保留给定值的最低 8 位。

## <a name="see-also"></a>另请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [CV_HREG_e 枚举](../../debugger/debug-interface-access/cv-hreg-e.md)
