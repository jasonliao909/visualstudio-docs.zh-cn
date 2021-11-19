---
description: 执行堆栈展开并返回堆栈审核帧接口中的结果。
title: IDiaFrameData::execute | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::execute method
ms.assetid: 7a6c7d03-1ff1-4059-bd54-5f407eeebc26
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 6774cd500d4282acaebefe3e2dc1f2edee8f55ff
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832133"
---
# <a name="idiaframedataexecute"></a>IDiaFrameData::execute
执行堆栈展开并返回堆栈审核帧接口中的结果。

## <a name="syntax"></a>语法

```C++
HRESULT execute ( 
   IDiaStackWalkFrame* frame
);
```

#### <a name="parameters"></a>参数
 `frame`

中保存框架寄存器状态的 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 下表显示了此方法的可能的返回值。

|值|说明|
|-----------|-----------------|
|E_DIA_INPROLOG|无法在序言代码中执行堆栈帧。|
|E_DIA_SYNTAX|帧程序中出现分析错误。|
|E_DIA_FRAME_ACCESS|无法访问寄存器或内存。|
|E_DIA_VALUE|计算值时出错 (例如，被零除) 。|

## <a name="remarks"></a>备注
 在调试过程中调用此方法展开堆栈。 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)对象由客户端应用程序实现，以接收对寄存器的更新并提供方法使用的方法 `execute` 。

## <a name="see-also"></a>另请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
