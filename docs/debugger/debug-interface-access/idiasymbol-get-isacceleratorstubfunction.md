---
description: 指示该符号是否对应于为与 parallel_for_each 调用对应的加速器编译的着色器的顶级函数符号。
title: IDiaSymbol::get_isAcceleratorStubFunction | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: cc4ea375-76f6-4ba8-baed-c5fa82108137
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: b652591ea55aa7b25a95c12b1813c67c252fd817
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832667"
---
# <a name="idiasymbolget_isacceleratorstubfunction"></a>IDiaSymbol::get_isAcceleratorStubFunction
指示该符号是否对应于为与 `parallel_for_each` 调用对应的加速器编译的着色器的顶级函数符号。

## <a name="syntax"></a>语法

```C++
HRESULT get_isAcceleratorStubFunction(
   BOOL* pFlag);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out] 指向 `BOOL` 的指针，指示该符号是否对应于为与 `parallel_for_each` 调用对应的加速器编译的着色器的顶级函数符号。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
