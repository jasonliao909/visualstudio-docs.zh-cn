---
description: 在给定相应标记值的情况下，此方法返回包含在此存根函数中的符号的枚举。
title: IDiaSymbol::findSymbolsForAcceleratorPointerTag | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: fb66852c-c5f7-4140-b9fe-20cb4e51a9fe
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: b5ccf90584cfc948fc4ecb886dd20ada5cbf6036
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831736"
---
# <a name="idiasymbolfindsymbolsforacceleratorpointertag"></a>IDiaSymbol::findSymbolsForAcceleratorPointerTag

在给定相应标记值的情况下，此方法返回包含在此存根函数中的符号的枚举。

## <a name="syntax"></a>语法

```C++
HRESULT findSymbolsForAccleratorPointerTag (
   DWORD             tagValue,
   IDiaEnumSymbols** ppResult);
```

#### <a name="parameters"></a>参数
 `tagValue`

[in] 找到了指针符号记录的指针标记值。

 `ppResult`

[out] 指向已使用结果进行初始化的 `IDiaEnumSymbols` 接口指针的指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
