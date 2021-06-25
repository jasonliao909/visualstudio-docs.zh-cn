---
description: 此函数重命名源代码管理系统中的文件。
title: SccRename 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccRename
helpviewer_keywords:
- SccRename function
ms.assetid: b467ade6-a1db-4c0b-b60f-7850ec4f79eb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fb3fa392cd4ed31d907fe5913f8d7965a20df05b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900455"
---
# <a name="sccrename-function"></a>SccRename 函数
此函数重命名源代码管理系统中的文件。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccRename(
   LPVOID pvContext,
   HWND   hWnd,
   LPCSTR lpFileName,
   LPCSTR lpNewName
);
```

#### <a name="parameters"></a>参数
 pvContext

[in]源代码管理插件上下文结构。

 hWnd

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 lpFileName

[in]要重命名的文件的完全限定文件名。

 lpNewName

[in]完全限定的新名称。 如果目录路径不同，则文件已从一个子目录移动到另一个子目录。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|重命名操作已成功完成。|
|SCC_E_PROJNOTOPEN|项目未在源代码管理下打开。|
|SCC_E_FILENOTCONTROLLED|该文件不在源代码管理下。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。|
|SCC_E_NOTAUTHORIZED|用户无权完成此操作。|
|SCC_E_COULDNOTCREATEPROJECT|项目无法作为重命名过程的一部分创建。|
|SCC_E_OPNOTPERFORMED|未执行该操作。|
|SCC_E_NONSPECIFICERROR|发生未指定或常规错误。|

## <a name="remarks"></a>备注
 此函数可用于重命名文件或将其从源代码管理系统中的一个位置移到另一个位置。 源代码管理插件不应尝试访问磁盘上的文件。 IDE 负责重命名本地文件。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
