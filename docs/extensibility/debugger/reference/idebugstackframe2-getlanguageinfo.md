---
description: 获取与此堆栈帧关联的语言。
title: IDebugStackFrame2：： GetLanguageInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetLanguageInfo
helpviewer_keywords:
- IDebugStackFrame2::GetLanguageInfo
ms.assetid: 0e12fd92-f155-46a7-8272-cda279388cfb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f7b87cc242a1d9abeaebdfe768bb101dead6d134
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122063728"
---
# <a name="idebugstackframe2getlanguageinfo"></a>IDebugStackFrame2::GetLanguageInfo

获取与此堆栈帧关联的语言。

## <a name="syntax"></a>语法

```cpp
HRESULT GetLanguageInfo ( 
   BSTR* pbstrLanguage,
   GUID* pguidLanguage
);
```

```csharp
int GetLanguageInfo ( 
   ref string pbstrLanguage,
   ref Guid   pguidLanguage
);
```

## <a name="parameters"></a>参数

`pbstrLanguage`\
弄返回实现与此堆栈帧关联的方法的语言名称。

`pguidLanguage`\
弄返回 `GUID` 语言的。 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]例如，对于语言，可以返回以下内容：

- `guidVBScriptLang`\

- `guidJScriptLang`\

- `guidCPPLang`\

- `guidVBLang`\

- `guidSQLLang`\

- `guidScriptLang`\

## <a name="return-value"></a>返回值

 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>请参阅

- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
