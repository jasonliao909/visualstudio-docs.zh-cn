---
description: 指示整个文档已销毁。
title: IDebugDocumentTextEvents2：： onDestroy |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentTextEvents2::OnDestroy
helpviewer_keywords:
- IDebugDocumentTextEvents2::onDestroy
ms.assetid: 60e4689c-c899-4c14-9d18-96393b741e1f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 011be7f08f6af124dd78e082ce5cd0d38afe982b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066290"
---
# <a name="idebugdocumenttextevents2ondestroy"></a>IDebugDocumentTextEvents2::onDestroy
指示整个文档已销毁。

## <a name="syntax"></a>语法

```cpp
HRESULT onDestroy( 
   void 
);
```

```csharp
int onDestroy();
```

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)
