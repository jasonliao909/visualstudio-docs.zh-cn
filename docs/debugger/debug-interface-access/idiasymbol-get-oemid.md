---
description: 检索符号的原始设备制造商 (OEM) ID 值。
title: IDiaSymbol::get_oemId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_oemId method
ms.assetid: c472830f-c3eb-46ab-9498-cd637763d241
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: fe88b4c523e71f9100c67736cfbc2f224df16c93
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832516"
---
# <a name="idiasymbolget_oemid"></a>IDiaSymbol::get_oemId
检索符号的原始设备制造商 (OEM) ID 值。

## <a name="syntax"></a>语法

```C++
HRESULT get_oemId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回标识 OEM 的唯一值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 此属性仅适用于具有 `SymTagCustomType` 的 [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)类型的符号。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
