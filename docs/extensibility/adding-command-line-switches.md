---
title: 添加Command-Line开关|Microsoft Docs
description: 了解如何在执行命令时添加应用于 VSPackage 的devenv.exe开关。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- command-line switches, adding
- command-line switches, retrieving
- IVsAppCommandLine::GetOption method
- command line, switches
ms.assetid: 8bbbd87e-76fe-4fb5-8ef9-65f5e31967cf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 539ab9c7a70d1e2ed22c864132048175eebfcda3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602513"
---
# <a name="add-command-line-switches"></a>添加命令行开关
可以在执行 VSPackage 时添加 *devenv.exe开关。* 使用 <xref:Microsoft.VisualStudio.Shell.ProvideAppCommandLineAttribute> 声明开关的名称及其属性。 此示例中，为名为 **AddCommandSwitchPackage** 的 VSPackage 子类添加了 MySwitch 开关，该子类没有参数且已自动加载 VSPackage。

```csharp
[ProvideAppCommandLine("MySwitch", typeof(AddCommandSwitchPackage), Arguments = "0", DemandLoad = 1)]
```

 以下说明显示了命名参数。

|名称|说明|
|-|-|
| 参数 | 开关的参数数。 可以是"*"或参数列表。 |
| DemandLoad | 如果设置为 1，则自动加载 VSPackage，否则设置为 0。 |
| HelpString | 要与 **devenv /？** 一起显示的字符串的帮助字符串或资源 ID。 |
| 名称 | 开关。 |
| PackageGuid | 包的 GUID。 |

 Arguments 的第一个值通常为 0 或 1。 特殊值"*"可用于指示命令行的整个余下部分都是 参数。 对于用户必须传递调试器命令字符串的调试方案，这非常有用。

 DemandLoad 值为 `true` (1) 或 (`false` 0) 指示应自动加载 VSPackage。

 HelpString 值是出现在 **devenv /？** 帮助显示。 此值应格式为"#nnn"，其中 nnn 是整数。 资源文件的字符串值应以新的行字符结尾。

 Name 值是开关的名称。

 PackageGuid 值是实现此开关的包的 GUID。 IDE 使用此 GUID 在应用命令行开关的注册表中查找 VSPackage。

## <a name="retrieve-command-line-switches"></a>检索命令行开关
 加载包后，可以通过完成以下步骤来检索命令行开关。

1. 在 VSPackage 的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> 实现中，调用 `QueryService` <xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine> 获取 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine> 接口。

2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine.GetOption%2A> 以检索用户输入的命令行开关。

   以下代码演示如何确定用户是否输入了 MySwitch 命令行开关：

```csharp
IVsAppCommandLine cmdline = (IVsAppCommandLine)GetService(typeof(SVsAppCommandLine));

int isPresent = 0;
string optionValue = "";

cmdline.GetOption("MySwitch", out isPresent, out optionValue);
```

 每次加载包时，你负责检查命令行开关。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>
- [Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)
- [CreatePkgDef 实用工具](../extensibility/internals/createpkgdef-utility.md)
- [.Pkgdef 文件](https://devblogs.microsoft.com/visualstudio/whats-a-pkgdef-and-why/)
