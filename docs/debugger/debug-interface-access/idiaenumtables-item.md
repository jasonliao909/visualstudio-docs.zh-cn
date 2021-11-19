---
description: 通过索引或名称检索表。
title: IDiaEnumTables::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Item method
ms.assetid: d65ab262-10c6-48ce-95a3-b5e4cb2c85af
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 30e224b7edb621cb31d4124ac092e39e53f801fd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832146"
---
# <a name="idiaenumtablesitem"></a>IDiaEnumTables::Item
通过索引或名称检索表。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   VARIANT     index,
   IDiaTable** table
);
```

#### <a name="parameters"></a>参数
 `index`

[in] 要检索的 [IDiaTable](../../debugger/debug-interface-access/idiatable.md) 的索引或名称。 如果使用整数变体，则它必须在 0 到 `count`-1 范围内，其中 `count` 由 [IDiaEnumTables::get_Count](../../debugger/debug-interface-access/idiaenumtables-get-count.md) 方法返回。

 `table`

[out] 返回表示所需表的 [IDiaTable](../../debugger/debug-interface-access/idiatable.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="remarks"></a>备注
 如果指定了字符串变体，则字符串将命名特定表。 该名称应该是[常量（调试接口访问 SDK）](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md)中定义的表名之一。

## <a name="example"></a>示例

```C++
VARIANT var;
var.vt = VT_BSTR;
var.bstrVal = SysAllocString(DiaTable_Symbols );
IDiaTable* pTable;
pEnumTables->Item( var, &pTable );
```

## <a name="see-also"></a>另请参阅
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
- [IDiaEnumTables::get_Count](../../debugger/debug-interface-access/idiaenumtables-get-count.md)
- [常量（调试接口访问 SDK）](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md)
