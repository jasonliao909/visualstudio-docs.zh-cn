---
description: 检索托管函数或变量的元数据标记。
title: IDiaSymbol::get_token | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_token method
ms.assetid: 7ee7a9be-a0d8-48e4-9fef-d37b3d6ae4ef
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: d2aff8f344dd9ba7dbc94a29cad29b9e2ce58aeb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832653"
---
# <a name="idiasymbolget_token"></a>IDiaSymbol::get_token
检索托管函数或变量的元数据标记。

## <a name="syntax"></a>语法

```C++
HRESULT get_token ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回托管函数或变量的元数据标记。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
