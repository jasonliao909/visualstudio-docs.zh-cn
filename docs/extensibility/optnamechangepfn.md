---
title: OPTNAMECHANGEPFN |Microsoft Docs
description: 了解 OPTNAMECHANGEPFN 回调函数，该函数将名称更改从源代码管理插件传递到 Visual Studio IDE。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- OPTNAMECHANGEPFN
helpviewer_keywords:
- OPTNAMECHANGEPFN callback function
ms.assetid: 147303f3-c7f1-438a-81b7-db891ea3d076
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 15485540921f9a4dbe3ef95e0fd878eeaecc5d5a8861a3e4460999be3d3d8bb7
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414098"
---
# <a name="optnamechangepfn"></a>OPTNAMECHANGEPFN
这是使用选项) 调用 [SccSetOption](../extensibility/sccsetoption-function.md) (指定的回调函数 `SCC_OPT_NAMECHANGEPFN` ，用于将源代码管理插件所做的名称更改传递回 IDE。

## <a name="signature"></a>签名

```cpp
typedef void (*OPTNAMECHANGEPFN)(
   LPVOID pvCallerData,
   LPCSTR pszOldName,
   LPCSTR pszNewName
);
```

## <a name="parameters"></a>参数
 pvCallerData

中使用 option) 在先前对 [SccSetOption](../extensibility/sccsetoption-function.md) (的调用中指定的用户值 `SCC_OPT_USERDATA` 。

 pszOldName

中文件的原始名称。

 pszNewName

中文件已重命名为的名称。

## <a name="return-value"></a>返回值
 无。

## <a name="remarks"></a>备注
 如果在源代码管理操作期间重命名了某个文件，则源代码管理插件可以通过此回调通知 IDE 有关名称更改的信息。

 如果 IDE 不支持此回调，则它将不会调用 [SccSetOption](../extensibility/sccsetoption-function.md) 来指定它。 如果插件不支持此回调，则在 `SCC_E_OPNOTSUPPORTED` `SccSetOption` IDE 尝试设置回调时，它将从函数返回。

## <a name="see-also"></a>请参阅
- [IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccSetOption](../extensibility/sccsetoption-function.md)
