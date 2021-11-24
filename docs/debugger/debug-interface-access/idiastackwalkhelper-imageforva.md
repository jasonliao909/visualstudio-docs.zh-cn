---
description: 如果可执行文件内存空间中的某个位置有一个虚拟地址，则返回该可执行文件的图像在内存中的起始位置。
title: IDiaStackWalkHelper::imageForVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper::imageForVA method
ms.assetid: 8d4edabf-3c01-4fef-8b61-4779f3371067
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 8ad55d62007c139f1a14e6c93b34797110b47557
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831773"
---
# <a name="idiastackwalkhelperimageforva"></a>IDiaStackWalkHelper::imageForVA
如果可执行文件内存空间中的某个位置有一个虚拟地址，则返回该可执行文件的图像在内存中的起始位置。

## <a name="syntax"></a>语法

```C++
HRESULT imageForVA(
   ULONGLONG  vaContext,
   ULONGLONG *pvaImageStart
);
```

#### <a name="parameters"></a>参数
 `vaContext`

[in] 位于可执行文件空间中某个位置的虚拟地址。

 `pvaImageStart`

[out] 返回可执行文件的图像的起始虚拟地址。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
