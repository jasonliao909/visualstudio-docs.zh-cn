---
description: IDiaStackFrame::get_lengthParams 检索在堆栈上推送的参数的字节数。
title: IDiaStackFrame::get_lengthParams | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_lengthParams method
ms.assetid: 78005efa-2883-4823-b4e4-711a66672c78
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 36aca2df154f70902f65fa4bee9546d14f4bad94
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831831"
---
# <a name="idiastackframeget_lengthparams"></a>IDiaStackFrame::get_lengthParams
检索在堆栈上推送的参数的字节数。

## <a name="syntax"></a>语法

```C++
HRESULT get_lengthParams ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回参数的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
