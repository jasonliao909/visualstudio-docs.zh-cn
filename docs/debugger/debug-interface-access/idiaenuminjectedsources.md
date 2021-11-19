---
description: 枚举数据源中包含的各种注入源。
title: IDiaEnumInjectedSources | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumInjectedSources interface
ms.assetid: f97e2392-22e1-48da-b7ce-ad94c8b684b0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: ea46cf39774e41e128a163c1a649bafb16c4b524
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832255"
---
# <a name="idiaenuminjectedsources"></a>IDiaEnumInjectedSources
枚举数据源中包含的各种注入源。

## <a name="syntax"></a>语法

```
IDiaEnumInjectedSources : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示了 的方法 `IDiaEnumInjectedSources` 。

|方法|说明|
|------------|-----------------|
|[IDiaEnumInjectedSources::get__NewEnum](../../debugger/debug-interface-access/idiaenuminjectedsources-get-newenum.md)|检索此 [枚举数的 IEnumVARIANT](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant) 接口版本。|
|[IDiaEnumInjectedSources::get_Count](../../debugger/debug-interface-access/idiaenuminjectedsources-get-count.md)|检索注入源的数量。|
|[IDiaEnumInjectedSources::Item](../../debugger/debug-interface-access/idiaenuminjectedsources-item.md)|通过索引检索注入的源。|
|[IDiaEnumInjectedSources::Next](../../debugger/debug-interface-access/idiaenuminjectedsources-next.md)|检索枚举序列中指定数量的注入源。|
|[IDiaEnumInjectedSources::Skip](../../debugger/debug-interface-access/idiaenuminjectedsources-skip.md)|跳过枚举序列中指定数量的注入源。|
|[IDiaEnumInjectedSources::Reset](../../debugger/debug-interface-access/idiaenuminjectedsources-reset.md)|将枚举序列重置为开头。|
|[IDiaEnumInjectedSources::Clone](../../debugger/debug-interface-access/idiaenuminjectedsources-clone.md)|创建一个枚举器，其中包含与当前枚举器相同的枚举状态。|

## <a name="remarks"></a>备注

## <a name="notes-for-callers"></a>调用方说明
通过调用具有特定源文件名称的 [IDiaSession：：findInjectedSource](../../debugger/debug-interface-access/idiasession-findinjectedsource.md) 方法，或者使用接口的 GUID 调用 [IDiaSession：：getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md) 方法，可获取此 `IDiaEnumInjectedSources` 接口。

## <a name="example"></a>示例
此示例演示如何获取 (函数 `GetEnumInjectedSources`) ， (`DumpAllInjectedSources` 接口) `IDiaEnumInjectedSources` 函数。 有关 [函数的实现，请参阅 IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md) `PrintPropertyStorage` 接口。 有关备用输出，请参阅 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md) 接口。

```C++

IDiaEnumInjectedSources* GetEnumInjectedSources(IDiaSession *pSession)
{
    IDiaEnumInjectedSources* pUnknown    = NULL;
    REFIID                   iid         = __uuidof(IDiaEnumInjectedSources);
    IDiaEnumTables*          pEnumTables = NULL;
    IDiaTable*               pTable      = NULL;
    ULONG                    celt        = 0;

    if (pSession->getEnumTables(&pEnumTables) != S_OK)
    {
        wprintf(L"ERROR - GetTable() getEnumTables\n");
        return NULL;
    }
    while (pEnumTables->Next(1, &pTable, &celt) == S_OK && celt == 1)
    {
        // There is only one table that matches the given iid
        HRESULT hr = pTable->QueryInterface(iid, (void**)&pUnknown);
        pTable->Release();
        if (hr == S_OK)
        {
            break;
        }
    }
    pEnumTables->Release();
    return pUnknown;
}

void DumpAllInjectedSources( IDiaSession* pSession)
{
    IDiaEnumInjectedSources* pEnumInjSources;

    pEnumInjSources = GetEnumInjectedSources(pSession);
    if (pEnumInjSources != NULL)
    {
        IDiaInjectedSource* pInjSource;
        ULONG celt = 0;

        while(pEnumInjSources->Next(1, &pInjSource, &celt) == S_OK &&
              celt == 1)
        {
            IDiaPropertyStorage *pPropertyStorage;
            if (pInjSource->QueryInterface(__uuidof(IDiaPropertyStorage),
                                          (void **)&pPropertyStorage) == S_OK)
            {
                PrintPropertyStorage(pPropertyStorage);
                pPropertyStorage->Release();
            }
            pInjSource->Release();
        }
        pEnumInjSources->Release();
    }
}
```

## <a name="requirements"></a>要求
标头：Dia2.h

库：diaguids.lib

DLL：msdia80.dll

## <a name="see-also"></a>另请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaSession::findInjectedSource](../../debugger/debug-interface-access/idiasession-findinjectedsource.md)
- [IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
