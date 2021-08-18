---
description: 此函数启动源代码管理操作批处理序列。
title: SccBeginBatch 函数|Microsoft Docs
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122144595"
---
# <a name="sccbeginbatch-function"></a>SccBeginBatch 函数
此函数启动源代码管理操作批处理序列。 将 [调用 SccEndBatch](../extensibility/sccendbatch-function.md) 以结束批处理。 这些批不能嵌套。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccBeginBatch(void);
```

### <a name="parameters"></a>参数
 无。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|批处理操作已成功开始。|
|SCC_E_UNKNOWNERROR|非特定故障。|

## <a name="remarks"></a>备注
 源代码管理批处理用于跨多个项目或多个上下文执行相同的操作。 批处理可用于在批处理操作期间消除用户体验中每个项目的冗余对话框。 `SccBeginBatch`函数和[SccEndBatch](../extensibility/sccendbatch-function.md)用作函数对，以指示操作开始和结束。 它们不能嵌套。 `SccBeginBatch` 设置指示批处理操作正在进行的标志。

 当批处理操作生效时，源代码管理插件最多应显示一个对话框，用于向用户提问，并针对所有后续操作应用来自该对话框的响应。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccEndBatch](../extensibility/sccendbatch-function.md)
