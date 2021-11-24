---
description: 检索此方法的逻辑 this 调整器。
title: IDiaSymbol::get_thisAdjust | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_thisAdjust method
ms.assetid: 56b9a147-e8c0-4d4b-a42a-398214dd5f86
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 7b4f166f936bef12c183eb7064d10f1c1d6217e1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831710"
---
# <a name="idiasymbolget_thisadjust"></a>IDiaSymbol::get_thisAdjust
检索此方法的逻辑 `this` 调整器。

## <a name="syntax"></a>语法

```C++
HRESULT get_thisAdjust ( 
   LONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回此方法的逻辑 `this` 调整器。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 在某些多重继承情况下，方法本身必须通过将偏移量添加到 `this` 来计算真正的 `this` 值。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
