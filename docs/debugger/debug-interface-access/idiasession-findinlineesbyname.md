---
description: 检索一个枚举，该枚举允许客户端遍历与指定名称匹配的所有内联函数的行号信息。
title: IDiaSession::findInlineesByName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 9860336d-f703-4ecb-bfc4-3f5beb175a76
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: e06442d07bf13a24a59c9bd365fb5861f52ab527
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831909"
---
# <a name="idiasessionfindinlineesbyname"></a>IDiaSession::findInlineesByName
检索一个枚举，该枚举允许客户端遍历与指定名称匹配的所有内联函数的行号信息。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineesByName ( 
   LPCOLESTR             name,
   DWORD                 option,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
 `name`

[in] 指定要用于比较的名称。

 `option`

[in] 指定应用于名称搜索的比较选项。 [NameSearchOptions Enumeration](../../debugger/debug-interface-access/namesearchoptions.md) 枚举中的值可以单独使用，也可以组合使用。

 `ppResult`

[out] 返回一个 [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md) 对象，该对象包含检索到的行号的列表。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
