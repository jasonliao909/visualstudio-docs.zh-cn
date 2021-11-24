---
description: 检索一个标记，该标记指示节是否包含注释或类似的信息。
title: IDiaSectionContrib::get_informational | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_informational method
ms.assetid: 5351e89f-7db1-4f8e-9e57-2dd1c74002e0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: b05ab78bdaaac3c53da1ce08bbeef6bbae2c4b8e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831979"
---
# <a name="idiasectioncontribget_informational"></a>IDiaSectionContrib::get_informational
检索一个标记，该标记指示节是否包含注释或类似的信息。

## <a name="syntax"></a>语法

```C++
HRESULT get_informational(
   BOOL* pRetVal
};
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 如果节包含注释或其他信息，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 通常，.directive 节包含信息。

## <a name="see-also"></a>另请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
