---
description: 确定源文件中指定行号所在的或附近的编译单位的行号。
title: IDiaSession::findLinesByLinenum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findLinesByLinenum method
ms.assetid: 76d5622d-9a91-4c2a-a98f-263af5d1daef
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 54a5d74e65879873db3d6a9394b9f7a74e6d0a64
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831888"
---
# <a name="idiasessionfindlinesbylinenum"></a>IDiaSession::findLinesByLinenum
确定源文件中指定行号所在的或附近的编译单位的行号。

## <a name="syntax"></a>语法

```C++
HRESULT findLinesByLinenum ( 
    IDiaSymbol*           compiland,
    IDiaSourceFile*       file,
    DWORD                 linenum,
    DWORD                 column,
    IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
`compiland`

[in] 一个 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象，表示要在其中搜索行号的编译单位。 此参数不能为 `NULL`。

`file`

[in] 一个 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) 对象，表示要在其中搜索的源文件。 此参数不能为 `NULL`。

`linenum`

[in] 指定一个从 1 开始的行号。

> [!NOTE]
> 不能使用零指定所有行（使用 [IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md) 方法查找所有行）。

`column`

[in] 指定列号。 使用零指定所有列。 一列是偏移到一行的一个字节。

`ppResult`

[out] 返回一个 [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md) 对象，该对象包含检索到的行号的列表。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="example"></a>示例
下面的示例展示了如何打开源文件、枚举此文件贡献的编译单位，以及在源文件中找到每个编译单位开始的行号。

```C++
void ShowLinesInCompilands(IDiaSession *pSession, LPCOLESTR filename)
{
    IDiaEnumSourceFiles* pEnum;
    IDiaSourceFile*      pFile;
    DWORD                celt;

    pSession->findFile ( NULL, filename, nsFNameExt, &pEnum );
    while ( pEnum->Next ( 1, &pFile, &celt ) == S_OK ) // for each file
    {
        IDiaEnumSymbols* pEnumCompilands;
        IDiaSymbol* pCompiland;

        pFile->get_compilands ( &pEnumCompilands );
        // for each compiland
        while ( pEnumCompilands->Next ( 1, &pCompiland, &celt ) == S_OK )
        {
            IDiaEnumLineNumbers* pEnum;
            // Find first compiland closest to line 1 of the file.
            if (pSession->findLinesByLinenum( pCompiland, pFile, 1, 0, &pEnum ) == S_OK)
            {
                IDiaLineNumber *pLineNumber;
                DWORD lineCount;
                while ( pEnum->Next(1,&pLineNumber,&lineCount) == S_OK)
                {
                    DWORD lineNum;
                    if (pLineNumber->get_line(&lineNum) == S_OK)
                    {
                        printf("compiland starts in source at line number = %lu\n",lineNum);
                    }
                }
            }
        }
    }
}
```

## <a name="see-also"></a>另请参阅
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
