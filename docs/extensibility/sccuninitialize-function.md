---
description: 此函数将清理先前调用 SccInitialize 创建的任何分配或打开连接，以准备关闭源代码管理插件。
title: SccUninitialize 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccUninitialize
helpviewer_keywords:
- SccUninitialize function
ms.assetid: 17cf5337-d251-4422-bc96-93fe7d48f2ae
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 56d2365df1e613976943bd8ba33f6d49a32566f5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602326"
---
# <a name="sccuninitialize-function"></a>SccUninitialize 函数
此函数将清理先前调用 [SccInitialize](../extensibility/sccinitialize-function.md) 创建的任何分配或打开连接，以准备关闭源代码管理插件。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccUninitialize (
   LPVOID pvContext
);
```

#### <a name="parameters"></a>parameters
 pvContext

[in]指向在 [SccInitialize](../extensibility/sccinitialize-function.md)中创建的源代码管理插件上下文结构的指针。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|清理已成功完成。|

## <a name="remarks"></a>备注
 源代码管理插件负责准备关闭和释放插件为上下文结构分配的内存。 对于每个插件的给定实例，调用该函数一次。 在此调用之前调用[SccInitialize。](../extensibility/sccinitialize-function.md) 调用 时，仍无法打开任何项目 `SccUninitialize` 。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
