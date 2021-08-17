---
description: 检索有关模块是否表示用户代码的信息。
title: IDebugModule3：：IsUserCode |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3::IsUserCode
helpviewer_keywords:
- IDebugModule3::IsUserCode
ms.assetid: 77022946-bb8b-4114-aa81-614df6e54b13
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c62bb7fcd423c7a2f243cd7491b1a3d5489defac3ea22560ba8064a7006653b4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417023"
---
# <a name="idebugmodule3isusercode"></a>IDebugModule3::IsUserCode
检索有关模块是否表示用户代码的信息。

## <a name="syntax"></a>语法

```cpp
HRESULT IsUserCode(
   BOOL* pfUser
);
```

```csharp
int IsUserCode(
   out int pfUser
);
```

## <a name="parameters"></a>参数
`pfUser`\
[out]如果模块 () ，则非零 () `TRUE` `FALSE` 为零。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
