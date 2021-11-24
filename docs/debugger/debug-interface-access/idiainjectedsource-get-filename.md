---
description: 检索源的文件名。
title: IDiaInjectedSource::get_filename | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_filename method
ms.assetid: 20f4fc68-335a-4971-b3a6-76501f0e8b19
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 66ad7581bb65e6601f831a55a8aeee77a0f42aa4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832087"
---
# <a name="idiainjectedsourceget_filename"></a>IDiaInjectedSource::get_filename
检索源的文件名。

## <a name="syntax"></a>语法

```C++
HRESULT get_filename ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>参数
 pRetVal

[out] 返回源的文件名。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
