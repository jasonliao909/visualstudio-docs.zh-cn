---
description: 枚举数据源中包含的各种表。
title: IDiaEnumTables | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables interface
ms.assetid: 016190c5-09e4-48f2-bf60-9b02603a03e0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: bea0f72726ed8a484aa520ed8733b06fda619a6a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832140"
---
# <a name="idiaenumtables"></a>IDiaEnumTables
枚举数据源中包含的各种表。

## <a name="syntax"></a>语法

```
IDiaEnumTables : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 `IDiaEnumTables` 方法。

|方法|说明|
|------------|-----------------|
|[IDiaEnumTables::get__NewEnum](../../debugger/debug-interface-access/idiaenumtables-get-newenum.md)|检索该枚举器的 [IEnumVARIANT Interface](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant) 版本。|
|[IDiaEnumTables::get_Count](../../debugger/debug-interface-access/idiaenumtables-get-count.md)|检索表的数量。|
|[IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)|通过索引或名称检索表。|
|[IDiaEnumTables::Next](../../debugger/debug-interface-access/idiaenumtables-next.md)|检索枚举序列中指定数目的表。|
|[IDiaEnumTables::Skip](../../debugger/debug-interface-access/idiaenumtables-skip.md)|跳过枚举序列中指定数量的表。|
|[IDiaEnumTables::Reset](../../debugger/debug-interface-access/idiaenumtables-reset.md)|将枚举序列重置到开头。|
|[IDiaEnumTables::Clone](../../debugger/debug-interface-access/idiaenumtables-clone.md)|创建一个枚举器，其中包含与当前枚举器相同的枚举状态。|

## <a name="remarks"></a>备注

## <a name="notes-for-callers"></a>对调用者的说明
通过调用 [IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md) 方法获取此接口。

## <a name="example"></a>示例
此示例演示如何从会话获取 `IDiaEnumTables` 接口。 有关使用表的更完整示例，请参阅 [IDiaTable](../../debugger/debug-interface-access/idiatable.md) 接口。

```C++
void ShowTableNames(IDiaSession *pSession)
{
    CComPtr<IDiaEnumTables> pTables;
    if ( FAILED( psession->getEnumTables( &pTables ) ) )
    {
        Fatal( "getEnumTables" );
    }
    // Do something with table
}
```

## <a name="requirements"></a>要求
标头：Dia2.h

库：diaguids.lib

DLL：msdia80.dll

## <a name="see-also"></a>另请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)
