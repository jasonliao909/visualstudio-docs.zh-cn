---
description: 检索表示此符号类型的符号。
title: IDiaSymbol::get_type | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_type method
ms.assetid: 1c6a4176-dd4e-4c22-8b8f-0e559fc078ba
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 6d9025a51e06158448cf273a60f95ac40b8f99a9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832652"
---
# <a name="idiasymbolget_type"></a>IDiaSymbol::get_type
检索表示此符号类型的符号。

## <a name="syntax"></a>语法

```C++
HRESULT get_type (
    IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>参数
`pRetVal`

[out] 返回表示此符号类型的 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
若要确定符号的类型，必须调用此方法并检查生成的 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象。 请注意，符号可能没有类型。 例如，结构的名称没有类型，但它可能有子符号（使用 [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md) 方法检查这些子符号）。

## <a name="example"></a>示例

```C++
IDiaSymbol*         pType;
CComPtr<IDiaSymbol> pBaseType;
if (SUCCEEDED(pType->get_type( &pBaseType ))) {
    BasicType btBaseType;
    if (SUCCEEDED(pBaseType->get_baseType((DWORD *)&btBaseType))) {
        // Do something with basic type.
    }
}
```

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
