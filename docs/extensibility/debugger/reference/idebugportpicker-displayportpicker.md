---
description: 显示允许用户选择端口的指定对话框。
title: IDebugPortPicker：:D isplayPortPicker |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- DisplayPortPicker
- IDebugPortPicker::DisplayPortPicker
ms.assetid: 08511ef5-be64-4069-b169-a569cc94bc64
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f1acd8565c65e522d75652701fdf8333c70faa40
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122126838"
---
# <a name="idebugportpickerdisplayportpicker"></a>IDebugPortPicker::DisplayPortPicker
显示允许用户选择端口的指定对话框。

## <a name="syntax"></a>语法

```cpp
HRESULT DisplayPortPicker(
   HWND hwndParentDialog,
   BSTR* pbstrPortId
);
```

```csharp
public int DisplayPortPicker(
   int hwndParentDialog,
   out string pbstrPortId
);
```

## <a name="parameters"></a>参数
`hwndParentDialog`\
[in]父对话框的句柄。

`pbstrPortId`\
[out]端口标识符字符串。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。 返回值 (或 的返回值，其 设置为) `S_FALSE` `S_OK` `BSTR` `NULL` 指示用户单击了"取消 **"。**

## <a name="see-also"></a>请参阅
- [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md)
