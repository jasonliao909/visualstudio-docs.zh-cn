---
title: Visual Studio 扩展程序 Per-Monitor 感知支持
titleSuffix: ''
description: 了解 Visual Studio 2019 中提供的每监视器感知的新扩展程序支持。
ms.date: 04/10/2019
helpviewer_keywords:
- Visual Studio, PMA, per-monitor-awareness, extenders, Windows Forms
- Per-Monitor Awareness support for extenders
author: rub8n
ms.author: rurios
manager: anthc
monikerRange: vs-2019
ms.topic: reference
dev_langs:
- CSharp
- CPP
ms.openlocfilehash: 90ec038e8f27407ba08633bacbb5576bee2a7883
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902041"
---
# <a name="per-monitor-awareness-support-for-visual-studio-extenders"></a>Visual Studio 扩展程序 Per-Monitor 感知支持

Visual Studio 2019 之前的版本将其 DPI 感知上下文设置为 "系统感知"，而不是根据监视 DPI 识别 (PMA) 。 在系统感知中运行会导致视觉体验下降 (例如，当 Visual Studio 必须跨具有不同缩放系数的监视器进行呈现，或在具有不同显示配置的计算机之间呈现时，) 模糊的视觉体验， (例如不同的 Windows 缩放) 。

Visual Studio 2019 的 DPI 感知上下文设置为 PMA，当环境支持它时，允许 Visual Studio 根据其托管位置（而不是单个系统定义的配置）的配置进行呈现。 最终转换为支持 PMA 模式的表面区域的始终清晰的 UI。

有关本文档中所述的条款和整体方案的详细信息，请参阅 [Windows 上的高 DPI 桌面应用程序开发](/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows) 文档。

## <a name="quickstart"></a>快速入门

- 确保 Visual Studio 在 PMA 模式下运行 (参阅 **启用 PMA**) 

- 验证扩展是否可在一组常见方案中正确工作 (参阅 **测试扩展 PMA 问题**) 

