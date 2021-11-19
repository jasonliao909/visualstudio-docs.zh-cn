---
description: 设置可执行文件的加载地址，该地址与此符号存储区中的符号对应。
title: IDiaSession::put_loadAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::put_loadAddress method
ms.assetid: b157b245-1ea0-4b80-8962-d8b278dbc742
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 692ab9f7a1d792de504478349bd1fe58908485a5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831858"
---
# <a name="idiasessionput_loadaddress"></a>IDiaSession::put_loadAddress
设置可执行文件的加载地址，该地址与此符号存储区中的符号对应。

## <a name="syntax"></a>语法

```C++
HRESULT put_loadAddress ( 
   ULONGLONG NewVal
);
```

#### <a name="parameters"></a>参数
 `NewVal`

[in] 可执行文件的加载地址。

## <a name="remarks"></a>备注
 符号虚拟地址 (VA) 属性使用此方法的值进行计算。 除非此属性设置为非零，否则不会计算虚拟地址。

> [!NOTE]
> 在获取 [IDiaSession](../../debugger/debug-interface-access/idiasession.md) 对象之后、开始使用该对象之前，如果需要使用符号的任何虚拟属性，则必须调用此方法。

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
