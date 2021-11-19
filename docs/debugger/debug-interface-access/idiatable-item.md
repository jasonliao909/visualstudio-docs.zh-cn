---
description: 检索对表中指定项的引用。
title: IDiaTable：： Item |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable::Item method
ms.assetid: eae11b26-4807-400c-be25-e85bbc0c6b20
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 384aab56a17faa4ada1ff99fc43f13032d18db3d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832541"
---
# <a name="idiatableitem"></a>IDiaTable::Item
检索对表中指定项的引用。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   DWORD      index,
   IUnknown** element
);
```

#### <a name="parameters"></a>参数
 `index`

中表项在0到-1 范围内的索引 `count` ，其中 `count` 由 [IDiaTable：： get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)方法返回。

 `element`

弄返回一个 `IUnknown` 对象，该对象表示指定的表项。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 表表示对象的集合。 元素参数可以强制转换为相应的接口，具体取决于这些对象。 例如，如果表中包含 [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md) 对象，则可以将元素参数强制转换为 `IDiaSegment` 接口。

 在 `QueryInterface` [IDiaTable](../../debugger/debug-interface-access/idiatable.md) 接口中调用相应枚举器接口的方法，并使用枚举器的特定方法访问表内容，这种方法更常见。 有关示例，请参阅 [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md) 接口。

## <a name="see-also"></a>另请参阅
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
- [IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
