---
description: 创建一个枚举器，其中包含与当前调试流枚举器相同的枚举状态。
title: IDiaEnumDebugStreams::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreams::Clone method
ms.assetid: e85ec592-de97-4f95-a774-1623315ba415
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: d9bef5efe587915d43c1b3399fbbc534f53e4613
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832300"
---
# <a name="idiaenumdebugstreamsclone"></a>IDiaEnumDebugStreams::Clone
创建一个枚举器，其中包含与当前枚举器相同的枚举状态。

## <a name="syntax"></a>语法

```C++
HRESULT Clone ( 
   IDiaEnumDebugStreams** ppenum
);
```

#### <a name="parameters"></a>参数
 `ppenum`

[out] 返回包含枚举器副本的 [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md) 对象。 不会复制流，只会复制枚举器。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)
