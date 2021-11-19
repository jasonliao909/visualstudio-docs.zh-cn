---
description: 检索与名称和符号类型匹配的指定父标识符的所有子级。
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
检索与名称和符号类型匹配的指定父标识符的所有子级。

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

中表示父对象的 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象。 如果此父符号是函数、模块或块，则将在中返回其词法子对象 `ppResult` 。 如果父符号是类型，则返回其类子级。 如果此参数为 `NULL` ，则 `symtag` 必须将设置为 `SymTagExe` 或 `SymTagNull` ，这将返回全局范围 (.exe 文件) 。

 `symtag`

中指定要检索的子级的符号标记。 值取自 [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md) 枚举。 设置为 `SymTagNull` 可检索所有子级。

 `name`

中指定要检索的子项的名称。 `NULL`对于要检索的所有子级，将设置为。

 `compareFlags`

中指定应用于名称匹配的比较选项。 [NameSearchOptions 枚举](../../debugger/debug-interface-access/namesearchoptions.md)枚举中的值可以单独使用，也可以组合使用。

 `ppResult`

弄返回一个 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) 对象，该对象包含所检索到的子符号的列表。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="example"></a>示例
 下面的示例演示如何查找与名称匹配的函数的局部变量 `pFunc` `szVarName` 。

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
