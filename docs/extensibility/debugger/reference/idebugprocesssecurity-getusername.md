---
description: 获取端口提供商提供的用户名。
title: IDebugProcessSecurity：： GetUserName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity::GetUserName
ms.assetid: c73c60ac-da6e-45ae-8f04-95353a24ca3e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 04ad8bf6ba572a1f9e14e26ef2ca37d021f6e3a0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166198"
---
# <a name="idebugprocesssecuritygetusername"></a>IDebugProcessSecurity::GetUserName
获取端口提供商提供的用户名。

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
弄一个包含用户名的字符串。

## <a name="return-value"></a>返回值
 如果该方法成功，则它会返回 `S_OK`。 否则，它将返回错误代码。

## <a name="remarks"></a>备注
 `GetUserName`返回在 "**附加到进程**" 对话框的 "**用户名**" 列中显示的用户名。 若要查看 "**附加到进程**" 对话框，请在集成开发环境中的 "**工具**" 菜单上单击 "**附加到进程**" [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] (IDE) 。

## <a name="see-also"></a>另请参阅
- [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
