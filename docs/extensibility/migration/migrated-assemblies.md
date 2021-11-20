---
title: VS SDK NuGet包
description: 了解 VS SDK 元包NuGet在将扩展迁移到 2022 Visual Studio时可能需要Visual Studio包。
ms.date: 06/08/2021
ms.topic: conceptual
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
monikerRange: vs-2022
ms.workload:
- vssdk
feedback_system: GitHub
ms.openlocfilehash: 79ab6bca8437017a2a1ec781407e89a343527050
ms.sourcegitcommit: 932cf0f653c6258b73f42102d134cbaf50b8f20c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2021
ms.locfileid: "132880061"
---
# <a name="sdk-reference-packages"></a>SDK 参考包

创作扩展Visual Studio方法是引用 NuGet[ `Microsoft.VisualStudio.Sdk` 包](https://www.nuget.org/packages/microsoft.visualstudio.sdk)。
此包适用于 Visual Studio 2017 (15.0) 、Visual Studio 2019 (16.0、16.9) 和 Visual Studio 2022。

根据扩展，可能需要添加上述元包中未包含的额外 VS SDK 包。
引用特定的其他 SDK 包时，这些包可能因主要 VS 版本而异。

请注意，许多互操作程序集在 2022 年 2 月之前Visual Studio嵌入。 从 2022 Visual Studio开始，不再需要或支持嵌入。
*请引用* 互操作程序集，而不是链接它们。

下表提供了从程序集或包进行映射，Visual Studio 2022 年 2 月之前扩展可能已经引用了新的包 ID，在面向 2022 年 2 月时Visual Studio ID。 在某些情况下，程序集现在可用于NuGet以前仅从本地程序集安装Visual Studio包。

2022 Visual Studio之前 | Visual Studio 2022
--|--
`envdte` | `Microsoft.VisualStudio.Interop`
`envdte100` | `Microsoft.VisualStudio.Interop`
`envdte80` | `Microsoft.VisualStudio.Interop`
`envdte90` | `Microsoft.VisualStudio.Interop`
`envdte90a` | `Microsoft.VisualStudio.Interop`
`extensibility` | `Microsoft.VisualStudio.Interop`
`Microsoft.MSXML` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.CommandBars` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Designer.Interfaces` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.OLE.Interop` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.SDK.EmbedInteropTypes` |  (已过时。 删除 reference.) 
`Microsoft.VisualStudio.Shell.Embeddable` | `Microsoft.VisualStudio.Shell.Framework`
`Microsoft.VisualStudio.Shell.Interop.10.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.11.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.12.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.12.1.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.14.1.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.14.2.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.14.3.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.15.0.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.15.1.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.15.3.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.15.5.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.15.6.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.15.7.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.15.8.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.0.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.1.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.10.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.2.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.3.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.4.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.5.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.6.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.7.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.9.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.8.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.9.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.10.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.11.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.12.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.12.1.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.14.2.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.15.0.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.15.1.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.16.0.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.8.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.9.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.UserNotifications.Interop.12.0.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.VSHelp.dll` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.VSHelp80.dll` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.WCFReference.Interop` | `Microsoft.VisualStudio.Interop`
`stdole` | `Microsoft.VisualStudio.Interop`
`VSLangProj` | `Microsoft.VisualStudio.Interop`
`VSLangProj100` | `Microsoft.VisualStudio.Interop`
`VSLangProj110` | `Microsoft.VisualStudio.Interop`
`VSLangProj140` | `Microsoft.VisualStudio.Interop`
`VSLangProj150` | `Microsoft.VisualStudio.Interop`
`VSLangProj157` | `Microsoft.VisualStudio.Interop`
`VSLangProj158` | `Microsoft.VisualStudio.Interop`
`VSLangProj165` | `Microsoft.VisualStudio.Interop`
`VSLangProj2` | `Microsoft.VisualStudio.Interop`
`VSLangProj80` | `Microsoft.VisualStudio.Interop`
`VSLangProj90` | `Microsoft.VisualStudio.Interop`

请注意，现在只有一个合并的互操作程序集中有多少个互操作程序集可用。
如果上表中未显示包，则两个版本中的包可能相同。
