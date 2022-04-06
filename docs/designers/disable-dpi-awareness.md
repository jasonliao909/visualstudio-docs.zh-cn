---
title: 禁用 DPI 感知，以在窗体中进行缩放
description: 解决 HDPI 监视器上 Windows 窗体设计器的缩放问题。
ms.date: 04/10/2022
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-designers
ms.topic: how-to
ms.custon: contperf-fy22q2
ms.openlocfilehash: 0720c23c74eeb477da82cb69bbeeb5f9a44a06c3
ms.sourcegitcommit: d9cab667735450e735622f8b93266f07b8046f3e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2022
ms.locfileid: "141402201"
---
# <a name="disable-dpi-awareness-to-fix-hdpi--scaling-issues-with-windows-forms-designer-in-visual-studio"></a>禁用 DPI 感知以修复 Visual Studio 中Windows 窗体设计器的 HDPI/缩放问题

在本文中，你将了解 HDPI 监视器上Windows 窗体设计器的限制，[以及如何以 DPI-unaware 过程的形式运行Visual Studio](#resolve-hdpi-display-problems)。

Visual Studio 是一个每英寸点数 (DPI) 感知应用程序，因此其显示可以自动缩放。 如果某个应用程序声明自己是非 DPI 感知应用程序，则操作系统作将该应用程序作为位图缩放。 此行为也称为 DPI 虚拟化。 应用程序仍会认为它以 100% 缩放比例（即 96 dpi）运行。

也可执行以下操作：
+ [在 Windows 窗体中自动缩放](/dotnet/framework/winforms/automatic-scaling-in-windows-forms)
+ 选择“[使用不同像素密度优化屏幕呈现(需要重启)](../ide/reference/general-environment-options-dialog-box.md#visual-experience)”选项

## <a name="scaling-issues-in-windows-forms-designer-on-hdpi-monitors"></a>在 HDPI 监视器上Windows 窗体设计器中缩放问题

由于 Visual Studio 中的 **Windows 窗体设计器** 没有缩放支持，因此在 HDPI) 监视器 (高点上打开某些窗体时，可能会出现显示问题。 例如，控件可能显示为重叠，如下图所示：

![HDPI 监视器上的 Windows 窗体设计器](./media/win-forms-designer-hdpi-1.gif)

如果不在设计器中工作，并且无需调整窗体的布局，可以忽略该信息栏，在代码编辑器或其他类型的设计器中继续工作。 （还可以[禁用通知](#disable-notifications)，以便信息栏不会继续显示。）只有 Windows 窗体设计器才会受到影响  。

在 HDPI 监视器上的 **Windows 窗体设计器** 中打开窗体时，Visual Studio显示信息栏。

::: moniker range=">=vs-2019"

:::image type="content" source="media/scaling-gold-bar-message-1.png" alt-text="Visual Studio中以 DPI-unaware 模式重启的信息栏的屏幕截图。":::

::: moniker-end

::: moniker range="vs-2017"
消息为“主显示器上的缩放比例设置为 200% (192 dpi)。  这可能会导致设计器窗口中出现呈现问题”。

![Visual Studio 2017 中信息栏以 DPI-unaware 模式重启的屏幕截图。](./media/scaling-gold-bar.png)

> [!NOTE]
> 此信息栏是在 Visual Studio 2017 版本 15.8 中引入的。

::: moniker-end


> [!TIP]
> 如果已关闭设计器顶部的信息栏，但仍希望复制显示 **"重启"Visual Studio且缩放为 100%** 的链接的行为，仍可以。 从Visual Studio菜单栏中选择 **ToolsCommand** >  **LineDeveloper** >  命令提示符。 然后，输入 `devenv /noScale`。


## <a name="resolve-hdpi-display-problems"></a>解决 HDPI 显示问题

有三个选项可解决显示问题：

- [以非 DPI 感知进程的形式重启 Visual Studio](#restart-visual-studio-as-a-dpi-unaware-process)
- [添加注册表项](#add-a-registry-entry)
- [将显示缩放比例设置为 100%](#set-your-display-scaling-setting-to-100)

> [!TIP]
> 如果更希望通过命令行管理设置，可使用 [`devenv.exe`](../ide/reference/devenv-command-line-switches.md) 将 `/noscale` 作为命令行参数，在 100% 缩放模式下运行。

### <a name="restart-visual-studio-as-a-dpi-unaware-process"></a>以非 DPI 感知进程的形式重启 Visual Studio

此问题的首选解决方案是重启Visual Studio作为 DPI-unaware 进程。 为此，请选择黄色信息栏上的选项。 

当Visual Studio作为 DPI-unaware 进程运行时，设计器布局问题会得到解决，但字体可能会模糊，并且你可能会在其他设计器（如 **XAML 设计器**）中看到问题。 以非 DPI 感知进程的形式运行 Visual Studio 时，Visual Studio 将显示另一条黄色信息性消息，表示“Visual Studio 正在以非 DPI 感知进程的形式运行。  WPF 和 XAML 设计器可能无法正确显示。” 此信息栏还提供了一个选项，“以非 DPI 感知进程的形式重启 Visual Studio”  。

> [!NOTE]
> - 选择以非 DPI 感知进程的形式重启 Visual Studio 的选项时，如果 Visual Studio 中有未停靠的工具窗口，则这些工具窗口的位置可能会发生更改。
> - 如果使用默认的 Visual Basic 配置文件，或者在“工具” > “选项” > “项目和解决方案”中取消选择了“创建时保存新项目”选项，则 Visual Studio 以非 DPI 感知进程的形式重启时无法重新打开该项目     。 但是，可以通过在“文件” > “最近使用的项目和解决方案”下选择该项目将其打开   。

在 Windows 窗体设计器中完成操作后，必须以 DPI 感知进程的形式重启 Visual Studio  。 如果在 Visual Studio 以非 DPI 感知模式运行时，将其关闭并重新打开，它会再次变为 DPI 感知。 还可以在信息栏中选择“以 DPI 感知进程的形式重启 Visual Studio”选项。

### <a name="add-a-registry-entry"></a>添加注册表项

作为选项 2，可以通过修改注册表将Visual Studio标记为 DPI-unaware。 打开注册表编辑器并向 HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Layers 子项添加项   ：

条目：根据所使用的是 Visual Studio 2017、2019 还是 2022，请使用以下值之一：

- C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE\devenv.exe
- C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\IDE\devenv.exe
- C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\devenv.exe

> [!NOTE]
> 如果你正在使用 Visual Studio Professional 或 Enterprise Edition，请将该项中的“Community”替换为“Professional”或“Enterprise”    。 还可根据需要替换驱动器号。

**类型**：REG_SZ <br>
**值**：DPIUNAWARE

在删除注册表项之前，Visual Studio 将保持非 DPI 感知模式。

### <a name="set-your-display-scaling-setting-to-100"></a>将显示缩放比例设置为 100%

解决问题的第三个选项是在Windows 10中将显示缩放设置设置为 100%，在任务栏搜索框中键入 **显示设置**，然后选择"**更改显示设置**"。 在“设置”窗口中，将“更改文本、应用和其他项的大小”设置为“100%”    。  但是，将显示器缩放设置为 100% 可能是不可取的，因为它会使用户界面太小，无法使用。

## <a name="disable-notifications"></a>禁用通知

可以在 Visual Studio 中选择不接收 DPI 缩放问题的通知。 例如，如果不在设计器中工作，可能需要禁用通知。

若要禁用通知，请执行以下操作：
1. 选择“工具” > “选项”，打开“选项”对话框  。
2. 在 **"选项**"对话框中，选择 **Windows 窗体** **DesignerGeneral** > ，并将 **DPI 缩放通知** 设置为 **False**。

如果稍后要重新启用缩放通知，请将此属性设置为“True”  。

## <a name="troubleshoot"></a>疑难解答

如果 DPI 感知转换在 Visual Studio 中未按预期方式工作，请检查注册表编辑器中的 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\devenv.exe 子项中是否有 `dpiAwareness` 值  。 如果存在该值，请将其删除。
