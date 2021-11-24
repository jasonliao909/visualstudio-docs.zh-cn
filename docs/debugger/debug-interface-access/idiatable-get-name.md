---
description: 检索表的名称。
title: IDiaTable::get_name | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable::get_name method
ms.assetid: f6e9cd07-63cd-48a6-9835-e69c2d0859c5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: a54db09dced33aed000466be5cb6f75c13ca7f4c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832739"
---
# <a name="idiatableget_name"></a>IDiaTable::get_name
检索表的名称。

## <a name="syntax"></a>语法

```C++
HRESULT get_name ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回表的名称。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
