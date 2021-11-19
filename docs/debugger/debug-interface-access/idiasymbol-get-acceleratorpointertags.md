---
description: 返回与快捷键存根函数C++ AMP指针标记值。
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
返回与快捷键存根函数C++ AMP指针标记值。

## <a name="syntax"></a>语法

```C++
HRESULT get_acceleratorPointerTags(
   DWORD          cnt,
   DWORD*         pcnt,
   DWORD*         pPointerTags);
```

#### <a name="parameters"></a>参数
 `cnt`

[in]输出数组 的大小 `pPointerTags` 。

 `pcnt`

[out]快捷键存根函数中C++ AMP标记的计数。

 `pPointerTags`

[out]使用 `DWORD` 快捷键存根函数中的快捷键指针标记值填充的C++ AMP指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回 `S_FALSE` 或错误代码。

## <a name="remarks"></a>备注
 此方法在一个接口 `IDiaSymbol` 上调用，该接口对应于C++ AMP存根函数。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
