---
description: 检索贡献地址的节部分。
title: IDiaSectionContrib::get_addressSection | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_addressSection method
ms.assetid: 13fe7e0b-c978-4a1d-bb57-64c8583b5e14
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: d549d9ef101cb5b94f19c70e1b5a0c9f1860e964
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831995"
---
# <a name="idiasectioncontribget_addresssection"></a>IDiaSectionContrib::get_addressSection
检索贡献地址的节部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_addressSection ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 检索贡献地址的节部分。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
