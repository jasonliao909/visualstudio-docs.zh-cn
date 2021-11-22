---
title: 排查 XAML 热重载问题
description: 修复在使用 XAML 热重载时可能遇到的问题。
ms.date: 09/04/2019
ms.topic: troubleshooting
helpviewer_keywords:
- xaml edit and continue, troubleshooting
- xaml hot reload, troubleshooting
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-xaml-tools
ms.workload:
- multiple
ms.openlocfilehash: 0c90e8009540ad42c6efb6734c2ca034f4180a4e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666962"
---
# <a name="troubleshooting-xaml-hot-reload"></a>排查 XAML 热重载问题

本故障排除指南包含详细说明，这些说明应解决大多数妨碍 XAML 热重载正常运行的问题。

WPF 和 UWP 应用支持 XAML 热重载。 有关操作系统和工具要求的详细信息，请参阅[使用 XAML 热重载编写和调试正在运行的 XAML 代码](xaml-hot-reload.md)。

## <a name="hot-reload-is-not-available"></a>热重载不可用

如果在调试应用时在应用内工具栏中看到“热重载不可用”消息，请按照本文中所述的说明解决此问题。

## <a name="verify-that-xaml-hot-reload-is-enabled"></a>验证 XAML 热重载是否已启用

默认情况下启用此功能。 开始调试应用时，请确保看到应用内工具栏，它确认 XAML 热重载可用：

![XAML 热重载可用](../debugger/media/xaml-hot-reload-available.png)

如果看不到应用内工具栏，请打开“调试” > “选项” > “常规”。 确保选中“启用 XAML 的 UI 调试工具”和“启用 XAML 热重载”这两个选项。

![Visual Studio“调试选项”窗口的屏幕截图。 选择常规调试选项并选中“启用 XAML 热重载”选项。](../debugger/media/xaml-hot-reload-enable.png)

如果选择了这些选项，则转至实时可视化树（“调试” > “Windows” > “实时可视化树”），并确保选择“在应用程序中显示运行时工具”工具栏按钮（最左侧）。

![“实时可视化树”窗口顶部的工具栏的屏幕截图，其中选择了“在应用程序中显示运行时工具”按钮。](../debugger/media/xaml-hot-reload-show-runtime-tools.png)

## <a name="verify-that-you-use-start-debugging-rather-than-attach-to-process"></a>验证是否使用“开始调试”而不是“附加到进程”

XAML 热重载要求在应用程序启动时将环境变量 `ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO` 设置为 1。 Visual Studio 会自动将此设置为“调试” > “开始调试”（或 F5）命令的一部分。 如果要改为使用“调试” > “附加到进程”命令使用 XAML 热重载，请自行设置环境变量。

> [!NOTE]
> 若要设置环境变量，请使用“开始”按钮搜索“环境变量”，然后选择“编辑系统环境变量”。 在打开的对话框中，选择“环境变量”，然后将其添加为用户变量，并将值设置为 `1`。 若要清理，请在完成调试后删除该变量。

## <a name="verify-that-your-msbuild-properties-are-correct"></a>验证 MSBuild 属性是否正确

默认情况下，源信息包含在调试配置中。 它由项目文件（例如 *.csproj）中的 MSBuild 属性控制。 对于 WPF，属性为 `XamlDebuggingInformation`，必须设置为 `True`。 对于 UWP，属性为 `DisableXbfLineInfo`，必须设置为 `False`。 例如：

WPF：

`<XamlDebuggingInformation>True</XamlDebuggingInformation>`

UWP：

`<DisableXbfLineInfo>False</DisableXbfLineInfo>`

## <a name="verify-that-you-are-using-the-correct-build-configuration-name"></a>验证是否使用了正确的生成配置名称

必须手动设置正确的 MSBuild 属性以支持XAML 热重载（请参阅上一部分），或者必须使用默认生成配置名称（调试）。 如果未正确设置 MSBuild 属性，则自定义生成配置名称将不起作用，发布生成也将不起作用。

## <a name="verify-that-your-xaml-file-has-no-errors"></a>验证 XAML 文件是否没有错误

如果 XAML 文件在“错误列表”中显示错误，则 XAML 热重载可能无法工作。

## <a name="see-also"></a>另请参阅

[使用 XAML 热重载编写和调试正在运行的 XAML 代码](xaml-hot-reload.md)
