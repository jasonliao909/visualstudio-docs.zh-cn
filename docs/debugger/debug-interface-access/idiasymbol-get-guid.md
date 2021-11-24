---
description: 检索符号的全局唯一标识符 (GUID)。
title: IDiaSymbol::get_guid | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_guid method
ms.assetid: c02a6c92-f406-4646-82e7-3cd005af900e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: c06ed62ad6820ea44bd1259edcac738020361129
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832670"
---
# <a name="idiasymbolget_guid"></a>IDiaSymbol::get_guid
检索符号的全局唯一标识符 (GUID)。

## <a name="syntax"></a>语法

```C++
HRESULT get_guid ( 
   GUID* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回符号的 GUID。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
