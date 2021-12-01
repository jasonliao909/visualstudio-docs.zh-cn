---
description: 从帧指针寄存器中检索堆栈填充的偏移量。
title: IDiaSymbol::get_framePadOffset | Microsoft Docs
ms.date: 04/27/2021
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_framePadOffset method
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 2bccd0087c22072efd016fe43646cceb75cf8a18
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833088"
---
# <a name="idiasymbolget_framepadoffset"></a>IDiaSymbol::get_framePadOffset

从帧指针寄存器中检索堆栈填充的偏移量。

## <a name="syntax"></a>语法

```C++
HRESULT get_framePadOffset ( 
   DWORD* pPadOffset
);
```

#### <a name="parameters"></a>参数

 `pPadOffset`

[out] 返回堆栈填充的偏移量。

## <a name="return-value"></a>返回值

 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注

从 Visual Studio 2019 版本 16.10 预览版 2 开始支持此方法。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
