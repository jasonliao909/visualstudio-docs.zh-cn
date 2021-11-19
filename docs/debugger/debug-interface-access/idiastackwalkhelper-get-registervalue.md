---
description: IDiaStackWalkHelper：：get_registerValue检索寄存器的值。
title: IDiaStackWalkHelper::get_registerValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::get_registerValue method
ms.assetid: 46ac5eee-73a3-44a1-8635-6c58ba193cb6
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 5f5edbbe7e01e1b15f308687d58be0623521b1ce
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831778"
---
# <a name="idiastackwalkhelperget_registervalue"></a>IDiaStackWalkHelper::get_registerValue
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

[in]一 [个来自](../../debugger/debug-interface-access/cv-hreg-e.md) CV_HREG_e 枚举枚举的值，该值指定从哪个寄存器获取值。

 `pRetVal`

[out]返回寄存器的当前值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 尽管 参数的大小 `pRetVal` 大，但实现应只存储寄存器通常保存的项。 例如，8 位寄存器只保留给定值的最低 8 位。 从此方法返回时，此 8 位值将扩展为 64 位。

## <a name="see-also"></a>另请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [CV_HREG_e 枚举](../../debugger/debug-interface-access/cv-hreg-e.md)
