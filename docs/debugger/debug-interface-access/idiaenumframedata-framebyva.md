---
description: 按虚拟地址 (VA) 返回帧。
title: IDiaEnumFrameData::frameByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::frameByVA method
ms.assetid: 0b1e441b-710a-46d8-8060-bed39071c834
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: c713ea86baad9529b9dbca4ee2e07f2dd5d2b7e3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832285"
---
# <a name="idiaenumframedataframebyva"></a>IDiaEnumFrameData::frameByVA
按虚拟地址 (VA) 返回帧。

## <a name="syntax"></a>语法

```C++
HRESULT frameByVA( 
   ULONGLONG       virtualAddress,
   IDiaFrameData** frame
);
```

#### <a name="parameters"></a>参数
 virtualAddress

[in] 感兴趣的帧的 VA。

 框架

[out] 返回表示包含所提供地址的帧的 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有帧数据与指定地址匹配，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
