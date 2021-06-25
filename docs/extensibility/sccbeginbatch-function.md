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
ms.workload:
- vssdk
ms.openlocfilehash: 08b9199b98e566a71bfeb95124ebd85781e69950
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904755"
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

|值|描述|
|-----------|-----------------|
|SCC_OK|批处理操作已成功开始。|
|SCC_E_UNKNOWNERROR|非特定故障。|

## <a name="remarks"></a>备注
 源代码管理批处理用于跨多个项目或多个上下文执行相同的操作。 批处理可用于在批处理操作期间消除用户体验中每个项目的冗余对话框。 `SccBeginBatch`函数和[SccEndBatch](../extensibility/sccendbatch-function.md)用作函数对，以指示操作开始和结束。 它们不能嵌套。 `SccBeginBatch` 设置指示批处理操作正在进行的标志。

 当批处理操作生效时，源代码管理插件最多应显示一个对话框，用于向用户提问，并针对所有后续操作应用来自该对话框的响应。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccEndBatch](../extensibility/sccendbatch-function.md)
