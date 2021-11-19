---
description: 检索包含指向参数的基指针的寄存器的 ID。
title: IDiaSymbol::get_paramBasePointerRegisterId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_paramBasePointerRegisterId method
ms.assetid: 9f5caeb4-5c88-4054-bf8b-50d34bbbf8c5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: f1213f1b201b76c31bed1f494bdd62710a9231aa
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832455"
---
# <a name="idiasymbolget_parambasepointerregisterid"></a>IDiaSymbol::get_paramBasePointerRegisterId
检索包含指向参数的基指针的寄存器的 ID。 当 [SymTagEnum 枚举设置为](../../debugger/debug-interface-access/symtagenum.md) 时，请使用 `SymTagFunction` 。

## <a name="syntax"></a>语法

```C++
HRESULT get_paramBasePointerRegisterId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回寄存器的 ID，该寄存器包含指向参数的基指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 表示属性不可用于符号。

## <a name="remarks"></a>备注

## <a name="requirements"></a>要求
 标头：Dia2.h

 库：diaguids.lib

 DLL：msdia100.dll

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
