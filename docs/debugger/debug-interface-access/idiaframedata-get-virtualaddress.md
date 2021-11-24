---
description: 检索帧代码的虚拟地址 (VA)。
title: IDiaFrameData::get_virtualAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_virtualAddress method
ms.assetid: de137bee-132f-4aae-a067-9578b7a3e6d4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 003975e7eaf17783fc036da15c4653cf48d7c7ce
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832102"
---
# <a name="idiaframedataget_virtualaddress"></a>IDiaFrameData::get_virtualAddress
检索帧代码的虚拟地址 (VA)。

## <a name="syntax"></a>语法

```C++
HRESULT get_virtualAddress ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回帧代码的虚拟地址。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
