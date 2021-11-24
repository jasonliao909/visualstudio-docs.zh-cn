---
description: 检索符号的词法父标识符。
title: IDiaSymbol::get_lexicalParentId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_lexicalParentId method
ms.assetid: 6c0c2874-cc47-4e4f-ad9c-02a18a108d9d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: fde19f77fe924fbbc8cb7ba7e6ae096ba0805151
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832749"
---
# <a name="idiasymbolget_lexicalparentid"></a>IDiaSymbol::get_lexicalParentId
检索符号的词法父标识符。

## <a name="syntax"></a>语法

```C++
HRESULT get_lexicalParentId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回符号的词法父级 ID。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 标识符是由 DIA SDK 创建的唯一值，用于将所有符号标记为唯一。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