- 如果发现问题，可以使用本文档中所述的策略/建议来诊断并解决这些问题。 还需要将新的 [VisualStudio DpiAwareness](https://www.nuget.org/packages/Microsoft.VisualStudio.DpiAwareness/) NuGet 包添加到项目中，以访问所需的 api。

## <a name="enable-pma"></a>启用 PMA

若要在 Visual Studio 中启用 PMA，需要满足以下要求：

- Windows 10 2018 年4月更新 (v1803，RS4) 或更高版本
- .NET Framework 4.8 RTM 或更高版本
- 启用了 ["针对具有不同像素密度的屏幕优化呈现"](../../ide/reference/general-environment-options-dialog-box.md) 选项的 Visual Studio 2019

满足这些要求后，Visual Studio 将自动在整个过程中启用 PMA 模式。

> [!NOTE]
> Windows 窗体 Visual Studio 中的内容 (例如，仅当安装了 Visual Studio 2019 16.1 或更高版本时，属性浏览器) 才支持 PMA。

## <a name="test-your-extensions-for-pma-issues"></a>测试 PMA 问题的扩展

Visual Studio 正式支持 WPF、Windows 窗体、Win32 和 HTML/JS UI 框架。 将 Visual Studio 置于 PMA 模式下时，每个 UI 堆栈的行为会有所不同。 因此，无论 UI 框架如何，都建议执行测试通过，以确保所有 UI 都符合 PMA 模式。

建议你验证以下常见方案：

- 在应用程序运行时更改单个监视器环境的缩放比例。

  此方案有助于测试 UI 是否响应动态 Windows DPI 更改。

- 停靠/脱开便携式计算机，其中连接的监视器设置为主监视器，而连接的监视器在运行应用程序时具有不同的缩放比例。

  此方案有助于测试 UI 是否响应显示 DPI 更改，以及动态添加或删除的处理显示。

- 使多个监视器具有不同的缩放因子，并在它们之间移动应用程序。

  此方案有助于测试 UI 是否响应显示 DPI 更改
    
- 当本地计算机和远程计算机的主监视器具有不同的缩放系数时，远程处理到计算机中。

  此方案有助于测试 UI 是否响应动态 Windows DPI 更改。

对 UI 是否可能存在问题的一个良好的初步测试 *是：代码* 使用的是 VisualStudio、 *DpiHelper*、DpiHelper 还是 *VsUI：： CDpiHelper* 类。 这些旧的 DpiHelper 类仅支持系统 DPI 感知，在进程 PMA 时不会始终正常运行。

这些 DpiHelpers 的典型用法如下所示：

```cs
Point screenTopRight = logicalBounds.TopRight.LogicalToDeviceUnits();

POINT screenIntTopRight = new POINT
{
    x = (int)screenTopRIght.X,
    y = (int)screenTopRIght.Y
}

// Declared via P/Invoke
IntPtr monitor = MonitorFromPoint(screenIntTopRight, MONITOR_DEFAULTTONEARST);
```

在上面的示例中，表示窗口逻辑边界的矩形将转换为设备单位，以便可以将其传递给需要设备坐标才能返回准确监视器指针的本机方法 MonitorFromPoint。

### <a name="classes-of-issues"></a>问题类别
为 Visual Studio 启用 PMA 模式后，UI 可以通过多种常见方式复制问题。 大多数（如果不是全部）这些问题都可以在任何 Visual Studio 支持的 UI 框架中发生。 此外，当在混合模式 DPI 缩放方案中承载一段 UI 时也可能发生这些问题 (参阅 Windows [文档](/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows) 以了解详细) 。 

#### <a name="win32-window-creation"></a>Win32 窗口创建
使用 CreateWindow () 或 CreateWindowEx () 创建 windows 时，一种常见的模式是创建坐标 (0，0)  (主显示器的左上角，然后将其移至最终位置。 但这样做可能会导致窗口触发 DPI 更改的消息或事件，这可能重新触发其他 UI 消息或事件，并最终导致意外行为或呈现。

#### <a name="wpf-element-placement"></a>WPF 元素位置
当使用旧的 VisualStudio 移动 WPF 元素时，如果元素在非主 DPI 上，则不能正确计算左上角的坐标。

#### <a name="serialization-of-ui-element-sizes-or-positions"></a>UI 元素大小或位置的序列化
如果 "UI 大小" 或 "位置" (作为设备单位保存) 在不同于存储它的 DPI 上下文上还原，则会将其定位并且大小不正确。 发生这种情况是因为设备单位具有固有的 DPI 关系。

#### <a name="incorrect-scaling"></a>缩放不正确
在主 DPI 上创建的 UI 元素将正确缩放，但当移动到具有不同 DPI 的显示时，它们不会重新缩放，并且其内容太大或太小。

#### <a name="incorrect-bounding"></a>边界不正确
与缩放问题类似，UI 元素会在其主 DPI 上下文中正确计算其边界，但当移动到非主 DPI 时，它们不会正确计算新边界。 在这种情况下，与宿主 UI 相比，内容窗口太小或太大，这将导致空格或剪裁。

#### <a name="drag--drop"></a>拖 & drop
无论何时在混合模式 DPI 方案 (例如，在不同 DPI 识别模式下呈现的不同 UI 元素) ，拖放坐标都可能 miscalculated，导致最终放置位置最终出现错误。

#### <a name="out-of-process-ui"></a>进程外 UI
某些 UI 是在进程外创建的，如果创建外部进程的 DPI 感知模式与 Visual Studio 不同，这可能会导致出现前面的任何呈现问题。

#### <a name="windows-forms-controls-images-or-layouts-rendered-incorrectly"></a>错误呈现 Windows 窗体控件、图像或布局
并非所有 Windows 窗体内容都支持 PMA 模式。 因此，可能会出现使用不正确的布局或缩放的呈现问题。 在这种情况下，可能的解决方案是显式呈现 "系统感知" DpiAwarenessContext 中的 Windows 窗体内容 (请参阅将 [控件强制转换为特定的 DpiAwarenessContext](#force-a-control-into-a-specific-dpiawarenesscontext)) 。

#### <a name="windows-forms-controls-or-windows-not-displaying"></a>Windows 窗体控件或 windows 未显示
导致此问题的主要原因之一是，开发人员尝试将具有一个 DpiAwarenessContext 的控件或窗口与另一个 DpiAwarenessContext 的窗口进行重定。

下图显示了父级窗口中当前的 **默认** Windows 操作系统限制：

![正确的父级行为的屏幕截图](media/PMA-parenting-behavior.PNG)

> [!Note]
> 您可以通过设置线程宿主行为 (引用 [Dpi_Hosting_Behavior 枚举](/windows/desktop/api/windef/ne-windef-dpi_hosting_behavior)) 来更改此行为。

因此，如果在不受支持的模式之间设置父子关系，它将失败，并且可能无法按预期方式呈现控件或窗口。

### <a name="diagnose-issues"></a>诊断问题

标识与 PMA 相关的问题时，需要考虑以下几个因素： 

- UI 或 API 是否需要逻辑或设备值？
    - WPF UI 和 Api 通常使用逻辑值 (但并非始终使用) 
    - Win32 UI 和 Api 通常使用设备值

- 值来自何处？
    - 如果从其他 UI 或 API 接收值，则它将传递设备或逻辑值。
    - 如果从多个源接收值，它们是否全部使用/预期相同类型的值，或者是否需要混合和匹配转换？

- UI 常量是否正在使用中，什么是窗体？

- 线程是否在其接收的值的正确的 DPI 上下文中？

  启用混合 DPI 承载的更改通常应将代码路径放在正确的上下文中，但在主消息循环之外完成的工作可能会在错误的 DPI 上下文中执行。

- 是否跨越 DPI 上下文边界实现值？

  拖动 & drop 是坐标可跨 DPI 上下文的常见情况。 窗口尝试执行正确的操作，但在某些情况下，宿主 UI 可能需要执行转换工作以确保上下文边界匹配。

### <a name="pma-nuget-package"></a>PMA NuGet 包
可以在 [VisualStudio DpiAwareness](https://www.nuget.org/packages/Microsoft.VisualStudio.DpiAwareness/) NuGet 包中找到新的 DpiAwarness 库。

### <a name="recommended-tools"></a>建议的工具
以下工具可帮助调试 Visual Studio 支持的某些不同 UI 堆栈之间的 PMA 相关问题。

#### <a name="snoop"></a>Snoop
Snoop 是一个 XAML 调试工具，它具有内置 Visual Studio XAML 工具没有的额外功能。 此外，Snoop 无需主动调试 Visual Studio 即可查看和调整其 WPF UI。 Snoop 的两种主要方法可用于诊断 PMA 问题，用于验证逻辑放置坐标或大小边界，验证 UI 是否具有正确的 DPI。
 
#### <a name="visual-studio-xaml-tools"></a>Visual Studio XAML 工具
与 Snoop 一样，Visual Studio 中的 XAML 工具可帮助诊断 PMA 问题。 找到可能的原因后，你可以设置断点，并使用 "实时可视化树" 窗口以及 "调试窗口" 来检查 UI 边界和当前 DPI。

## <a name="strategies-for-fixing-pma-issues"></a>解决 PMA 问题的策略

### <a name="replace-dpihelper-calls"></a>替换 DpiHelper 调用

在大多数情况下，修复 PMA 模式下的 UI 问题，以将托管代码中的调用替换为旧的 *VisualStudio DpiHelper* *和 PlatformUI 类，同时调用* 新的 *。* DpiHelper 帮助程序类。 

```cs
// Remove this kind of use:
Point deviceTopLeft = new Point(window.Left, window.Top).LogicalToDeviceUnits();

// Replace with this use:
Point deviceTopLeft = window.LogicalToDevicePoint(new Point(window.Left, window.Top));
```

对于本机代码，它会将对新的 *VsUI：： CDpiHelper* 类的调用替换为对新的 *VsUI：： CDpiAwareness* 类的调用。 

```cpp
// Remove this kind of use:
int cx = VsUI::DpiHelper::LogicalToDeviceUnitsX(m_cxS);
int cy = VsUI::DpiHelper::LogicalToDeviceUnitsY(m_cyS);

// Replace with this use:
int cx = m_cxS;
int cy = m_cyS;
VsUI::CDpiAwareness::LogicalToDeviceUnitsX(m_hwnd, &cx);
VsUI::CDpiAwareness::LogicalToDeviceUnitsY(m_hwnd, &cy);
```

新的 DpiAwareness 和 CDpiAwareness 类提供与 DpiHelper 类相同的单位转换帮助程序，但需要额外的输入参数：用作转换操作参考的 UI 元素。 请务必注意，新的 DpiAwareness/CDpiAwareness 帮助程序中不存在图像缩放帮助程序，如果需要，应改为使用 [ImageService](../image-service-and-catalog.md) 。

托管 DpiAwareness 类提供了针对 WPF 视觉对象、Windows 窗体控件以及 Win32 Hwnd 和 HMONITORs 的帮助程序，同时以 IntPtrs) 的形式 (，而 native CDpiAwareness 类提供 HWND 和 HMONITOR 帮助程序。

### <a name="windows-forms-dialogs-windows-or-controls-displayed-in-the-wrong-dpiawarenesscontext"></a>Windows 窗体错误的 DpiAwarenessContext 中显示的对话框、窗口或控件
即使由于 Windows 默认行为) ，对具有不同 DpiAwarenessContexts (的窗口进行成功父级设置后，用户仍可能会看到缩放问题，因为不同 DpiAwarenessContexts 缩放方式不同。 因此，用户可能会看到 UI 上的对齐/模糊文本或图像问题。

解决方法是为应用程序的所有窗口和控件设置正确的 DpiAwarenessContext 范围。

### <a name="top-level-mixed-mode-tlmm-dialogs"></a>顶级混合模式 (TLMM) 对话框
创建顶级窗口（如模式对话框）时，请务必确保在创建窗口窗口之前线程的状态正确 (及其句柄) 状态。 可以使用本机 中的 CDpiScope 帮助程序或托管中的 DpiAwareness.EnterDpiScope 帮助程序将线程置于系统感知中。  (TLMM 通常应用于非 WPF 对话框/windows.) 

### <a name="child-level-mixed-mode-clmm"></a>CLMM (子级混合) 
默认情况下，如果创建时没有父级，则子窗口接收当前线程 DPI 感知上下文;如果使用父级创建，则接收父级的 DPI 感知上下文。 若要创建具有不同于其父级的 DPI 感知上下文的子级，可以将线程放入所需的 DPI 感知上下文。 然后，可以在没有父级的情况下创建子级，并手动重新父级到父窗口。

#### <a name="clmm-issues"></a>CLMM 问题
作为主消息传递循环或事件链的一部分发生的大多数 UI 计算工作都应已在正确的 DPI 感知上下文中运行。 但是，如果协调或大小调整计算在这些主要工作流之外进行 (例如，在空闲时间任务期间或在 UI 线程之外执行，则当前 DPI 感知上下文可能不正确，从而导致 UI 位置错误或大小调整错误问题。 将线程置于 UI 工作的正确状态通常可解决此问题。
 
#### <a name="opt-out-of-clmm"></a>选择退出 CLMM
如果正在迁移非 WPF 工具窗口以完全支持 PMA，则需要选择退出 CLMM。 为此，需要实现一个新接口：IVsDpiAware。

```cs
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
public interface IVsDpiAware
{
    [ComAliasName("Microsoft.VisualStudio.Shell.Interop.VSDPIMode")]
    uint Mode {get;}
}
```

```cpp
IVsDpiAware : public IUnknown
{
    public:
        HRRESULT STDMETHODCALLTYPE get_Mode(__RCP__out VSDPIMODE *dwMode);
};
```

对于托管语言，实现此接口的最佳位置是派生自 *Microsoft.VisualStudio.Shell.ToolWindowPane* 的同一类。 对于 C++，实现此接口的最佳位置是在从 vsshell.h 实现 *IVsWindowPane* 的同一个类中。

接口上的 Mode 属性返回的值是一个__VSDPIMODE (并强制转换到托管接口中的 uint) ：

```cs
enum __VSDPIMODE
{
    VSDM_Unaware    = 0x01,
    VSDM_System     = 0x02,
    VSDM_PerMonitor = 0x03,
}
```

- 不知道意味着工具窗口需要处理 96 DPI，Windows 将处理所有其他 DPI 的缩放。 导致内容略微模糊。
- 系统意味着工具窗口需要处理主显示器 DPI 的 DPI。 任何具有匹配 DPI 的显示器看起来都清晰明了，但如果 DPI 不同或在会话期间发生更改，Windows 将处理缩放，并且会稍微模糊一些。
- PerMonitor 表示工具窗口需要处理所有显示器上的所有 DPI，并且每当 DPI 发生更改时。

> [!NOTE]
> Visual Studio仅支持 PerMonitorV2 感知，因此 PerMonitor 枚举值将转换为 DPI_AWARENESS_CONTEXT_PER_MONITOR_AWARE_V2 的 Windows 值。

#### <a name="force-a-control-into-a-specific-dpiawarenesscontext"></a>将控件强制转换为特定的 DpiAwarenessContext

在 PMA 模式下运行时，未更新以支持 PMA 模式的旧 UI 可能Visual Studio进行细微调整。 此类修复之一涉及确保在正确的 DpiAwarenessContext 中创建 UI。 若要强制 UI 进入特定的 DpiAwarenessContext，可以使用以下代码输入 DPI 范围：

```cs
using (DpiAwareness.EnterDpiScope(DpiAwarenessContext.SystemAware))
{
    Form form = new MyForm();
    form.ShowDialog();
}
```

```cpp
void MyClass::ShowDialog()
{
    VsUI::CDpiScope dpiScope(DPI_AWARENESS_CONTEXT_SYSTEM_AWARE);
    HWND hwnd = ::CreateWindow(...);
}
```

> [!NOTE]
> 强制 DpiAwarenessContext 仅适用于非 WPF UI 和顶级 WPF 对话框。 创建要托管在工具窗口或设计器中的 WPF UI 时，只要内容插入到 WPF UI 树中，它就会转换为当前进程 DpiAwarenessContext。

## <a name="known-issues"></a>已知问题

### <a name="windows-forms"></a>Windows 窗体

为了针对新的混合模式方案进行优化，Windows 窗体更改了在未显式设置控件和窗口父级时创建控件和窗口的方式。 以前，没有显式父级的控件使用内部"停车窗口"作为所创建的控件或窗口的临时父级。 

在 .NET 4.8 之前，有一个"停车窗口"，该窗口在窗口创建时从当前线程 DPI 感知上下文获取其 DpiAwarenessContext。 当创建控件的句柄时，任何未父级的控件都会继承与"停车窗口"相同的 DpiAwarenessContext，并且应用程序开发人员将重新成为最终/预期的父级。 如果"停车窗口"的 DpiAwarenessContext 高于最终父窗口，这可能会导致基于计时的故障。

从 .NET 4.8 开始，遇到的每个 DpiAwarenessContext 现在都有一个"停车窗口"。 另一个主要区别是，创建控件时（而不是创建句柄时）缓存用于控件的 DpiAwarenessContext。 这意味着整体结束行为是相同的，但可以将过去基于计时的问题转变为一致的问题。 它还为应用程序开发人员提供了更具确定性的行为，以编写其 UI 代码并正确确定其范围。
