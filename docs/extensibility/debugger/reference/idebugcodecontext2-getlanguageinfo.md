---
description: 获取此代码上下文的语言信息。
title: IDebugCodeContext2：： GetLanguageInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCodeContext2::GetLanguageInfo
helpviewer_keywords:
- IDebugCodeContext2::GetLanguageInfo
ms.assetid: 03002ef1-9fe6-44b6-b23b-ef7b86b2b21b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: be16e29ae21cec11aee264fa468b35c28cd3d348770fc856edbfa7d7e04008a8
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342474"
---
# <a name="idebugcodecontext2getlanguageinfo"></a>IDebugCodeContext2::GetLanguageInfo
获取此代码上下文的语言信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetLanguageInfo( 
   BSTR* pbstrLanguage,
   GUID* pguidLanguage
);
```

```csharp
int GetLanguageInfo( 
   ref string pbstrLanguage,
   ref Guid pguidLanguage
);
```

## <a name="parameters"></a>参数
`pbstrLanguage`\
[in，out]返回一个字符串，其中包含语言的名称，如 "c + +"。

`pguidLanguage`\
[in，out]返回代码上下文语言的 GUID，例如 `guidCPPLang` 。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 至少一个参数必须返回非 null 值。

## <a name="see-also"></a>另请参阅
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
