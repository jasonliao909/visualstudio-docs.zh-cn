---
description: 此方法以原始字节的形式检索指定局部变量的值。
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
此方法以原始字节的形式检索指定局部变量的值。

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

[in] 一个 `IDiaLVarInstance` 对象，表示要获取其值的局部变量的实例。

 `cbDataMax`

[in] `pbData` 指向的缓冲区中的最大字节数。 其最大长度可达 8 字节 (`sizeof(ULONGLONG)`)。

 `pcbData`

[out] 返回存储在缓冲区中的实际字节数。

 `pbData`

[out] 要用数据填充的缓冲区。 该类型不能为 `NULL`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
