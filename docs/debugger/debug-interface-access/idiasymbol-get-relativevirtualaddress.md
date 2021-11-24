---
description: 检索位置的相对虚拟地址 (RVA)。
title: IDiaSymbol::get_relativeVirtualAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_relativeVirtualAddress method
ms.assetid: e37219e3-c021-4057-9ec8-4f7cf3c13a15
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: afd85895077291bd6ab93b2b099058744d8e7987
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832719"
---
# <a name="idiasymbolget_relativevirtualaddress"></a>IDiaSymbol::get_relativeVirtualAddress
检索位置的相对虚拟地址 (RVA)。 当 [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)设置为 `LocIsStatic` 时使用。

## <a name="syntax"></a>语法

```C++
HRESULT get_relativeVirtualAddress ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回位置的相对虚拟地址。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="example"></a>示例

```C++
IDiaSymbol* pSymbol;
DWORD       rva;
pSymbol->get_relativeVirtualAddress( &rva );
```

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)
