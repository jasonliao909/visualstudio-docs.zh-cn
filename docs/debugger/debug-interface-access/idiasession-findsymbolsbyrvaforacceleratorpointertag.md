---
description: 给定相应的标记值后，此方法将在指定的相对虚拟地址返回指定父级 Accelerator 存根函数中包含的符号的枚举。
title: IDiaSession::findSymbolsByRVAForAcceleratorPointerTag | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: a073cc45-0c7b-417e-b5fc-a3b08beccdbc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 74c6990599fdf75e05b9f009f20a5ea4a6e201a9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831874"
---
# <a name="idiasessionfindsymbolsbyrvaforacceleratorpointertag"></a>IDiaSession::findSymbolsByRVAForAcceleratorPointerTag
给定相应的标记值后，此方法将在指定的相对虚拟地址返回指定父级 Accelerator 存根函数中包含的符号的枚举。

## <a name="syntax"></a>语法

```C++
HRESULT findSymbolsByRVAForAcceleratorPointerTag ( 
   IDiaSymbol*           parent,
   DWORD                 tagValue,
   DWORD                 rva,
   IDiaEnumSymbols**     ppResult
);
```

#### <a name="parameters"></a>参数
 `parent`

[in] 对应于要搜索的 Accelerator 存根函数的 `IDiaSymbol`。

 `tagValue`

[in] 指针标记值。

 `rva`

[in] 相对虚拟地址。

 `ppResult`

[out] 指向使用结果初始化的 `IDiaEnumSymbols` 接口指针的指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="remarks"></a>备注
 仅在对应于 Accelerator 存根函数的 `IDiaSymbol` 接口上调用此方法。

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
