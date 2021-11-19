---
description: 检索符号存储区中包含的所有表的枚举器。
title: IDiaSession::getEnumTables | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::getEnumTables method
ms.assetid: 66e0fba2-ca63-4e24-a46a-c99c7fb61dd1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9a90c9938481755e2e813343b60d7bf0f3ff375d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831865"
---
# <a name="idiasessiongetenumtables"></a>IDiaSession::getEnumTables
检索符号存储区中包含的所有表的枚举器。

## <a name="syntax"></a>语法

```C++
HRESULT getEnumTables (
    IDiaEnumTables** ppEnumTables
);
```

#### <a name="parameters"></a>参数
`ppEnumTables`

[out] 返回一个 [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md) 对象。 使用此接口枚举符号存储区中的表。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="example"></a>示例
此示例提供一个常规函数，该函数使用 `getEnumTables` 方法获取特定枚举器对象。 如果找到枚举器，则该函数返回可强制转换为所需接口的指针；否则，该函数返回 `NULL`。

```C++
IUnknown *GetTable(IDiaSession *pSession, REFIID iid)
{
    IUnknown *pUnknown = NULL;
    if (pSession != NULL)
    {
        CComPtr<IDiaEnumTables> pEnumTables;
        if (pSession->getEnumTables(&pEnumTables) == S_OK)
        {
            CComPtr<IDiaTable> pTable;
            DWORD celt = 0;
            while(pEnumTables->Next(1,&pTable,&celt) == S_OK &&
                  celt == 1)
            {
                if (pTable->QueryInterface(iid, (void **)pUnknown) == S_OK)
                {
                    break;
                }
                pTable = NULL;
            }
        }
    }
    return(pUnknown);
}
```

## <a name="see-also"></a>另请参阅
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
