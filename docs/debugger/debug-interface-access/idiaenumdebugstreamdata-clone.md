---
description: 创建一个枚举器，其中包含与当前调试数据流枚举器相同的枚举序列。
title: IDiaEnumDebugStreamData::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreamData::Clone method
ms.assetid: e7f17750-0694-4634-bf34-c821cd265c2f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 965fb81fec0964b5e682c21e03c67410b148eae0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832322"
---
# <a name="idiaenumdebugstreamdataclone"></a>IDiaEnumDebugStreamData::Clone
创建一个枚举器，其中包含与当前枚举器相同的枚举序列。

## <a name="syntax"></a>语法

```C++
HRESULT Clone ( 
   IDiaEnumDebugStreamData** ppenum
);
```

#### <a name="parameters"></a>参数
 ppenum

[out] 返回包含调试数据流记录的重复序列的 [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
