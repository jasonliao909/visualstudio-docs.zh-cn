---
description: 给定相应的标记值后，此方法将在指定的相对虚拟地址返回此存根函数中包含的符号的枚举。
title: IDiaSymbol::findSymbolsByRVAForAcceleratorPointerTag | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 024ccd78-5867-4ca7-bc26-548758e9ac53
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 3d1c469d99149bdd21435d7e5b99dd1c193f4659
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831740"
---
# <a name="idiasymbolfindsymbolsbyrvaforacceleratorpointertag"></a>IDiaSymbol::findSymbolsByRVAForAcceleratorPointerTag
给定相应的标记值后，此方法将在指定的相对虚拟地址返回此存根函数中包含的符号的枚举。

## <a name="syntax"></a>语法

```C++
HRESULT findSymbolsByRVAForAcceleratorPointerTag (
   DWORD             tagValue,
   DWORD             rva,
   IDiaEnumSymbols** ppResult);
```

#### <a name="parameters"></a>参数
 `tagValue`

[in] 找到了指针符号记录的指针标记值。

 `rva`

[in] 用于过滤与具有指定标记值的指针变量对应的符号的 rva。

 `ppResult`

[out] 指向已使用结果进行初始化的 `IDiaEnumSymbols` 接口指针的一个指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

## <a name="remarks"></a>备注
 仅在对应于 Accelerator 存根函数的 `IDiaSymbol` 接口上调用此方法。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
