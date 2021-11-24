---
description: 指定 this 指针是否指向具有多个继承的数据成员。
title: IDiaSymbol::get_isMultipleInheritance | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 0aa356a1-5c5c-4ee4-8b48-bae0a2610013
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: b64d22dea62ceaf20162c3e4734bc057b54213d1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832484"
---
# <a name="idiasymbolget_ismultipleinheritance"></a>IDiaSymbol::get_isMultipleInheritance
指定 `this` 指针是否指向具有多个继承的数据成员。

## <a name="syntax"></a>语法

```C++
HRESULT get_isMultipleInheritance(
   BOOL* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 一个指向 `BOOL` 的指针，指定 `this` 指针是否指向具有多个继承的数据成员。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
