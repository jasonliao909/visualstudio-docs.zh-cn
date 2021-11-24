---
description: 检索帧类型。
title: IDiaStackFrame::get_type | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_type method
ms.assetid: 99daa97b-5c05-455d-bd1e-800762ccf7c9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: b40e449f784a065d20126916694da01c238680f0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832447"
---
# <a name="idiastackframeget_type"></a>IDiaStackFrame::get_type
检索帧类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_type ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 从 [StackFrameTypeEnum Enumeration](../../debugger/debug-interface-access/stackframetypeenum.md) 枚举返回一个值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
- [StackFrameTypeEnum 枚举](../../debugger/debug-interface-access/stackframetypeenum.md)
