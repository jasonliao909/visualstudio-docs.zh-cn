---
title: IDiaSymbol::get_baseType
description: 检索此符号的基类型
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_baseType method
ms.assetid: 5c69a241-a8d3-48ed-8b36-27463a196572
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: f3fe85f37d75db8a86f544908e23a0a229992e89
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832596"
---
# <a name="idiasymbolget_basetype"></a>IDiaSymbol::get_baseType
检索此符号的基类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_baseType (
    DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
`pRetVal`

[out]从 [BasicType 枚举枚举返回](../../debugger/debug-interface-access/basictype.md) 一个值，该值指定符号的基类型。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK` ;否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 表示 属性不可用于 符号。

## <a name="remarks"></a>备注
符号的基本类型可以通过先获取符号的类型，然后询问基类型的返回类型来确定。 请注意，某些符号可能没有基类型，例如结构名称。

## <a name="example"></a>示例

```C++
IDiaSymbol* pType;
CComPtr<IDiaSymbol> pBaseType;
if (pType->get_type( &pBaseType ) == S_OK)
{
    BasicType btBaseType;
    if (pBaseType->get_baseType((DWORD *)&btBaseType) == S_OK)
    {
        // Do something with basic type.
    }
}
```

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [BasicType 枚举](../../debugger/debug-interface-access/basictype.md)
- [IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)
