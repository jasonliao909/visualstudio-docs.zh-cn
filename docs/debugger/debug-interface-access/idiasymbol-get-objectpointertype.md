---
description: 检索类方法的对象指针的类型。
title: IDiaSymbol::get_objectPointerType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_objectPointerType method
ms.assetid: bce193b9-67b0-4c35-96e5-6a664937322e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 0695ba8dbe0c5846f8c7495600e71d89fb0aa5c6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832776"
---
# <a name="idiasymbolget_objectpointertype"></a>IDiaSymbol::get_objectPointerType
检索类方法的对象指针的类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_objectPointerType ( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回一个 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象，该对象表示类方法的对象指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 此属性仅适用于具有 `SymTagFunctionType` 的 [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)类型的符号。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
