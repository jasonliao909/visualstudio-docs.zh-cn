---
description: 表示用于选择端口的自定义 UI。
title: IDebugPortPicker |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortPicker interface
ms.assetid: 8b7f6685-a3c5-4355-b706-c1b574f6ff84
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 7800956063236055962eb295a3101b40f99f22a1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122072196"
---
# <a name="idebugportpicker"></a>IDebugPortPicker
表示用于选择端口的自定义 UI。

## <a name="syntax"></a>语法

```
IDebugPortPicker : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 此接口由端口供应商实现。 端口提供程序通过将其作为 CLSID 公开，并将指标指向已公开的 CLSID 来定义端口选取器 `metricPortPickerCLSID` 。

## <a name="methods"></a>方法
 下表显示的方法 `IDebugPortPicker` 。

|方法|说明|
|------------|-----------------|
|[DisplayPortPicker](../../../extensibility/debugger/reference/idebugportpicker-displayportpicker.md)|显示允许用户选择端口的指定对话框。|
|[SetSite](../../../extensibility/debugger/reference/idebugportpicker-setsite.md)|设置服务提供程序。|

## <a name="requirements"></a>要求
 标头： Msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
