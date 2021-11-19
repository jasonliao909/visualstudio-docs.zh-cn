---
description: 检索在调用当前函数之前用于计算寄存器集的程序字符串。
title: IDiaFrameData::get_program | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_program method
ms.assetid: 9201409e-b4b1-4e2e-a9f8-d17678ac538b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: e78315ba7fe4f4de3ae94cafe6d8ffa78ef32065
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832108"
---
# <a name="idiaframedataget_program"></a>IDiaFrameData::get_program
检索在调用当前函数之前用于计算寄存器集的程序字符串。

## <a name="syntax"></a>语法

```C++
HRESULT get_program ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回程序字符串。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果 `S_FALSE` 不支持此属性，则返回 。 否则，返回错误代码。

## <a name="remarks"></a>备注
 程序字符串是一系列宏，为了建立序言而进行解释。 例如，典型的堆栈帧可能使用程序字符串 `"$T0 $ebp = $eip $T0 4 + ^ = $ebp $T0 ^ = $esp $T0 8 + ="` 。 格式为反向波兰表示法，其中运算符遵循操作数。 `T0` 表示堆栈上的临时变量。 此示例执行以下步骤：

1. 将寄存器的内容移动到 `ebp` `T0` 。

2. 将 添加到 中的 值以生成地址、从该地址获取值，以及将 `4` `T0` 值存储在寄存器 中 `eip` 。

3. 从中存储的地址获取值， `T0` 将该值存储在寄存器 中 `ebp` 。

4. 将 `8` 添加到 中的值 `T0` ，将该值存储在寄存器 中 `esp` 。

   请注意，程序字符串特定于 CPU 和为当前堆栈帧表示的函数设置的调用约定。

## <a name="see-also"></a>另请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
