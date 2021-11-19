---
description: 按编译单位和名称检索源文件。
title: IDiaSession::findFile | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findFile method
ms.assetid: a215dc21-b316-40d7-9923-55bfa014976b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: d1d8d9b32e850214d45703107dcdc5e22a1b9a8d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831921"
---
# <a name="idiasessionfindfile"></a>IDiaSession::findFile
按编译单位和名称检索源文件。

## <a name="syntax"></a>语法

```C++
HRESULT findFile ( 
   IDiaSymbol*           pCompiland,
   LPCOLESTR             name,
   DWORD                 option,
   IDiaEnumSourceFiles** ppResult
);
```

#### <a name="parameters"></a>参数
 `pCompiland`

中表示要用作搜索上下文的编译单位的 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象。 将此参数设置为 `NULL` 可以在所有 compiland 中查找源文件。

 `name`

中指定要检索的源文件的名称。 将此参数设置为可 `NULL` 检索所有源文件。

 `option`

中指定应用于名称搜索的比较选项。 [NameSearchOptions 枚举](../../debugger/debug-interface-access/namesearchoptions.md)枚举中的值可以单独使用，也可以组合使用。

 `ppResult`

弄返回一个 [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md) 对象，该对象包含检索到的源文件的列表。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="example"></a>示例

```C++
IDiaEnumSourceFiles* pEnum;
pSession->findFile( NULL, L"sourcefile.cpp", nsFNameExt, &pEnum );
```

## <a name="see-also"></a>另请参阅
- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [NameSearchOptions 枚举](../../debugger/debug-interface-access/namesearchoptions.md)
