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
ms.openlocfilehash: a376a8d51d7b4d974bf0c7b609bbc53cc334cb33
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122057572"
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
 `GetUserName` 返回显示在"附加到进程" **对话框的"** 用户名" **列中的用户名** 。 若要查看"**附加到进程"** 对话框，请在集成开发环境的"工具"菜单上单击"附加到进程 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] " (IDE) 。

## <a name="see-also"></a>请参阅
- [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
