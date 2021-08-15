---
description: 从端口供应商获取用户名。
title: IDebugProcessSecurity：：GetUserName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity::GetUserName
ms.assetid: c73c60ac-da6e-45ae-8f04-95353a24ca3e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 025e6d4b707280ee00cd262cb917ab30c47298835e0d881faa000c049796a0fd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121451765"
---
# <a name="idebugprocesssecuritygetusername"></a>IDebugProcessSecurity::GetUserName
从端口供应商获取用户名。

## <a name="syntax"></a>语法

```cpp
HRESULT GetUserName(
    BSTR *pbstrUserName
);
```

```csharp
int GetUserName (
    string pbstrUserName
);
```

## <a name="parameters"></a>参数
`pbstrUserName`\
[out]包含用户名的字符串。

## <a name="return-value"></a>返回值
 如果该方法成功，则它会返回 `S_OK`。 否则，它将返回错误代码。

## <a name="remarks"></a>备注
 `GetUserName` 返回显示在"附加到进程" **对话框的"** 用户名" **列中的用户名** 。 若要查看"**附加到进程"** 对话框，请单击 IDE 中集成开发环境中"工具"菜单上的"附加到进程 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] (") 。

## <a name="see-also"></a>另请参阅
- [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
