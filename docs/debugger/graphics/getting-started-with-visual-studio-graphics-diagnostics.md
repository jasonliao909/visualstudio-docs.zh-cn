---
title: 图形诊断入门 | Microsoft Docs
description: 准备首次使用图形诊断，然后从 Direct3D 应用捕获帧并在图形分析器中检查它们。
ms.date: 02/22/2022
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: bc06149e7a8ffbec78f5d11f150823be68a1a384
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139551074"
---
# <a name="getting-started-with-visual-studio-graphics-diagnostics"></a>Visual Studio 图形诊断入门
在此部分中，你会准备首次使用图形诊断，然后从 Direct3D 应用捕获帧并在图形分析器中检查它们。

## <a name="requirements"></a>要求
 若要使用 Visual Studio 中的图形诊断，必须使用 Visual Studio Enterprise、Visual Studio Professional 或 Visual Studio Community。  包括 Visual Studio Code 在内的其他版本均不包含此功能。

 [!INCLUDE[downloadvs](../includes/downloadvs_md.md)]

### <a name="windows-prerequisites"></a>Windows 先决条件

 可选的Windows *图形* 工具"功能提供了在 图形诊断 及更高版本上Windows 10和播放基础结构。

 有关安装图形工具的信息，请参阅安装图形[工具Windows 10及更高版本](#InstallGraphicsTools)。

## <a name="install-graphics-tools-for-windows-10-and-later"></a><a name="InstallGraphicsTools"></a>安装图形工具Windows 10及更高版本

 在 Windows 10 及更高版本中，图形诊断基础结构由名为"图形工具"的 Windows *功能提供*。 无论捕获的应用是面向以前版本的窗口还是它使用的 Direct3D 版本，都需要此功能来捕获和播放 Windows 10 及更高版本上的图形信息。 可以选择提前安装图形工具功能；否则它会在你首次从 Visual Studio 启动图形诊断会话时按需安装。

#### <a name="to-install-graphics-tools-for-windows-10-and-later"></a>安装图形工具Windows 10及更高版本

1. 在“搜索”中，键入“应用和功能”，然后打开“应用和功能”设置。

2. 选择 **"可选功能"**。

   在Windows 10"应用""应用功能"设置的右侧&**可选** 功能。 选择 **"可选功能"**。

   在Windows 11，你将在"应用"设置中查找可选功能，而不是"**应用**"&功能。 选择 **"应用**"，然后选择" **可选功能"**。

   此时将显示“可选功能”设置。

3. 在“可选功能”设置中，选择“添加功能”。 可以安装的可选功能列表随即出现。

4. 从功能列表中选择“图形工具”，然后选择“安装” 。

   在安装 Windows 10 或 Windows 11 SDK 时，也会自动安装图形工具功能。

> [!TIP]
> Windows 10 及更高版本的可选图形工具功能提供轻型捕获和播放功能（如命令行捕获程序 **dxcap.exe）** 可用于未安装开发人员工具的计算机的支持、测试和诊断方案。 有关详细信息，请参阅[命令行捕获工具](command-line-capture-tool.md)主题。

## <a name="using-graphics-diagnostics-for-the-first-time"></a>首次使用图形诊断

 现在你拥有所有所需内容，已准备好开始使用图形诊断。 请执行这些步骤。

### <a name="1---create-a-direct3d-app"></a>1 - 创建 Direct3D 应用

如果你已经拥有自己的 Direct3D 应用，可以用来探索图形诊断，那就再好不过了！ 如果没有，可以使用以下项之一：

::: moniker range=">=vs-2019"
从 [Direct3D 游戏示例](/samples/microsoft/windows-universal-samples/simple3dgamedx/)下载示例。
::: moniker-end
::: moniker range="vs-2017"
- **DirectX 11 应用 (通用** Windows) 或 **DirectX 12 应用 (适用于** Windows) 或更高版本的通用 Windows 10 模板。
- 适用于 Windows 10 或更高版本的 [Direct3D 12 UAP](https://code.msdn.microsoft.com/Direct3D-12-UAP-Sample-ecb1779f) 示例。
::: moniker-end

在继续之前，请确保你可以生成和运行应用。 依次选择“生成” > “生成解决方案”，以确保它在生成时不会出错。 然后，依次选择“调试” > “在不调试的情况下启动”(Ctrl+F5)，以确保它能正常运行。 根据要用此工具测试的计算机，可能需要调整示例的平台和调试目标。 例如，若要在 Visual Studio 主机上对 x64 平台进行测试，请选择“x64”作为解决方案平台，并选择“本地计算机”作为调试目标。 

### <a name="2---start-a-graphics-diagnostics-session"></a>2 - 启动图形诊断会话
 现在你已准备好启动第一个图形诊断会话。 在 Visual Studio 中的主菜单上，依次选择“调试”、“图形”、“启动图形诊断”，或只需按 Alt+F5 。 这会在图形诊断下启动你的应用并在 Visual Studio 中显示诊断会话窗口。

> [!IMPORTANT]
> 如果在或更高版本上运行应用Windows 10尚未安装可选的图形工具功能，则系统会提示你立即安装。 必须先安装它，然后才能使用图形诊断。

### <a name="3---capture-frames"></a>3 - 捕获帧
 只要应用启动，你便已准备好捕获帧。

#### <a name="to-capture-single-frames"></a>捕获单个帧

- 在 Visual Studio 中，从图形工具栏或诊断会话窗口选择“捕获帧”按钮。 或者，如果你的应用具有焦点，则只需按键盘上的 Print Screen 键即可。

#### <a name="to-capture-a-sequence-of-frames"></a>捕获帧序列

- 在 Visual Studio 的诊断会话窗口中，将“要捕获的帧数”设置为要按顺序捕获的帧数，然后使用上述任何捕获单个帧的方法来捕获序列。

   若要再次捕获单个帧，请将“要捕获的帧数”设置为“1”。

  捕获帧完成时，只需退出应用，或从图形工具栏或诊断会话窗口选择“停止”按钮。

### <a name="4---examine-captured-frames-in-the-graphics-analyzer"></a>4 - 在图形分析器中检查捕获的帧
 现在你已准备好检查刚捕获的帧。 若要开始分析帧，请从诊断会话窗口选择要检查的帧的帧号码。 这会在“图形分析器”中打开该帧，在其中可以使用图形诊断工具检查应用如何使用 Direct3D 来跟踪呈现问题，或使用“帧分析”工具来了解其性能 。

 如果从诊断会话窗口选择了错误的帧，或者要检查不同的帧，则可以从图形分析器选择一个新帧。 在图形日志窗口的“呈现目标”选项卡上，在呈现目标图像下展开“帧列表”，然后选择不同的帧进行检查 。

 若要了解有关如何结合使用图形分析器工具的详细信息，请参阅[示例](graphics-diagnostics-examples.md)。

## <a name="see-also"></a>请参阅
- [Direct3D 12 图形](/windows/desktop/direct3d12/direct3d-12-graphics)