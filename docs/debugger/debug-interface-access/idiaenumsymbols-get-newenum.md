---
description: 检索符号枚举器的 System.Runtime.InteropServices.ComTypes.IEnumVARIANT 版本。
title: IDiaEnumSymbols::get__NewEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbols::get__NewEnum method
ms.assetid: 879609ea-8e5a-4fa3-afa6-d24870fb4392
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 962771f9243a53ca7ca1f92441439663c0f9d710
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832179"
---
# <a name="idiaenumsymbolsget__newenum"></a>IDiaEnumSymbols::get__NewEnum
检索该枚举器的 <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> 版本。

## <a name="syntax"></a>语法

```C++
HRESULT get__NewEnum ( 
   IUnknown** pRetVal
);
```

#### <a name="parameters"></a>参数
 pRetVal

[out] 返回表示该枚举器 <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> 版本的 `IUnknown` 接口。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
