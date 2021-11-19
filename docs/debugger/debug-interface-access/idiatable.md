---
description: 枚举 DIA 数据源表。
title: IDiaTable | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable interface
ms.assetid: c99a2c44-7b72-4e3c-b963-25fe3df3a555
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 7f8dc87343a425d87c2936b6667f350c456b45cf
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831788"
---
# <a name="idiatable"></a>IDiaTable
枚举 DIA 数据源表。

## <a name="syntax"></a>语法

```
IDiaTable : IEnumUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示了 `IDiaTable` 方法。

|方法|说明|
|------------|-----------------|
|[IDiaTable::get__NewEnum](../../debugger/debug-interface-access/idiatable-get-newenum.md)|检索该枚举器的 [IEnumVARIANT Interface](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant) 版本。|
|[IDiaTable::get_name](../../debugger/debug-interface-access/idiatable-get-name.md)|检索表名称。|
|[IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)|检索表中的项数。|
|[IDiaTable::Item](../../debugger/debug-interface-access/idiatable-item.md)|检索对特定条目索引的引用。|

## <a name="remarks"></a>备注
此接口实现 Microsoft.VisualStudio.OLE.Interop 命名空间中的 `IEnumUnknown` 枚举方法。 相比 [IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md) 和 [IDiaTable::Item](../../debugger/debug-interface-access/idiatable-item.md) 方法，`IEnumUnknown` 枚举接口在循环访问表内容时要高效得多。

`IDiaTable::Item` 方法或 `Next` 方法（在 Microsoft.VisualStudio.OLE.Interop 命名空间中）返回的 `IUnknown` 接口的解释取决于表类型。 例如，如果 `IDiaTable` 接口表示注入源代码列表，则应对 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md) 接口查询 `IUnknown` 接口。

## <a name="notes-for-callers"></a>对调用者的说明
通过调用 [IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md) 或 [IDiaEnumTables::Next](../../debugger/debug-interface-access/idiaenumtables-next.md) 方法获取此接口。

以下接口是使用 `IDiaTable` 接口实现的（也就是说，你可以在下列接口之一查询 `IDiaTable` 接口）：

- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)

- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)

- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)

- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)

- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)

- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)

- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)

## <a name="example"></a>示例
第一个函数 `ShowTableNames` 显示会话中所有表的名称。 第二个函数 `GetTable` 在所有表中搜索实现指定接口的表。 第三个函数 `UseTable` 演示如何使用 `GetTable` 函数。

> [!NOTE]
> `CDiaBSTR` 是一个类，在实例化超出范围时，它会包装 `BSTR` 并自动处理释放字符串。

```C++
void ShowTableNames(IDiaSession *pSession)
{
    CComPtr<IDiaEnumTables> pTables;
    if ( FAILED( psession->getEnumTables( &pTables ) ) )
    {
        Fatal( "getEnumTables" );
    }
    CComPtr< IDiaTable > pTable;
    while ( SUCCEEDED( hr = pTables->Next( 1, &pTable, &celt ) )
            && celt == 1 )
    {
        CDiaBSTR bstrTableName;
        if ( pTable->get_name( &bstrTableName ) != 0 )
        {
            Fatal( "get_name" );
        }
        printf( "Found table: %ws\n", bstrTableName );
    }

// Searches the list of all tables for a table that supports
// the specified interface.  Use this function to obtain an
// enumeration interface.
HRESULT GetTable(IDiaSession* pSession,
                 REFIID       iid,
                 void**       ppUnk)
{
    CComPtr<IDiaEnumTables> pEnumTables;
    HRESULT hResult;

    if (FAILED(pSession->getEnumTables(&pEnumTables)))
        Fatal("getEnumTables");

    CComPtr<IDiaTable> pTable;
    ULONG celt = 0;
    while (SUCCEEDED(hResult = pEnumTables->Next(1, &pTable, &celt)) &&
           celt == 1)
    {
        if (pTable->QueryInterface(iid, (void**)ppUnk) == S_OK)
        {
            return S_OK;
        }
        pTable = NULL;
    }

    if (FAILED(hResult))
        Fatal("EnumTables->Next");

    return E_FAIL;
}

// This function shows how to use the GetTable function.
void UseTable(IDiaSession *pSession)
{
    CComPtr<IDiaEnumSegments> pEnumSegments;
    if (SUCCEEDED(GetTable(pSession, __uuidof(IDiaEnumSegments), &pEnumSegments)))
    {
        // Do something with pEnumSegments.
    }
}
```

## <a name="requirements"></a>要求
标头：Dia2.h

库：diaguids.lib

DLL：msdia80.dll

## <a name="see-also"></a>另请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)
- [IDiaEnumTables::Next](../../debugger/debug-interface-access/idiaenumtables-next.md)
