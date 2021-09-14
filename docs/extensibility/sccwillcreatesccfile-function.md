---
description: 此函数确定源代码管理插件是否支持创建 MSSCCPRJ。每个给定文件的 SCC 文件。
title: SccWillCreateSccFile 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccWillCreateSccFile
helpviewer_keywords:
- SccWillCreateSccFile function
ms.assetid: 0d7542f0-4351-41b3-b24c-960ab99c05a1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: ef42e88426f5fa91fcebc5e8ffc1b0954c6554ee
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602325"
---
# <a name="sccwillcreatesccfile-function"></a>SccWillCreateSccFile 函数
此函数确定源代码管理插件是否支持创建 MSSCCPRJ。每个给定文件的 SCC 文件。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccWillCreateSccFile(
   LPVOID  pContext,
   LONG    nFiles,
   LPCSTR* lpFileNames,
   LPBOOL  pbSccFiles
);
```

#### <a name="parameters"></a>parameters
 pContext

[in]源代码管理插件上下文指针。

 nFiles

[in]数组中包含的文件名 `lpFileNames` 数以及数组 `pbSccFiles` 的长度。

 lpFileNames

[in]要检查数组的完全限定文件名 (必须由调用方分配) 。

 pbSccFiles

[in， out]要存储结果的数组。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|成功。|
|SCC_E_INVALIDFILEPATH|数组中的一个路径无效。|
|SCC_E_NONSPECIFICERROR|非特定故障。|

## <a name="remarks"></a>备注
 使用文件列表调用此函数，以确定源代码管理插件是否支持 MSSCCPRJ。有关 MSSCCPRJ (每个给定文件的 SCC 文件。SCC 文件，请参阅 [MSSCCPRJ。SCC 文件](../extensibility/mssccprj-scc-file.md)) 。 源代码管理插件可以声明它们是否具有创建 MSSCCPRJ 的能力。在初始化过程中通过声明来保存 SCC `SCC_CAP_SCCFILE` 文件。 插件返回 或 `TRUE` `FALSE` 数组中的每个文件， `pbSccFiles` 以指示哪些给定文件具有 MSSCCPRJ。SCC 支持。 如果插件从 函数返回成功代码，则使用返回数组中的值。 失败时，将忽略数组。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [MSSCCPRJ.SCC 文件](../extensibility/mssccprj-scc-file.md)
