---
title: ARM 支持的设备上的 Visual Studio
description: 在具有基于 ARM 的处理器的设备上使用 Visual Studio 的建议。
ms.date: 03/09/2022
ms.topic: conceptual
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: d09420f80aa6b4e7cccbf9c0595f99790b74250f
ms.sourcegitcommit: b0ec2d8b7e32a9a6b50e462d588c64d471665533
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/10/2022
ms.locfileid: "139703994"
---
# <a name="visual-studio-on-arm-powered-devices"></a>ARM 支持的设备上的 Visual Studio

::: moniker range="vs-2019"

Visual Studio 生成为基于 x86 体系结构匹配处理器，并且没有适用于基于 ARM 的处理器的 Visual Studio 版本。

Visual Studio 可以通过 x86 仿真在支持 arm 的设备上运行，但 arm 上当前不支持某些功能。 因此，建议不要在使用基于 ARM 的处理器的设备上运行 Visual Studio，而是建议使用远程目标 ARM 设备。

有关支持的操作系统、硬件、支持的语言以及其他要求和指导，请参阅[Visual Studio 2019 系统要求](/visualstudio/releases/2019/system-requirements)。

::: moniker-end

::: moniker range="vs-2022"

Visual Studio 构建为基于 x64 体系结构的处理器，并且没有用于基于 ARM 的处理器的 Visual Studio 版本。

Visual Studio 可以通过 x64 模拟在支持 arm 的设备上运行，但 arm 上当前不支持某些功能。 因此，建议不要在使用基于 ARM 的处理器的设备上运行 Visual Studio，而是建议使用远程目标 ARM 设备。

有关支持的操作系统、硬件、支持的语言以及其他要求和指导，请参阅[Visual Studio 2022 系统要求](/visualstudio/releases/2022/system-requirements)。

::: moniker-end

## <a name="remote-targeting-arm-devices"></a>远程目标 ARM 设备

::: moniker range="vs-2019"

为了获得最佳体验，我们建议你在 x86 支持的单独计算机上使用 Visual Studio，并使用 Visual Studio 中的远程部署和调试功能以匹配基于 ARM 的设备。 若要调试设备上已安装的 Windows 通用应用程序，请参阅[调试安装的应用包](../debugger/debug-installed-app-package.md)文档。 若要部署新应用，请参阅[远程运行 Windows 应用商店应用](../debugger/run-windows-store-apps-on-a-remote-machine.md)。 对于所有其他应用程序类型，请参阅[远程调试](../debugger/remote-debugging.md)文档。

::: moniker-end

::: moniker range="vs-2022"

为了获得最佳体验，我们建议你在单独的、x64 支持的计算机上使用 Visual Studio，并使用 Visual Studio 中的远程部署和调试功能来面向基于 ARM 的设备。 若要调试设备上已安装的 Windows 通用应用程序，请参阅[调试安装的应用包](../debugger/debug-installed-app-package.md)文档。 若要部署新应用，请参阅[远程运行 Windows 应用商店应用](../debugger/run-windows-store-apps-on-a-remote-machine.md)。 对于所有其他应用程序类型，请参阅[远程调试](../debugger/remote-debugging.md)文档。

::: moniker-end

## <a name="tips-for-running-visual-studio-on-arm-devices"></a>在 ARM 设备上运行 Visual Studio 的提示

### <a name="use-only-when-needed"></a>仅在需要时使用

::: moniker range="vs-2019"

可以使用 x86 仿真在 ARM 处理器上运行 Visual Studio。 请注意，在对基于 ARM 的处理器使用模拟时，某些功能可能在此仿真中不受支持，并且性能可能会降低。 你可能会考虑以远程方式定向到 ARM 设备。

::: moniker-end

::: moniker range="vs-2022"

可以使用 x64 模拟在 ARM 处理器上运行 Visual Studio。 请注意，在对基于 ARM 的处理器使用模拟时，某些功能可能在此仿真中不受支持，并且性能可能会降低。 你可能会考虑以远程方式定向到 ARM 设备。

::: moniker-end

### <a name="install-time"></a>安装时间
计划 Visual Studio 需要更长的时间来安装，并希望暂停一段时间，或需要重新启动。
 
### <a name="remote-tools"></a>远程工具
若要调试在远程设备上运行的应用，将需要为 ARM [下载和安装远程工具](../debugger/remote-debugging.md#download-and-install-the-remote-tools)。

### <a name="start-debugging-f5"></a>启动调试 (F5)
并非所有 Visual Studio 项目都配置为从 ARM 设备开始调试 (F5) 时在本地启动项目。 即使你的应用在本地运行，也可能需要配置 Visual Studio 以进行远程调试。 有关详细信息，请参阅[远程调试](../debugger/remote-debugging.md)。

## <a name="we-need-your-help"></a>我们需要你的帮助！
如果希望 Visual Studio 在 ARM 设备上以本机方式运行，我们非常期待得到所需的方案和支持。 可以通过在[开发者社区](https://developercommunity.visualstudio.com/idea/1161018/native-arm-support-for-visual-studio.html)上发布来联系我们。
