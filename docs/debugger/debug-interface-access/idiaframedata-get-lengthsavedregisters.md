---
description: IDiaFrameData：： get_lengthSavedRegisters 检索推送到堆栈上的已保存寄存器的字节数。
title: IDiaFrameData::get_lengthSavedRegisters | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_lengthSavedRegisters method
ms.assetid: dfda4e91-9bfa-4b9d-9133-b73015bfa4d5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: fc5f3ef7a27ef367c1f48bb17bf346322eff6434
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832114"
---
# <a name="idiaframedataget_lengthsavedregisters"></a>IDiaFrameData::get_lengthSavedRegisters
检索推送到堆栈上的已保存寄存器的字节数。

## <a name="syntax"></a>语法

```C++
HRESULT get_lengthSavedRegisters ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回已保存寄存器的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 `S_FALSE`如果此属性不受支持，则返回。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的值通常用在程序字符串的解释中 (有关程序字符串的定义，请参阅 [IDiaFrameData：： get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md) 方法) 。

## <a name="see-also"></a>另请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)
