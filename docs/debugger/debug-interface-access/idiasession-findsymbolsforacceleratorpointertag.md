---
description: 返回指定的标记值在父级 Accelerator 存根函数中对应的变量的符号枚举。
title: IDiaSession::findSymbolsForAcceleratorPointerTag | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 95fd5e7a-c637-437e-b369-c864eef733c2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: e508ef56dd6b3a52e8c65431a263d3bda9a47caf
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831872"
---
# <a name="idiasessionfindsymbolsforacceleratorpointertag"></a>IDiaSession::findSymbolsForAcceleratorPointerTag
返回指定的标记值在父级 Accelerator 存根函数中对应的变量的符号枚举。

## <a name="syntax"></a>语法

```C++
HRESULT findSymbolsForAcceleratorPointerTag ( 
   IDiaSymbol*           parent,
   DWORD                 tagValue,
   IDiaEnumSymbols**     ppResult
);
```

#### <a name="parameters"></a>参数
 `parent`

[in] 对应于要搜索的 Accelerator 存根函数的 IDiaSymbol。

 `tagValue`

[in] 指针标记值。

 `ppResult`

[out] 指向使用结果初始化的 `IDiaEnumSymbols` 接口指针的指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
