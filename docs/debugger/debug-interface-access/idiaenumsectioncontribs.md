---
description: 枚举数据源中包含的各种节发布。
title: IDiaEnumSectionContribs | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs interface
ms.assetid: 0d6c0632-310f-4a99-8921-58149a1817e3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: d56b5aa6bb35aa65b1e3736359fe0774c59fd1a1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832222"
---
# <a name="idiaenumsectioncontribs"></a>IDiaEnumSectionContribs
枚举数据源中包含的各种节发布。

## <a name="syntax"></a>语法

```
IDiaEnumSectionContribs : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示的方法 `IDiaEnumSectionContribs` 。

|方法|说明|
|------------|-----------------|
|[IDiaEnumSectionContribs::get__NewEnum](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-newenum.md)|检索此枚举器的 [IEnumVARIANT 接口](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant) 版本。|
|[IDiaEnumSectionContribs::get_Count](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-count.md)|检索部分基值。|
|[IDiaEnumSectionContribs::Item](../../debugger/debug-interface-access/idiaenumsectioncontribs-item.md)|通过索引检索节基值。|
|[IDiaEnumSectionContribs::Next](../../debugger/debug-interface-access/idiaenumsectioncontribs-next.md)|检索枚举序列中指定数目的节内容。|
|[IDiaEnumSectionContribs::Skip](../../debugger/debug-interface-access/idiaenumsectioncontribs-skip.md)|跳过枚举序列中指定数量的节发布。|
|[IDiaEnumSectionContribs::Reset](../../debugger/debug-interface-access/idiaenumsectioncontribs-reset.md)|将枚举序列重置到开始处。|
|[IDiaEnumSectionContribs::Clone](../../debugger/debug-interface-access/idiaenumsectioncontribs-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|

## <a name="remarks"></a>备注

## <a name="note-for-callers"></a>调用方的注释
从 [IDiaSession：： getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md) 方法获取此接口。 参阅示例了解详细信息。

## <a name="example"></a>示例
此示例演示如何获取 (`GetEnumSectionContribs` 函数) 并使用 `ShowSectionContribs`) 接口 (函数 `IDiaEnumSectionContribs` 。 有关使用节发布的更完整示例，请参阅 [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md) 接口。

```C++

IDiaEnumSectionContribs* GetEnumSectionContribs(IDiaSession *pSession)
{
    IDiaEnumSectionContribs* pUnknown    = NULL;
    REFIID                   iid         = __uuidof(IDiaEnumSectionContribs);
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

void ShowSectionContribs(IDiaSession *pSession)
{
    IDiaEnumSectionContribs* pEnumSectionContribs;

    pEnumSectionContribs = GetEnumSectionContribs(pSession);
    if (pSectionContrib != NULL)
    {
        IDiaSectionContrib* pSectionContrib;
        ULONG celt = 0;

        while(pEnumSectionContribs->Next(1, &pSectionContrib, &celt) == S_OK &&
              celt == 1)
        {
            PrintSectionContrib(pSectionContrib, pSession);
            pSectionContrib->Release();
        }
        pSectionContrib->Release();
    }
}
```

## <a name="requirements"></a>要求
标头： Dia2

库： diaguids

DLL： msdia80.dll

## <a name="see-also"></a>另请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
