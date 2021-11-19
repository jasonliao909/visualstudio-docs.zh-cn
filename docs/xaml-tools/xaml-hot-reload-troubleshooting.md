---
title: 排查 XAML 热重载问题
description: 修复了在管理过程中可能会遇到XAML 热重载。
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

本故障排除指南包含详细说明，这些说明应解决大多数妨碍XAML 热重载正常运行的问题。

XAML 热重载 WPF 和 UWP 应用支持此应用。 有关操作系统和工具要求的详细信息，请参阅使用 XAML 热重载 [编写和调试运行 XAML 代码](xaml-hot-reload.md)。

## <a name="hot-reload-is-not-available"></a>热重载不可用

如果在调试应用时在应用内工具栏中看到消息"热重载不可用"，请按照本文中所述的说明解决此问题。

## <a name="verify-that-xaml-hot-reload-is-enabled"></a>验证XAML 热重载是否已启用

此功能默认启用。 开始调试应用时，请确保看到应用内工具栏，该工具栏XAML 热重载可用：

![XAML 热重载可用](../debugger/media/xaml-hot-reload-available.png)

如果看不到应用内工具栏，请打开"调试选项  >  **""常规**  >  **"。** 确保选中"为 **XAML** 启用 UI 调试工具"和" **启用** XAML 热重载选项。

!["调试Visual Studio窗口的屏幕截图。 选中"常规调试"选项，并选中"XAML 热重载"选项。](../debugger/media/xaml-hot-reload-enable.png)

如果选择了这些选项，请转到"实时可视化树" ("调试"Windows"实时可视化树  >    >  ) "，并确保选择最左侧 ("在应用程序工具栏中显示运行时工具") 。

!["实时可视化树"窗口顶部的工具栏的屏幕截图，其中选择了"在应用程序中显示运行时工具"按钮。](../debugger/media/xaml-hot-reload-show-runtime-tools.png)

## <a name="verify-that-you-use-start-debugging-rather-than-attach-to-process"></a>验证是否使用"开始调试"而不是"附加到进程"

XAML 热重载应用程序启动时，环境变量设置为 `ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO` 1。 Visual Studio"调试开始调试"命令或  >  **F5** (中自动) 设置。 如果要改为使用"调试XAML 热重载  >  **附加到进程"** 命令，请自己设置环境变量。

> [!NOTE]
> 若要设置环境变量，请使用 “开始”按钮搜索"环境变量"，然后选择"**编辑系统环境变量"。** 在打开的对话框中，选择" **环境变量**"，然后添加为用户变量，然后将值设置为 `1` 。 若要清理，请完成调试后删除 变量。

## <a name="verify-that-your-msbuild-properties-are-correct"></a>验证MSBuild属性是否正确

默认情况下，源信息包含在调试配置中。 它由项目MSBuild属性控制， (如 *.csproj) 。 对于 WPF，属性为 `XamlDebuggingInformation` ，必须设置为 `True` 。 对于 UWP，属性为 `DisableXbfLineInfo` ，必须设置为 `False` 。 例如：

WPF：

`<XamlDebuggingInformation>True</XamlDebuggingInformation>`

UWP：

`<DisableXbfLineInfo>False</DisableXbfLineInfo>`

## <a name="verify-that-you-are-using-the-correct-build-configuration-name"></a>验证是否使用了正确的生成配置名称

必须手动设置正确的 MSBuild 属性以支持XAML 热重载 (请参阅上一部分) ，或者必须使用默认生成配置名称 (调试) 。 如果未正确设置属性MSBuild，则自定义生成配置名称将不起作用，发布版本也不会工作。

## <a name="verify-that-your-xaml-file-has-no-errors"></a>验证 XAML 文件是否没有错误

如果 XAML 文件在错误列表中显示 **错误**，XAML 热重载可能无法工作。

## <a name="see-also"></a>另请参阅

[使用代码编写和调试正在运行的 XAML XAML 热重载](xaml-hot-reload.md)
