---
description: 获取包含文档位置的源文件的文件名。
title: IDebugDocumentPosition2：： GetFileName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2::GetFileName
helpviewer_keywords:
- IDebugDocumentPosition2::GetFileName
ms.assetid: d713635e-088f-465b-b26d-00ac971c9e86
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 93588dec17efc3ef2384ccd8d0df95d1fe8260b4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122119498"
---
# <a name="idebugdocumentposition2getfilename"></a>IDebugDocumentPosition2::GetFileName
获取包含文档位置的源文件的文件名。

## <a name="syntax"></a>语法

```cpp
HRESULT GetFileName( 
   BSTR* pbstrFileName
);
```

```csharp
int GetFileName( 
   out string pbstrFileName
);
```

## <a name="parameters"></a>参数
`pbstrFileName`\
弄返回源文件的文件名。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 源文件可能并不总是有文件名 (源文件可能不存在于磁盘上，例如) 。

## <a name="see-also"></a>请参阅
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
