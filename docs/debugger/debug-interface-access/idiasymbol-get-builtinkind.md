---
description: 检索一种内置的 HLSL 类型。
title: IDiaSymbol::get_builtInKind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 953e6dba-582e-4b76-b736-898b92e5693e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 3208091cc7822bce8bcce82c404977283692ec3b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832634"
---
# <a name="idiasymbolget_builtinkind"></a>IDiaSymbol::get_builtInKind
检索一种内置的 HLSL 类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_buildInKind(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 指向保留一种内置的 HLSL 类型的 `DWORD` 的指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
