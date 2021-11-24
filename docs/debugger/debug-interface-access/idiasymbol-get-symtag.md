---
description: 检索符号类型分类器。
title: IDiaSymbol::get_symTag | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_symTag method
ms.assetid: 139a35bd-faeb-4878-be72-394dedfbb18f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: ad31fc4290daeec60f57c510c7a48cd41343d954
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831723"
---
# <a name="idiasymbolget_symtag"></a>IDiaSymbol::get_symTag
检索符号类型分类器。

## <a name="syntax"></a>语法

```C++
HRESULT get_symTag ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 从 [SymTagEnum Enumeration](../../debugger/debug-interface-access/symtagenum.md) 枚举返回一个值，用于指定符号类型分类器。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="example"></a>示例

```C++
IDiaSymbol* pType;
DWORD       tag = 0;
pType->get_symTag( &tag );
```

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
