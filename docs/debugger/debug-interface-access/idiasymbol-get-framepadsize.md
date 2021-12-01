---
description: 检索添加到每个函数的额外填充大小。
title: IDiaSymbol::get_framePadSize | Microsoft Docs
ms.date: 04/27/2021
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_framePadSize method
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 052aa705c645ee7dc991f5311aa9d96f3b6a637d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833087"
---
# <a name="idiasymbolget_framepadsize"></a>IDiaSymbol::get_framePadSize

检索添加到每个函数的额外填充大小。

## <a name="syntax"></a>语法

```C++
HRESULT get_framePadSize ( 
   DWORD* pPadSize
);
```

#### <a name="parameters"></a>参数

 `pPadSize`

[out] 返回添加到每个函数的额外填充大小。

## <a name="return-value"></a>返回值

 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注

“编辑并继续”通常使用额外的填充大小。

从 Visual Studio 2019 版本 16.10 预览版 2 开始支持此方法。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
