---
description: 指定堆栈帧类型。
title: StackFrameTypeEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- StackFrameTypeEnum enumeration
ms.assetid: 61e40163-eee0-4c1f-af47-cef3771bdc41
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 400a1db1f8a5ee5ffde7e00a428d83d170dc0d05
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832802"
---
# <a name="stackframetypeenum"></a>StackFrameTypeEnum
指定堆栈帧类型。

## <a name="syntax"></a>语法

```C++
enum StackFrameTypeEnum {
    FrameTypeFPO,
    FrameTypeTrap,
    FrameTypeTSS,
    FrameTypeStandard,
    FrameTypeFrameData,
    FrameTypeUnknown = -1
};
```

## <a name="elements"></a>元素
`FrameTypeFPO` 帧指针已省略；FPO 信息可用。

`FrameTypeTrap` 内核陷阱帧。

`FrameTypeTSS` 内核陷阱帧。

`FrameTypeStandard` 标准 EBP 堆栈帧。

`FrameTypeFrameData` 帧指针已省略；框架数据信息可用。

不包含任何调试信息的 `FrameTypeUnknown` 帧。

## <a name="remarks"></a>备注
此枚举中的值是通过调用 [IDiaStackFrame::get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md) 方法返回的。

## <a name="requirements"></a>要求
标头：cvconst.h

## <a name="see-also"></a>另请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaStackFrame::get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md)
