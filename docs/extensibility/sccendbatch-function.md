---
description: 此函数将结束一批源代码管理操作。
title: SccEndBatch 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccEndBatch
helpviewer_keywords:
- SccEndBatch function
ms.assetid: 100e7833-fe0a-45c0-9fca-3e61fd1165b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a608f05cada958a56f3fb5403793c70f5ece5ba9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122124420"
---
# <a name="sccendbatch-function"></a>SccEndBatch 函数
此函数将结束一批源代码管理操作。 这些批处理不能嵌套。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccEndBatch(void);
```

## <a name="parameters"></a>参数
 无。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|成功结束批处理操作。|
|SCC_E_UNKNOWNERROR|非特定故障。|

## <a name="remarks"></a>备注
 源代码管理批处理用于在多个项目或多个上下文中执行相同的源代码管理操作。 批处理可用于消除批处理操作期间用户体验中的冗余对话框。 [SccBeginBatch](../extensibility/sccbeginbatch-function.md)和函数用作 `SccEndBatch` 指示操作的开始和结束的对。 它们不能嵌套。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccBeginBatch](../extensibility/sccbeginbatch-function.md)
