---
description: 检索有关运行调试器的计算机的信息。
title: IDebugWindowsComputerPort2：：GetComputerInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetComputerInfo
- IDebugWindowsComputerPort2::GetComputerInfo
ms.assetid: 654910b2-c239-44c8-92fc-317680a5672f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e043ccc9f626e5a0ab3b0d8e5c3f1b5a6c1f1fabf66c93a93c233f15111c8ca3
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121306629"
---
# <a name="idebugwindowscomputerport2getcomputerinfo"></a>IDebugWindowsComputerPort2::GetComputerInfo
检索有关运行调试器的计算机的信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetComputerInfo(
   COMPUTER_INFO * pInfo
);
```

```csharp
public int GetComputerInfo(
   out COMPUTER_INFO[] pInfo
);
```

## <a name="parameters"></a>参数
`pInfo`\
[out]对包含计算机信息的结构的引用。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugWindowsComputerPort2](../../../extensibility/debugger/reference/idebugwindowscomputerport2.md)
- [COMPUTER_INFO](../../../extensibility/debugger/reference/computer-info.md)
