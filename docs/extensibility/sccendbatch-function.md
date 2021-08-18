---
description: 此函数结束一批源代码管理操作。
title: SccEndBatch 函数|Microsoft Docs
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
ms.openlocfilehash: c3fa3c7485add8773a550aabff76501f08d585bc05ceed3cbcebe56f60a67c3a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121388148"
---
# <a name="sccendbatch-function"></a>SccEndBatch 函数
此函数结束一批源代码管理操作。 这些批不能嵌套。

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
|SCC_OK|批处理操作已成功完成。|
|SCC_E_UNKNOWNERROR|非特定故障。|

## <a name="remarks"></a>备注
 源代码管理批处理用于跨多个项目或多个上下文执行相同的源代码管理操作。 批处理可用于在批处理操作期间消除用户体验中的冗余对话框。 [SccBeginBatch](../extensibility/sccbeginbatch-function.md)和 函数用作对来指示 `SccEndBatch` 操作开始和结束。 它们不能嵌套。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccBeginBatch](../extensibility/sccbeginbatch-function.md)
