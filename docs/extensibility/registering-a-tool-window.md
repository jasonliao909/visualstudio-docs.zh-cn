---
title: 注册工具窗口|Microsoft Docs
description: 了解如何使用 ProvideToolWindowAttribute 和 ProvideToolWindowVisibilityAttribute 向 Visual Studio 注册工具窗口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tool windows, registering managed
- tool windows, registering
ms.assetid: 8c8c4a24-3da4-497b-9db2-0ddd7cfbfdd2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 34ce07f873e2dd23f2c2ae296b482e3b7049651c49757dedacf22508d180fc53
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121336702"
---
# <a name="register-a-tool-window"></a>注册工具窗口
可以使用 和 注册工具 <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> 窗口  <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute> 。

## <a name="example"></a>示例

```csharp

[ProvideToolWindow(typeof(PersistedWindowPane), Style = MsVsShell.VsDockStyle.Tabbed, Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")]
[ProvideToolWindow(typeof(DynamicWindowPane), PositionX=250, PositionY=250, Width=160, Height=180, Transient=true)]
[ProvideToolWindowVisibility(typeof(DynamicWindowPane), /*UICONTEXT_SolutionExists*/"f1536ef8-92ec-443c-9ed7-fdadf150da82")]
[ProvideMenuResource(1000, 1)]
[PackageRegistration(UseManagedResourcesOnly = true)]
[Guid("01069CDD-95CE-4620-AC21-DDFF6C57F012")]
public class PackageToolWindow : Package
{
```

 在以上代码中， <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> 将 和 `PersistedWindowPane` `DynamicWindowPane` 工具窗口注册到 Visual Studio。 持久化工具窗口停靠并选项卡式 **解决方案资源管理器，动态** 窗口具有默认的起始位置和大小。 动态窗口是暂时性的，表示未在启动时创建。 这会在 `DontForceCreate` 系统注册表的 `ToolWindows` 项中写入值。 有关详细信息，请参阅工具 [窗口显示配置](/previous-versions/visualstudio/visual-studio-2015/extensibility/tool-window-display-configuration?preserve-view=true&view=vs-2015)。