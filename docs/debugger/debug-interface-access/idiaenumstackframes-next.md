---
description: 检索枚举序列中指定数目的堆栈帧元素。
title: IDiaEnumStackFrames::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumStackFrames::Next method
ms.assetid: 09378a21-d5e3-4213-b7e2-10f04d85295f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 76248ef1feb330157895ccd24d8fa071b3e857bd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832187"
---
# <a name="idiaenumstackframesnext"></a>IDiaEnumStackFrames::Next
检索枚举序列中指定数目的堆栈帧元素。

## <a name="syntax"></a>语法

```C++
HRESULT Next( 
   ULONG             celt,
   IDiaStackFrame**  rgelt,
   ULONG*            pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

[in] 要检索的枚举器中的堆栈帧元素的数目。

 rgelt

[out] 要用请求的 [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md) 对象填充的数组。

 pceltFetched

[out] 返回提取的枚举器中的堆栈帧元素的数量。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多堆栈帧，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumStackFrames](../../debugger/debug-interface-access/idiaenumstackframes.md)
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
