---
description: 程序数据库文件 (扩展 .pdb) 是一个二进制文件，其中包含在编译和链接项目的过程中收集的类型和符号调试信息。
title: 查询。Pdb 文件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- PDB files
- .pdb files, querying
ms.assetid: 8da07d1c-2712-45f9-8fbf-f34040408a8a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 4da3527b8f6834a7fb36077e73ec193204803d80
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832803"
---
# <a name="querying-the-pdb-file"></a>查询 .Pdb 文件
程序数据库文件 (扩展 .pdb) 是一个二进制文件，其中包含在编译和链接项目的过程中收集的类型和符号调试信息。 当使用 **/zi** 或 **/zi** 编译 C/c + + 程序或 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] 使用 **/Debug** 选项来编译 C/c + + 程序时，将创建 PDB 文件。 对于调试信息，对象文件包含对 .pdb 文件的引用。 有关 pdb 文件的详细信息，请参阅 [Pdb 文件](/previous-versions/visualstudio/visual-studio-2010/yd4f8bd1(v=vs.100))。 DIA 应用程序可以使用以下常规步骤来获取有关可执行映像中各种符号、对象和数据元素的详细信息。

### <a name="to-query-the-pdb-file"></a>查询 .pdb 文件

1. 通过创建 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md) 接口获取数据源。

    ```C++
    CComPtr<IDiaDataSource> pSource;
    hr = CoCreateInstance( CLSID_DiaSource,
                           NULL,
                           CLSCTX_INPROC_SERVER,
                           __uuidof( IDiaDataSource ),
                          (void **) &pSource);

    if (FAILED(hr))
    {
        Fatal("Could not CoCreate CLSID_DiaSource. Register msdia80.dll." );
    }
    ```

2. 调用 [IDiaDataSource：： loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) 或 [IDiaDataSource：： loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) 加载调试信息。

    ```C++
    wchar_t wszFilename[ _MAX_PATH ];
    mbstowcs( wszFilename, szFilename, sizeof( wszFilename )/sizeof( wszFilename[0] ) );
    if ( FAILED( pSource->loadDataFromPdb( wszFilename ) ) )
    {
        if ( FAILED( pSource->loadDataForExe( wszFilename, NULL, NULL ) ) )
        {
            Fatal( "loadDataFromPdb/Exe" );
        }
    }
    ```

3. 调用 [IDiaDataSource：： openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md) 以打开 [IDiaSession](../../debugger/debug-interface-access/idiasession.md) 以获取对调试信息的访问。

    ```C++
    CComPtr<IDiaSession> psession;
    if ( FAILED( pSource->openSession( &psession ) ) )
    {
        Fatal( "openSession" );
    }
    ```

4. 使用中的方法 `IDiaSession` 可以查询数据源中的符号。

    ```C++
    CComPtr<IDiaSymbol> pglobal;
    if ( FAILED( psession->get_globalScope( &pglobal) ) )
    {
        Fatal( "get_globalScope" );
    }
    ```

5. 使用 `IDiaEnum*` 接口枚举和扫描调试信息的符号或其他元素。

    ```C++
    CComPtr<IDiaEnumTables> pTables;
    if ( FAILED( psession->getEnumTables( &pTables ) ) )
    {
        Fatal( "getEnumTables" );
    }
    CComPtr< IDiaTable > pTable;
    while ( SUCCEEDED( hr = pTables->Next( 1, &pTable, &celt ) ) && celt == 1 )
    {
        // Do something with each IDiaTable.
    }
    ```

## <a name="see-also"></a>另请参阅
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
