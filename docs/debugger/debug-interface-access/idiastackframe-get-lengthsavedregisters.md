---
description: IDiaStackFrame::get_lengthSavedRegisters 检索在堆栈上推送的已保存寄存器的字节数。
title: IDiaStackFrame::get_lengthSavedRegisters | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_lengthSavedRegisters method
ms.assetid: b75fad6e-1ef4-44e6-89e3-c31c6fba10b3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 1a4c033d9df9f06df318d6156c73b3aee2d828ed
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831828"
---
# <a name="idiastackframeget_lengthsavedregisters"></a>IDiaStackFrame::get_lengthSavedRegisters
检索在堆栈上推送的已保存寄存器的字节数。

## <a name="syntax"></a>语法

```C++
HRESULT get_lengthSavedRegisters ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回已保存寄存器的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
