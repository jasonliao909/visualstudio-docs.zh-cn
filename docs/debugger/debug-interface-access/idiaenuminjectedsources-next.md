---
description: 检索枚举序列中指定数量的注入源代码。
title: IDiaEnumInjectedSources::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumInjectedSources::Next method
ms.assetid: 38af80fc-748f-4b15-bff1-823db21dd4d0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: a764df156aa661501d442d163a0f2f1a46dec22b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832261"
---
# <a name="idiaenuminjectedsourcesnext"></a>IDiaEnumInjectedSources::Next
检索枚举序列中指定数量的注入源代码。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
   ULONG                celt,
   IDiaInjectedSource** rgelt,
   ULONG*               pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

[in] 要检索的枚举器中注入源代码的数量。

 rgelt

[out] 返回表示所需注入源代码的 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md) 对象数组。

 pceltFetched

[out] 返回提取的枚举器中注入源代码的数量。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多注入源代码，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
