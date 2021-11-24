---
description: 通过索引检索节贡献。
title: IDiaEnumSectionContribs::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Item method
ms.assetid: 63a28f23-0ca0-44a7-b11b-ca0206d642a0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: c18f39898347313784e6201aedbc02018771e6f5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832228"
---
# <a name="idiaenumsectioncontribsitem"></a>IDiaEnumSectionContribs::Item
通过索引检索节贡献。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   DWORD                index,
   IDiaSectionContrib** section
);
```

#### <a name="parameters"></a>参数
 索引

[in] 要检索的 [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md) 对象的索引。 索引在 0 到 `count`-1 范围内，其中 `count` 由 [IDiaEnumSectionContribs::get_Count](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-count.md) 方法返回。

 section

[out] 返回表示所需节贡献的 [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumSectionContribs::get_Count](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-count.md)
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
