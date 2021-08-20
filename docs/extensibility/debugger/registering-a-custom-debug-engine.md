---
title: 注册自定义调试引擎 |Microsoft Docs
description: 了解调试引擎如何将自身注册为类工厂（遵循 COM 约定），以及如何通过注册表注册 Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, registering
ms.assetid: 9984cd3d-d34f-4662-9ace-31766499abf5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 2499e4aef01bd4812a705afd7777cacd7eb2ba14
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122117938"
---
# <a name="register-a-custom-debug-engine"></a>注册自定义调试引擎
调试引擎必须将自身注册为类工厂（遵循 COM 约定），并通过 Visual Studio 注册表子项注册 Visual Studio。

> [!NOTE]
> 可以在 TextInterpreter 示例中找到如何注册调试引擎的示例，该示例作为教程的一部分生成 [：使用 ATL COM 构建调试引擎](/previous-versions/bb147024(v=vs.90))。

## <a name="dll-server-process"></a>DLL 服务器进程
 调试引擎通常在自己的 DLL 中设置为 COM 服务器。 因此，在 Visual Studio 可以访问之前，调试引擎必须使用 COM 注册其类工厂的 CLSID。 然后，调试引擎必须将自己注册到 Visual Studio，以便建立) 调试引擎支持的任何属性 (（也称为指标）。 写入 Visual Studio 注册表子项的度量值的选择取决于调试引擎支持的功能。

 [用于调试的 SDK 帮助](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) 器不仅描述注册调试引擎所需的注册表位置;它还介绍了 *dbgmetric* 库，其中包含许多适用于 c + + 开发人员的有用函数和声明，使操作更容易。

### <a name="example"></a>示例
 下面的示例从 TextInterpreter 示例 () 演示了如何使用 `SetMetric` *dbgmetric*) 中的函数 (向 Visual Studio 注册调试引擎。 还会在 *dbgmetric* 中定义要传递的指标。

> [!NOTE]
> TextInterpreter 是一个基本的调试引擎;它不会进行设置，因此不会注册任何其他功能。 一个更完整的调试引擎可能有一个 `SetMetric` 或其等效的调用的完整列表，一个用于调试引擎支持的每个功能。

```
// Define base registry subkey to Visual Studio.
static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0";

HRESULT CTextInterpreterModule::RegisterServer(BOOL bRegTypeLib, const CLSID * pCLSID)
{
    SetMetric(metrictypeEngine, __uuidof(Engine), metricName, L"Text File", false, strRegistrationRoot);
    SetMetric(metrictypeEngine, __uuidof(Engine), metricCLSID, CLSID_Engine, false, strRegistrationRoot);
    SetMetric(metrictypeEngine, __uuidof(Engine), metricProgramProvider, CLSID_MsProgramProvider, false, strRegistrationRoot);

    return base::RegisterServer(bRegTypeLib, pCLSID);
}
```

## <a name="see-also"></a>请参阅
- [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)
- [SDK 调试帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [教程：使用 ATL COM 构建调试引擎](/previous-versions/bb147024(v=vs.90))