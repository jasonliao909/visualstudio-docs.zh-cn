---
description: 此函数初始化源代码管理插件，并针对 IDE (集成开发环境) 。
title: SccInitialize 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccInitialize
helpviewer_keywords:
- SccInitialize function
ms.assetid: 5bc0d28b-2c68-4d43-9e51-541506a8f76e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 633e8909febd758df455a9375f735a93e3407c77
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902522"
---
# <a name="sccinitialize-function"></a>SccInitialize 函数
此函数初始化源代码管理插件，并针对 IDE (集成开发环境) 。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccInitialize (
   LPVOID* ppvContext,
   HWND    hWnd,
   LPCSTR  lpCallerName,
   LPSTR   lpSccName,
   LPLONG  lpSccCaps,
   LPSTR   lpAuxPathLabel,
   LPLONG  pnCheckoutCommentLen,
   LPLONG  pnCommentLen
);
```

#### <a name="parameters"></a>参数
 `ppvContext`

[in]源代码管理插件可以在此处放置指向其上下文结构的指针。

 `hWnd`

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 `lpCallerName`

[in]调用源代码管理插件的程序的名称。

 `lpSccName`

[in， out]源代码管理插件将自己的名称置于的缓冲区 (不超过 `SCC_NAME_LEN`) 。

 `lpSccCaps`

[out]返回源代码管理插件的功能标志。

 `lpAuxPathLabel`

[in， out]源代码管理插件在缓冲区中插入一个字符串，该字符串描述 `lpAuxProjPath` [SccOpenProject](../extensibility/sccopenproject-function.md) 和 [SccGetProjPath](../extensibility/sccgetprojpath-function.md) (返回的参数 `SCC_AUXLABEL_LEN` ，) 。

 `pnCheckoutCommentLen`

[out]返回签出注释的最大允许长度。

 `pnCommentLen`

[out]返回其他注释的最大允许长度。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|源代码管理初始化成功。|
|SCC_E_INITIALIZEFAILED|无法初始化系统。|
|SCC_E_NOTAUTHORIZED|不允许用户执行指定的操作。|
|SCC_E_NONSPECFICERROR|非特定故障;源代码管理系统未初始化。|

## <a name="remarks"></a>备注
 IDE 首次加载源代码管理插件时调用此函数。 它使 IDE 能够将某些信息（如调用方名称）传递给插件。 IDE 还会返回某些信息，例如注释的最大允许长度和插件的功能。

 指向 `ppvContext` 指针 `NULL` 。 源代码管理插件可以分配结构供自己使用，并存储指向 该结构的指针 `ppvContext` 。 IDE 将此指针传递给其他每个 VSSCI API 函数，使插件具有可用的上下文信息，而无需使用全局存储并支持插件的多个实例。 调用 [SccUninitialize](../extensibility/sccuninitialize-function.md) 时，应解除分配此结构。

 和 `lpCallerName` `lpSccName` 参数使 IDE 和源代码管理插件能够交换名称。 这些名称可能仅用于区分多个实例，也可能实际出现在菜单或对话框中。

 参数是一个字符串，用作注释，用于标识存储在解决方案文件中，在调用 `lpAuxPathLabel` [SccOpenProject](../extensibility/sccopenproject-function.md)时传递给源代码管理插件的辅助项目路径。 [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] 使用字符串"SourceSafe 项目：";其他源代码管理插件应避免使用此特定字符串。

 `lpSccCaps`参数为源代码管理插件提供了一个存储指示插件功能的位标志的位置。  (有关功能位标志的完整列表，请参阅功能 [标志](../extensibility/capability-flags.md)) 。 例如，如果插件计划将结果写入调用方提供的回调函数，插件将设置功能位SCC_CAP_TEXTOUT。 这会向 IDE 发出信号，指示为版本控制结果创建一个窗口。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [功能标志](../extensibility/capability-flags.md)
