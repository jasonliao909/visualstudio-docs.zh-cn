---
description: 此函数从源代码管理中检索每个指定的文件，无需用户交互。
title: SccBackgroundGet 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccBackgroundGet
helpviewer_keywords:
- SccBackgroundGet function
ms.assetid: 69817e52-b9ac-4f4d-820b-2cc9c384f0dc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f010aa2ba214004422048513cea92adf67d62c69
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601033"
---
# <a name="sccbackgroundget-function"></a>SccBackgroundGet 函数
此函数从源代码管理中检索每个指定的文件，无需用户交互。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccBackgroundGet(
   LPVOID  pContext,
   LONG    nFiles,
   LPCSTR* lpFileNames,
   LONG    dwFlags,
   LONG    dwBackgroundOperationID
);
```

### <a name="parameters"></a>parameters
 pContext

[in]源代码管理插件上下文指针。

 nFiles

[in]数组中指定的文件 `lpFileNames` 数。

 lpFileNames

[in， out]要检索的文件的名称的数组。

> [!NOTE]
> 名称必须是完全限定的本地文件名。

 dwFlags 

[in]命令标志 (`SCC_GET_ALL` `SCC_GET_RECURSIVE` 、) 。

 dwBackgroundOperationID

[in]与此操作关联的唯一值。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|操作已成功完成。|
|SCC_E_BACKGROUNDGETINPROGRESS|后台检索已在进行 (源代码管理插件应仅在不支持同时批处理操作时返回) 。|
|SCC_I_OPERATIONCANCELED|操作在完成之前已取消。|

## <a name="remarks"></a>备注
 此函数始终在不同于加载源代码管理插件的线程上调用。 此函数在完成后不应返回;但是，可以使用多个文件列表多次调用它，所有这些文件都是同时调用的。

 参数的使用与 `dwFlags` [SccGet 相同](../extensibility/sccget-function.md)。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccGet](../extensibility/sccget-function.md)
