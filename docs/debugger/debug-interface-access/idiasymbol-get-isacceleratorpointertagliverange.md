---
description: 检索一个标记，该标记指示在为 C++ AMP 加速器编译的代码中，该符号是否与指针变量的标记组件的定义范围符号相对应。
title: IDiaSymbol::get_isAcceleratorPointerTagLiveRange | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: d195aec4-6d3c-42e0-88a5-3d463539f0b8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: b65e31e2e6d86711b576023ff0f70877e29cdd03
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832668"
---
# <a name="idiasymbolget_isacceleratorpointertagliverange"></a>IDiaSymbol::get_isAcceleratorPointerTagLiveRange
检索一个标记，该标记指示在为 C++ AMP 加速器编译的代码中，该符号是否与指针变量的标记组件的定义范围符号相对应。 定义范围符号是某个地址范围的变量位置。

## <a name="syntax"></a>语法

```C++
HRESULT get_isAcceleratorPointerTagLiveRange(
   BOOL* pFlag);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out] 指向 `BOOL` 的指针，该指针指示符号是否与定义范围符号相对应。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
