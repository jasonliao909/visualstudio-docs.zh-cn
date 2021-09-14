---
title: 定位Visual Studio |Microsoft Docs
description: 可以安装同一版本的数据库的多个Visual Studio。 了解如何使用 COM 查询 API 查找想要的实例。
ms.custom: SEO-VS-2020
ms.date: 08/21/2017
ms.topic: conceptual
helpviewer_keywords:
- deployment, VSIX
ms.assetid: 680c3b25-7901-4768-8363-6d1fcd1ea636
author: leslierichardson95
ms.author: lerich
ms.workload:
- vssdk
ms.openlocfilehash: cd0fcd294983d6a6567676f06703b4bd1dd376c4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664282"
---
# <a name="locate-visual-studio"></a>找到 Visual Studio

从 Visual Studio 2017 开始，可以安装同一版本甚至版本的多个实例。 当你想要在主开发计算机上预览新功能，同时保留以前的安装时，这非常有用。 由于这些更改，没有可用于查找实例的单一环境变量或注册表值。 相反，可以使用 COM [查询 API](/dotnet/api/microsoft.visualstudio.setup.configuration) 根据与扩展相关的条件查找实例。

这是一个快速、只读的 API，NuGet本机和托管代码可用的包。

| 代码 | 包 |
| ---- | --- |
| 本机 | https://nuget.org/packages/Microsoft.VisualStudio.Setup.Configuration.Native |
| 托管 | https://nuget.org/packages/Microsoft.VisualStudio.Setup.Configuration.Interop |

可以查找给定路径或当前进程的单个实例，或枚举所有实例。 请参阅[示例](https://github.com/Microsoft/vs-setup-samples)，了解如何查找Visual Studio。

## <a name="tools"></a>工具

若要Visual Studio环境、PowerShell 脚本、安装程序和其他方案中的一些工具，可以使用许多开源工具，也可以随自己的脚本一起重新分发。

| 项目 | 说明 |
| ------- | ----------- |
| [vswhere](https://github.com/Microsoft/vswhere) | 单文件本机可执行文件，用于查找满足发布或预发布、已安装的产品以及已安装的工作负荷等条件的实例。 还支持Visual Studio 2010 及更高版本，但返回的信息较少，Visual Studio 2017 及更高版本。 有关示例 [，](https://github.com/Microsoft/vswhere/wiki) 请参阅 wiki。 |
| [VSSetup cmdlet](https://github.com/Microsoft/vssetup.powershell) | PowerShell cmdlet 支持 2.0 及更高版本，这些 cmdlet 将丰富的信息作为对象返回，可用于根据与 _vswhere_ 相同的条件查找实例，并发现更多有关实例的属性。 有关示例 [，](https://github.com/Microsoft/vssetup.powershell/wiki) 请参阅 wiki。 |
| [VSIXBootstrapper](https://github.com/Microsoft/vsixbootstrapper) | 自动查找 _VSIXInstaller_ 并传递命令行以安装 **.vsix* 文件。 此功能在未直接支持查询 API 的安装程序中非常有用。 有关示例 [，](https://github.com/Microsoft/vsixbootstrapper/wiki) 请参阅 wiki。 |

## <a name="see-also"></a>另请参阅

* [对 2017 Visual Studio的更改](https://devblogs.microsoft.com/setup/changes-to-visual-studio-15-setup/)
* [使用 DTE 启动 Visual Studio](launch-visual-studio-dte.md)
