---
description: 检索一个标记，该标记指定编译单位是否包含调试信息。
title: IDiaSymbol::get_hasDebugInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasDebugInfo method
ms.assetid: 84cd2b67-0d83-4589-9ecb-a4bcbeed55f5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: e1a395963637974abfa126a310fed0ba3d0dc09e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832501"
---
# <a name="idiasymbolget_hasdebuginfo"></a>IDiaSymbol::get_hasDebugInfo
检索一个标记，该标记指定[编译单位](../../debugger/debug-interface-access/compiland.md)是否包含调试信息。

## <a name="syntax"></a>语法

```C++
HRESULT get_hasDebugInfo(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out] 如果编译单位包含调试信息，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
