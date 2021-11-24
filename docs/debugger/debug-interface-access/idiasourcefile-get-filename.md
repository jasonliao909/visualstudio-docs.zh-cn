---
description: 检索源文件名。
title: IDiaSourceFile::get_fileName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_fileName method
ms.assetid: a5cb8927-23c6-469e-8f78-f2787d85dba4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 5f9bb3ba8834c58fc7f4317afef689b34f48075a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831843"
---
# <a name="idiasourcefileget_filename"></a>IDiaSourceFile::get_fileName
检索源文件名。

## <a name="syntax"></a>语法

```C++
HRESULT get_fileName ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回源文件名。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
