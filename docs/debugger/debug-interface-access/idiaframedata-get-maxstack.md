---
description: IDiaFrameData::get_maxStack 检索在帧中的堆栈上推送的最大字节数。
title: IDiaFrameData::get_maxStack | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_maxStack method
ms.assetid: 2585e13c-c0f3-49fe-9a84-08adb0dbeaa4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: f0af1f96f3f9ee468c18b89a1fd15f291ce2de0c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832110"
---
# <a name="idiaframedataget_maxstack"></a>IDiaFrameData::get_maxStack
检索在帧中的堆栈上推送的最大字节数。

## <a name="syntax"></a>语法

```C++
HRESULT get_maxStack ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回在堆栈上推送的最大字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的值通常用于解释程序字符串（有关程序字符串的定义，请参阅 [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md) 方法）。

## <a name="see-also"></a>另请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)
