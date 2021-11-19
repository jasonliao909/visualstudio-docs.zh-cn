---
description: 检索一个标记，该标记指示符号是否与为 C++ AMP Accelerator 编译的代码中的组共享本地变量相对应。
title: IDiaSymbol::get_isAcceleratorGroupSharedLocal | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 17a20542-5b45-478f-bb80-0d56031aadb5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: bc8da59465ce2aa20c37bf03c9b9fbcd4186c7c7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832458"
---
# <a name="idiasymbolget_isacceleratorgroupsharedlocal"></a>IDiaSymbol::get_isAcceleratorGroupSharedLocal
检索一个标记，该标记指示符号是否与为 C++ AMP Accelerator 编译的代码中的组共享本地变量相对应。

## <a name="syntax"></a>语法

```C++
HRESULT get_isAcceleratorGroupSharedLocal(
   BOOL* pFlag);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out] 指向 `BOOL` 的指针，该指针指示符号是否与为 C++ AMP Accelerator 编译的代码中的组共享本地变量相对应。 如果是 `TRUE`，则可以使用 `get_baseDataSlot` 和 `get_baseDataOffset` 方法获取变量的存储位置信息。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_baseDataSlot](../../debugger/debug-interface-access/idiasymbol-get-basedataslot.md)
- [IDiaSymbol::get_baseDataOffset](../../debugger/debug-interface-access/idiasymbol-get-basedataoffset.md)
