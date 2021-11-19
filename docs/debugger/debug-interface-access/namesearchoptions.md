---
description: 指定符号和文件名的搜索选项。
title: NameSearchOptions |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- NameSearchOptions enumeration
ms.assetid: 67dfbede-2678-47df-b664-5c49841d0b9b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 82bebfc05ac360ac2cb32eac70679805b592c4cf
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832807"
---
# <a name="namesearchoptions"></a>NameSearchOptions
指定符号和文件名的搜索选项。

## <a name="syntax"></a>语法

```C++
enum NameSearchOptions {
    nsNone,
    nsfCaseSensitive     = 0x1,
    nsfCaseInsensitive   = 0x2,
    nsfFNameExt          = 0x4,
    nsfRegularExpression = 0x8,
    nsfUndecoratedName   = 0x10,

// For backward compatibility:
    nsCaseSensitive           = nsfCaseSensitive,
    nsCaseInsensitive         = nsfCaseInsensitive,
    nsFNameExt                = nsfCaseInsensitive | nsfFNameExt,
    nsRegularExpression       = nsfRegularExpression | nsfCaseSensitive,
    nsCaseInRegularExpression = nsfRegularExpression | nsfCaseInsensitive
};
```

## <a name="elements"></a>元素
`nsNone` 未指定任何选项。

`nsfCaseSensitive` 应用区分大小写的名称匹配。

`nsfCaseInsensitive` 应用不区分大小写的名称匹配。

`nsfFNameExt` 将名称视为路径并应用文件名。 ext 名称匹配。

`nsfRegularExpression` 使用星号 ( * ) 和问号 (？ ) 作为通配符来应用区分大小写的名称匹配。  (不支持其他常见正则表达式字符。 ) 

`nsfUndecoratedName` 仅适用于具有未修饰名称和修饰名的符号。

## <a name="remarks"></a>备注
此枚举中的值将传递给以下方法：

- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)

- [IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)

- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)

## <a name="requirements"></a>要求
标头： dia2

## <a name="see-also"></a>另请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
