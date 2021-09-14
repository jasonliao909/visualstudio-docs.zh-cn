---
description: 此函数启动源代码管理操作的批处理序列。
title: SccBeginBatch 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccBeginBatch
helpviewer_keywords:
- SccBeginBatch function
ms.assetid: 33968183-2e15-4e0d-955b-ca12212d1c25
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: fc1d78840915899181046d3e1bfb19d554751c1a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600685"
---
# <a name="sccbeginbatch-function"></a>SccBeginBatch 函数
此函数启动源代码管理操作的批处理序列。 将调用 [SccEndBatch](../extensibility/sccendbatch-function.md) 以结束批处理。 这些批处理不能嵌套。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccBeginBatch(void);
```

### <a name="parameters"></a>parameters
 无。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|成功的批处理操作。|
|SCC_E_UNKNOWNERROR|非特定故障。|

## <a name="remarks"></a>备注
 源代码管理批处理用于在多个项目或多个上下文中执行相同的操作。 批处理可用于消除批处理操作期间用户体验中的冗余每个项目对话框。 `SccBeginBatch`函数和[SccEndBatch](../extensibility/sccendbatch-function.md)用作函数对，用于指示操作的开始和结束。 它们不能嵌套。 `SccBeginBatch` 设置一个标志，指示正在进行批处理操作。

 批处理操作生效时，源代码管理插件最多应向用户显示一个对话框，并在所有后续操作上应用该对话框的响应。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccEndBatch](../extensibility/sccendbatch-function.md)
