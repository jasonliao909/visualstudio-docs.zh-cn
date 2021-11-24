---
description: 检索为其编译编译单位的平台类型。
title: IDiaSymbol::get_platform | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_platform method
ms.assetid: dff1c1eb-bcb2-4275-bb07-f2fdc076d6fb
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 3c05237056b826ec47978f01e5f2258ae19b157b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832440"
---
# <a name="idiasymbolget_platform"></a>IDiaSymbol::get_platform
检索为其编译编译单位的平台类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_platform ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 从指定为其编译编译单位的平台类型的 [CV_CPU_TYPE_e Enumeration](../../debugger/debug-interface-access/cv-cpu-type-e.md) 枚举中返回值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [CV_CPU_TYPE_e 枚举](../../debugger/debug-interface-access/cv-cpu-type-e.md)
