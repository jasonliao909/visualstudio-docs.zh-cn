---
description: 在已打开候选 .pdb 文件时调用。
title: IDiaLoadCallback::NotifyOpenPDB | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::NotifyOpenPDB method
ms.assetid: c0547f99-8468-4e57-82ca-9ef7d6707c8a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 0a3642fa6a3082c03c8b582895d7f423fdc10573
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832041"
---
# <a name="idialoadcallbacknotifyopenpdb"></a>IDiaLoadCallback::NotifyOpenPDB
在已打开候选 .pdb 文件时调用。

## <a name="syntax"></a>语法

```C++
HRESULT NotifyOpenPDB ( 
   LPCOLESTR pdbPath,
   HRESULT   resultCode
);
```

#### <a name="parameters"></a>参数
 `pdbPath`

[in] .pdb 文件的完整路径。

 `resultCode`

[in] 指示应用到此文件的加载是成功 (`S_OK`) 还是失败的代码。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。 通常会忽略返回代码。

## <a name="see-also"></a>另请参阅
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
