---
description: 检索一个标志，该标志指示该节是否可以作为代码执行。
title: IDiaSectionContrib::get_execute | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_execute method
ms.assetid: 66eb38ce-a5e1-467e-b845-b3dc433eda91
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 711e1a3618419f554955e458fa1f9603dea8c7de
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831977"
---
# <a name="idiasectioncontribget_execute"></a>IDiaSectionContrib::get_execute
检索一个标志，该标志指示该节是否可以作为代码执行。

## <a name="syntax"></a>语法

```C++
HRESULT get_excute ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 如果该节可以作为代码执行，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
