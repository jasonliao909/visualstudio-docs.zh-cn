---
description: 检索将源编译到的对象文件名。
title: IDiaInjectedSource::get_objectFilename | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_objectFilename method
ms.assetid: 7c42847a-f0df-443a-a9fe-c495c1271ea8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: cfe2dc595f541bfa7c68acbcf07cf98f84ffff55
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832089"
---
# <a name="idiainjectedsourceget_objectfilename"></a>IDiaInjectedSource::get_objectFilename
检索将源编译到的对象文件名。

## <a name="syntax"></a>语法

```C++
HRESULT get_objectFilename ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回将源编译到的对象文件名。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
