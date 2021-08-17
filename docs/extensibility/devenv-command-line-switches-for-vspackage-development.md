---
title: 用于 VSPackage Command-Line的 Devenv |Microsoft Docs
description: 了解开发人员在执行启动 IDE 的 devenv.exe 时，如何从命令行Visual Studio任务。
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
# <a name="devenv-command-line-switches-for-vspackage-development"></a>用于 VSPackage 开发 Devenv 命令行开关

Visual Studio允许开发人员在执行 时从命令行自动执行任务，该文件将启动 Visual Studio `devenv.exe` IDE。

 任务包括：

- 从 IDE 外部部署采用预设计配置的应用程序。

- 使用预设的生成设置或调试配置自动生成项目。

- 以特定配置加载 IDE，所有配置均从 IDE 外部加载。 还可以在启动时自定义 IDE。

## <a name="guidelines-for-switches"></a>交换机指南

Visual Studio文档介绍了用户 `devenv` 级命令行开关。 有关详细信息，请参阅 [Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)。 `devenv`该工具还支持其他命令行开关，这些开关可用于 VSPackage 开发、部署和调试。

| 命令行开关 | 说明 |
|---------------------| - |
| `/ResetSkipPkgs` | 清除希望避免加载有问题的 VSPackage 的用户添加的所有跳过加载选项，然后Visual Studio。 存在 SkipLoading 标记会禁用 VSPackage 的加载。 清除 标记会重新启用 VSPackage 的加载。<br /><br /> 此开关不带参数。 |
| `/RootSuffix` | 使用Visual Studio位置开始运行。 以下命令由 Visual Studio SDK 安装程序创建的快捷方式运行：<br /><br /> `devenv /RootSuffix exp`<br /><br /> 在这种情况下， `exp` 标识具有特定后缀的位置 (例如 ，而不是 `10.0Exp` `10.0`) 。 通过实验实例，你可以独立于用于编写代码Visual Studio实例调试 VSPackage。<br /><br /> 此开关可以采用任何字符串，该字符串标识使用 VSRegEx.exe。 有关详细信息，请参阅 [实验实例](../extensibility/the-experimental-instance.md)。 |
| `/SafeMode` | 在Visual Studio模式下启动，仅加载默认 IDE 和服务。 开关 `/SafeMode` 可防止所有第三方 VSPackage 在启动时Visual Studio，从而确保稳定执行。<br /><br /> 此开关不带参数。 |
| `/Setup` | 强制Visual Studio合并描述所有可用 VSPackage 中的菜单、工具栏和命令组的资源元数据。 只能以管理员角色运行此命令。 <br /><br /> 此开关不带参数。 `devenv /Setup` 命令通常作为安装过程的最后一步给出。 使用 `/Setup` 开关不会启动 IDE。|
| `/Splash` | 像往常一Visual Studio显示初始屏幕，然后在显示主 IDE 之前显示消息框。 使用消息框可以研究初始屏幕 (例如，检查 VSPackage 产品图标) 。<br /><br /> 此开关不带参数。 |

## <a name="see-also"></a>请参阅

- [添加命令行开关](../extensibility/adding-command-line-switches.md)
- [Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)
