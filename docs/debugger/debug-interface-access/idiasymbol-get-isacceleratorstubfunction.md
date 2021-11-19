---
description: 指示符号是否对应于为对应于 parallel_for_each 调用的快捷键编译的着色器的顶级函数符号。
title: IDiaSymbol：： get_isAcceleratorStubFunction |Microsoft Docs
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
指示符号是否对应于为对应于调用的快捷键编译的着色器的顶级函数符号 `parallel_for_each` 。

## <a name="syntax"></a>语法

```C++
HRESULT get_isAcceleratorStubFunction(
   BOOL* pFlag);
```

#### <a name="parameters"></a>参数
 `pFlag`

弄指向 `BOOL` 的指针，该指针指示符号是否对应于为对应于调用的快捷键编译的着色器的顶级函数符号 `parallel_for_each` 。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
