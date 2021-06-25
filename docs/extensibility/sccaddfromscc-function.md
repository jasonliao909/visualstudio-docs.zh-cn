---
description: 此函数允许用户浏览源代码管理系统中已有的文件，然后使这些文件成为当前项目的一部分。
title: SccAddFromScc 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccAddFromScc
helpviewer_keywords:
- SccAddFromScc function
ms.assetid: 902e764d-200e-46e1-8c42-4da7b037f9a0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 48560f135d73c4e53ba132845f4c768cdf4ac982
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904871"
---
# <a name="sccaddfromscc-function"></a>SccAddFromScc 函数
此函数允许用户浏览源代码管理系统中已有的文件，然后使这些文件成为当前项目的一部分。 例如，此函数可以将公共头文件获取到当前项目中，而无需复制该文件。 文件的返回数组 `lplpFileNames` 包含用户要添加到 IDE 项目的文件列表。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccAddFromScc (
   LPVOID   pvContext,
   HWND     hWnd,
   LPLONG   lpnFiles,
   LPCSTR** lplpFileNames
);
```

### <a name="parameters"></a>参数
 pvContext

[in]源代码管理插件上下文结构。

 hWnd

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 lpnFiles

[in， out]要添加的文件数的缓冲区。  (如果要 `NULL` 释放 指向的内存， `lplpFileNames` 则此为 。 有关详细信息，请参阅备注。) 

 lplpFileNames

[in， out]指向没有目录路径的所有文件名的指针数组。 此数组由源代码管理插件分配和释放。 如果 = 1 且 不是 ，则 指向的数组中的名字 `lpnFiles` `lplpFileNames` `NULL` `lplpFileNames` 包含目标文件夹。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|已成功找到文件并添加到项目中。|
|SCC_I_OPERATIONCANCELED|操作已取消，但不起作用。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|

## <a name="remarks"></a>备注
 IDE 调用此函数。 如果源代码管理插件支持指定本地目标文件夹，IDE 将 `lpnFiles` 传递 = 1，将本地文件夹名称传递给 `lplpFileNames` 。

 当对函数的调用返回时，插件将值分配给 和 ，并根据需要为文件名数组分配 (请注意，此分配将替换) 中的 `SccAddFromScc` `lpnFiles` `lplpFileNames` `lplpFileNames` 指针。 源代码管理插件负责将所有文件放入用户的目录或指定的指定文件夹中。 然后，IDE 将文件添加到 IDE 项目。

 最后，IDE 第二次调用此函数，为 传递 `NULL` `lpnFiles` 。 源代码管理插件将其解释为特殊信号，以释放中为文件名数组分配的内存 `lplpFileNames``.`

 `lplpFileNames` 是指针 `char ***` 。 源代码管理插件将指针指向指向文件名的指针数组，从而以此 API 的标准方式传递列表。

> [!NOTE]
> VSSCI API 的初始版本未提供一种方法来指示所添加文件的目标项目。 为了适应这种情况，已增强参数的语义 `lplpFIleNames` ，使其成为输入/输出参数，而不是输出参数。 如果仅指定了单个文件（即由 = 1 指向的值），则 `lpnFiles` 的第一个元素 `lplpFileNames` 包含目标文件夹。 若要使用这些新语义，IDE 将调用 参数 `SccSetOption` 设置为 `nOption` 的函数 `SCC_OPT_SHARESUBPROJ` 。 如果源代码管理插件不支持语义，它将返回 `SCC_E_OPTNOTSUPPORTED` 。 这样做会禁用"从源代码 **管理中添加"** 功能。 如果插件支持从 **源代码管理添加** 功能 () ，则它必须支持新语义并 `SCC_CAP_ADDFROMSCC` 返回 `SCC_I_SHARESUBPROJOK` 。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccSetOption](../extensibility/sccsetoption-function.md)
