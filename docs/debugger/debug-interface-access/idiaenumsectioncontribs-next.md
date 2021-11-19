---
description: 检索枚举序列中指定数量的节贡献。
title: IDiaEnumSectionContribs::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Next method
ms.assetid: a6bb2adb-ee6d-4f3c-ab5b-e89361c8880e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: d6377b8ee02a48878228e89ad277e4bc78b969c0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832227"
---
# <a name="idiaenumsectioncontribsnext"></a>IDiaEnumSectionContribs::Next
检索枚举序列中指定数量的节贡献。

## <a name="syntax"></a>语法

```C++
HRESULT Next( 
   ULONG                celt,
   IDiaSectionContrib** rgelt,
   ULONG*               pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

[in] 枚举器中要检索的节贡献数。

 rgelt

[out] 要用表示所需节贡献的 [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md) 对象填充的数组。

 pceltFetched

[out] 返回提取的枚举器中的节贡献数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多节贡献，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
