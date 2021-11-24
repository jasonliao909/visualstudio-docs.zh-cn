---
description: 检索帧的代码地址的节部分。
title: IDiaFrameData::get_addressSection | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_addressSection method
ms.assetid: e4eedede-4a1c-4da2-a812-b92df328fd8d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 57e8e8776535fd63bce604b300caf8340c8c5e70
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832130"
---
# <a name="idiaframedataget_addresssection"></a>IDiaFrameData::get_addressSection
检索帧的代码地址的节部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_addressSection ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回帧的代码地址的节部分。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
