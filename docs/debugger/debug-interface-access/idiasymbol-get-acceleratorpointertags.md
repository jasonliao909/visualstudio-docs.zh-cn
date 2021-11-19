---
description: 返回对应于 C++ AMP 加速器存根函数的所有加速器指针标记值。
title: IDiaSymbol::get_acceleratorPointerTags | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 30e13cee-e511-49ec-affd-99b0097071b2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 3bd2de4fe6599ec9dfc7d732a83dd4f88e04fabb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831810"
---
# <a name="idiasymbolget_acceleratorpointertags"></a>IDiaSymbol::get_acceleratorPointerTags
返回对应于 C++ AMP 加速器存根函数的所有加速器指针标记值。

## <a name="syntax"></a>语法

```C++
HRESULT get_acceleratorPointerTags(
   DWORD          cnt,
   DWORD*         pcnt,
   DWORD*         pPointerTags);
```

#### <a name="parameters"></a>参数
 `cnt`

[in] 输出数组 `pPointerTags` 的大小。

 `pcnt`

[out] C++ AMP 加速器存根函数中加速器指针标记的计数。

 `pPointerTags`

[out] 填充了 C++ AMP 加速器存根函数中加速器指针标记值的 `DWORD` 数组指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

## <a name="remarks"></a>备注
 此方法是在对应于 C++ AMP 快捷键存根函数的 `IDiaSymbol` 接口上调用的。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
