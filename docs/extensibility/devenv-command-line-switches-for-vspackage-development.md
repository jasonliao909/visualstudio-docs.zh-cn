---
title: 用于 VSPackage 开发的 Devenv Command-Line 开关 |Microsoft Docs
description: 了解开发人员如何通过命令行自动执行任务，devenv.exe，启动 Visual Studio IDE 的文件。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- /Setup command line switch
- /ResetSkipPkgs command line switch
- /RootSuffix command line switch
- /SafeMode command line switch
- /Splash command line switch
- command-line switches
- registry, Visual Studio SDK
- command line, switches
- Visual Studio SDK, command-line switches
ms.assetid: d65d2c04-dd84-42b0-b956-555b11f5a645
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 432aee15e77845308aad7c87284f43f3118c81f20d2bd5ce4c0c745a2b0f344b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338067"
---
# <a name="devenv-command-line-switches-for-vspackage-development"></a>Devenv 命令行开关，适用于 VSPackage 开发

Visual Studio 允许开发人员在执行时从命令行自动执行任务 `devenv.exe` ，这是启动 Visual Studio IDE 的文件。

 任务包括：

- 从 IDE 外部部署预先设计的配置中的应用程序。

- 使用预设生成设置或调试配置自动生成项目。

- 将 IDE 加载到 IDE 外部的特定配置。 你还可以在启动时自定义 IDE。

## <a name="guidelines-for-switches"></a>开关指南

Visual Studio 文档介绍用户级 `devenv` 命令行开关。 有关详细信息，请参阅 [Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)。 该 `devenv` 工具还支持可用于 VSPackage 开发、部署和调试的其他命令行开关。

| 命令行开关 | 说明 |
|---------------------| - |
| `/ResetSkipPkgs` | 清除所有要避免加载有问题的 Vspackage 的用户添加的 "跳过加载" 选项，然后 Visual Studio 开始。 如果存在 SkipLoading 标记，则会禁用 VSPackage 的加载。 清除标记会重新启用 VSPackage 的加载。<br /><br /> 此开关不带参数。 |
| `/RootSuffix` | 使用备用位置启动 Visual Studio。 Visual Studio SDK 安装程序创建的快捷方式将运行以下命令：<br /><br /> `devenv /RootSuffix exp`<br /><br /> 在这种情况下， `exp` 使用特定后缀标识一个位置 (例如， `10.0Exp` 而不是 `10.0`) 。 实验实例允许您从用于编写代码的 Visual Studio 实例中单独调试 VSPackage。<br /><br /> 此开关可以采用标识您使用 VSRegEx.exe 创建的位置的任何字符串。 有关详细信息，请参阅 [实验实例](../extensibility/the-experimental-instance.md)。 |
| `/SafeMode` | 在安全模式下启动 Visual Studio，仅加载默认 IDE 和服务。 该 `/SafeMode` 开关可防止在 Visual Studio 启动时加载所有第三方 vspackage，从而确保执行稳定。<br /><br /> 此开关不带参数。 |
| `/Setup` | 强制 Visual Studio 合并从所有可用的 vspackage 中描述菜单、工具栏和命令组的资源元数据。 只能以管理员身份运行此命令。 <br /><br /> 此开关不带参数。 `devenv /Setup` 命令通常作为安装过程的最后一步给出。 使用 `/Setup` 开关不会启动 IDE。|
| `/Splash` | 照常显示 Visual Studio 初始屏幕，然后在显示主 IDE 之前显示消息框。 使用消息框可以查看初始屏幕 (例如，查找) 的 VSPackage 产品图标。<br /><br /> 此开关不带参数。 |

## <a name="see-also"></a>另请参阅

- [添加命令行开关](../extensibility/adding-command-line-switches.md)
- [Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)
