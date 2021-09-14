---
description: 此函数显示文件或项目的源代码管理属性。
title: SccProperties 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccProperties
helpviewer_keywords:
- SccProperties function
ms.assetid: 1bed38c9-73d2-4474-9717-f9dc26a89cbe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 99d83dc2cdf5dd39a6f55f39ff78a203b4ed29b0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600683"
---
# <a name="sccproperties-function"></a>SccProperties 函数
此函数显示文件或项目的源代码管理属性。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccProperties (
   LPVOID pvContext,
   HWND   hWnd,
   LPCSTR lpFileName
);
```

#### <a name="parameters"></a>parameters
 pvContext

[in]源代码管理插件上下文结构。

 hWnd

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 lpFileName

[in]文件或项目的完全限定路径名称。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功显示属性。|
|SCC_I_RELOADFILE|版本控制系统已修改文件属性，因此 IDE 应重新加载此文件。|
|SCC_E_PROJNOTOPEN|指定的项目尚未在源代码管理中打开。|
|SCC_E_NOTAUTHORIZED|用户无权查看此文件或项目的属性。|
|SCC_E_FILENOTCONTROLLED|指定的文件或项目不在源代码管理下。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|发生未知或常规错误。|

## <a name="remarks"></a>备注
 源代码管理插件在其自己的对话框中显示属性。

 这些属性由源代码管理插件定义，可能不同于插件和插件。 如果插件允许用户更改文件的源代码管理属性，则它应返回以指示 IDE 需要重新加载此文件或 `SCC_I_RELOAD` 项目。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
