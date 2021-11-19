---
description: 此方法检索指定局部变量的值作为原始字节。
title: IDiaStackFrame::get_rawLVarInstanceValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_rawLVarInstanceValue method
ms.assetid: ce526259-85a6-475b-9274-0b3a21d95db2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 065e15ccbaa714a46eb388c2550e6e1db45558f2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831819"
---
# <a name="idiastackframeget_rawlvarinstancevalue"></a>IDiaStackFrame::get_rawLVarInstanceValue
此方法检索指定局部变量的值作为原始字节。

## <a name="syntax"></a>语法

```C++
HRESULT get_rawLVarInstanceValue(
   IDiaLVarInstance* pInstance,
   DWORD             cbDataMax,
   DWORD*            pcbData,
   BYTE*             pbData
);
```

#### <a name="parameters"></a>参数
 `pInstance`

中一个 `IDiaLVarInstance` 对象，该对象表示要获取其值的局部变量的实例。

 `cbDataMax`

中所指向的缓冲区中的最大字节数 `pbData` 。 最大 () ，最多可为8个字节 `sizeof(ULONGLONG)` 。

 `pcbData`

弄返回缓冲区中存储的实际字节数。

 `pbData`

弄要用数据填充的缓冲区。 该类型不能为 `NULL`。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
