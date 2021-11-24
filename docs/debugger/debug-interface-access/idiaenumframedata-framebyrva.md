---
description: 按相对虚拟地址 (RVA) 返回帧。
title: IDiaEnumFrameData::frameByRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::frameByRVA method
ms.assetid: 4b8dec05-e76c-4cc4-9644-2369d583849f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 220042316d0e7e89f14d6fc86637fa1122c9f9e1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832284"
---
# <a name="idiaenumframedataframebyrva"></a>IDiaEnumFrameData::frameByRVA
按相对虚拟地址 (RVA) 返回帧。

## <a name="syntax"></a>语法

```C++
HRESULT frameByRVA( 
   DWORD           relativeVirtualAddress,
   IDiaFrameData** frame
);
```

#### <a name="parameters"></a>参数
 relativeVirtualAddress

[in] 感兴趣帧的 RVA。

 框架

[out] 返回一个 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) 对象，该对象表示包含所提供地址的帧。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有帧数据与指定地址匹配，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
