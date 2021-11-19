---
description: 检索名称和符号类型都匹配的特定父标识符的所有子级。
title: IDiaSession::findChildren | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findChildren method
ms.assetid: 5d19046f-f668-4aa9-8788-95cda9a98997
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 13a1bcf4a4d5fed816ef467cdc15c5c6fb974f18
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831925"
---
# <a name="idiasessionfindchildren"></a>IDiaSession::findChildren
检索名称和符号类型都匹配的特定父标识符的所有子级。

## <a name="syntax"></a>语法

```C++
HRESULT findChildren ( 
   IDiaSymbol*       parent,
   SymTagEnum        symtag,
   LPCOLESTR         name,
   DWORD             compareFlags,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>参数
 `parent`

[in] 表示父级的 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象。 如果该父符号是函数、模块或块，那么其词汇子级将以 `ppResult` 格式返回。 如果父符号是一种类型，则返回其类子级。 如果该参数是 `NULL`，那么 `symtag` 必须设置为 `SymTagExe` 或 `SymTagNull`，以便返回全局范围（.exe 文件）。

 `symtag`

[in] 指定要检索的子项的符号标记。 值来自 [SymTagEnum Enumeration](../../debugger/debug-interface-access/symtagenum.md) 枚举。 设置为 `SymTagNull` 以检索所有子项。

 `name`

[in] 指定要检索的子项的名称。 对于要检索的所有子项，设置为 `NULL`。

 `compareFlags`

[in] 指定应用于名称匹配的比较选项。 [NameSearchOptions Enumeration](../../debugger/debug-interface-access/namesearchoptions.md) 枚举中的值可以单独使用，也可以组合使用。

 `ppResult`

[out] 返回包含检索到的子符号列表的 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="example"></a>示例
 以下示例介绍如何查找与名称 `szVarName` 匹配的函数 `pFunc` 的局部变量。

```C++
IDiaEnumSymbols* pEnum;
pSession->findChildren( pFunc, SymTagData, szVarName, nsCaseSensitive, &pEnum );
```

## <a name="see-also"></a>另请参阅
- [概述](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [NameSearchOptions 枚举](../../debugger/debug-interface-access/namesearchoptions.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
