---
title: 使用 Visual Studio Tools for Unity | Microsoft Docs
description: 了解如何使用 Visual Studio Tools for Unity 的集成和工作效率功能。 还可使用 Visual Studio 调试器进行 Unity 开发。
ms.date: 07/03/2018
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: how-to
ms.assetid: e67ec9a2-a449-413e-8930-9a471bd43a06
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
zone_pivot_groups: platform
ms.openlocfilehash: 08ad9bb1161b12ecc5cb588e3e37d0b9d318cacd
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129967686"
---
# <a name="use-visual-studio-tools-for-unity"></a>使用 Visual Studio Tools for Unity

在本部分中，你将了解如何使用 Visual Studio Tools for Unity 的集成和工作效率功能，以及如何使用 Visual Studio 调试器进行 Unity 开发。

## <a name="open-unity-scripts-in-visual-studio"></a>在 Visual Studio 中打开 Unity 脚本

将 Visual Studio [设置为 Unity 的外部编辑器](getting-started-with-visual-studio-tools-for-unity.md#configure-unity-to-use-visual-studio)后，在 Unity 编辑器中双击任何脚本都会自动启动或切换到 Visual Studio，并打开选择的脚本。

或者，可以通过在 Unity 中选择“资产”>“打开 C# 项目”菜单打开 Visual Studio，而无需在源编辑器中打开任何脚本。

:::zone pivot="windows"
![在 Visual Studio 中打开 C# 项目](../media/vs/vstu-open-csharp-project.png)
:::zone-end
:::zone pivot="macos"
![在 Visual Studio for Mac 中打开 C# 项目](../media/vsm/vstu-open-csharp-project.png)
:::zone-end

## <a name="unity-documentation-access"></a>Unity 文档访问

可以从 Visual Studio 快速访问 Unity 脚本文档。 如果 Visual Studio Tools for Unity 未在本地找到 API 文档，它将尝试联机查找。

:::zone pivot="windows"
- 在 Visual Studio 中，将需要了解的 Unity API 突出显示或将光标置于其上，然后按 Ctrl+Alt+M、Ctrl+H    
- 还可使用“帮助”>“Unity API 参考”菜单，而不是键绑定。
![Visual Studio 中的 Unity API 参考菜单](../media/vs/help-unity-documentation.png)
:::zone-end
:::zone pivot="macos"
- 在 Visual Studio for Mac 中，突出显示或将光标放在要了解的 Unity API 上，然后按 Cmd+' 
- 还可使用“帮助”>“Unity API 参考”菜单，而不是键绑定。
![Visual Studio for Mac 中的 Unity API 参考菜单](../media/vsm/help-unity-documentation.png)
:::zone-end

## <a name="intellisense-for-unity-api-messages"></a>针对 Unity API 消息的 Intellisense

Intellisense 代码完成简化了在 MonoBehaviour 脚本中实现 Unity API 消息，并有助于学习 Unity API。 对 Unity 消息使用 IntelliSense：

1. 将光标置于类主体内的新行上，该类派生自 `MonoBehaviour`。

2. 开始键入 Unity 消息的名称，如 `OnTriggerEnter`。

3. 键入字母“ontri”后，将显示 IntelliSense 建议列表。

:::zone pivot="windows"

![使用 Visual Studio IntelliSense](../media/vs/intellisense-example.png)  

:::zone-end

4. 可通过以下三种方式更改列表中的选择：

    - 使用向上键和向下键   。

    - 使用鼠标单击所需项。

    - 继续键入所需项的名称。

5. IntelliSense 可插入所选 Unity 消息，包括任何必需的参数：

    - 通过按 Tab。

    - 通过按 Enter。

    - 通过双击所选项。

:::zone pivot="windows"

![在 Visual Studio 中插入来自 IntelliSense 的 Unity 消息](../media/vs/vstu-intellisense2.png)

:::zone-end

## <a name="unity-monobehavior-scripting-wizard"></a>Unity MonoBehavior 脚本向导

MonoBehavior 向导可用于查看所有 Unity API 方法的列表，并快速实现空定义。 如果仍然想要了解 Unity API 中的可用功能，此功能将提供帮助，尤其是在启用了“生成方法注释”选项的情况下。

使用 MonoBehavior 向导创建 MonoBehavior 方法的空定义：

1. 在 Visual Studio 中，将光标放置在要插入方法的位置，然后按 Ctrl+Shift+M 启动 MonoBehavior 向导  。 在 Visual Studio for Mac 中，按 Cmd+Shift+M  。

2. 在“创建脚本方法”窗口中，标记每个要添加的方法的名称旁的复选框。

3. 使用“Framework 版本”下拉列表选择所需的版本。

4. 默认情况下，方法会插入到光标的位置。 或者，可以选择将它们插入到已在类中实现的任何方法后面，方法是将“插入点”下拉列表的值改为所需的位置。

5. 如果需要向导为所选方法生成注释，则标记“生成方法注释”复选框。 这些注释是为了帮助你了解方法的调用时间以及其常规责任。

6. 选择“确定”按钮退出向导，并将方法插入代码中。

:::zone pivot="windows"

![Visual Studio 中的 MonoBehavior 向导对话框。](../media/vs/vstu-monobehavior-wizard.png)
:::zone-end
:::zone pivot="macos"

![Visual Studio for Mac 中的 MonoBehavior 向导对话框。](../media/vsm/vstu-monobehavior-wizard.png)
:::zone-end   

## <a name="unity-project-explorer"></a>Unity 项目资源管理器
Unity 项目资源管理器会以与 Unity 编辑器相同的方式显示所有 Unity 项目文件和目录。 这是不同于使用普通 Visual Studio 解决方案资源管理器导航 Unity 脚本，后者将它们组织到项目和由 Visual Studio 生成的解决方案中。

:::zone pivot="windows"
- 在 Visual Studio 的主菜单上选择“视图”>“Unity 项目资源管理器”。 键盘快捷方式：Alt+Shift+E
  ![查看 Unity 项目资源管理器窗口。](../media/vs/unity-project-explorer.png)
:::zone-end
:::zone pivot="macos"
- 在 Visual Studio for Mac 中，当打开 Unity 项目时，Solution Pad 会自动表现如下。
:::zone-end
## <a name="unity-debugging"></a>Unity 调试

Visual Studio Tools for Unity 让你可以使用 Visual Studio 功能强大的调试器同时调试 Unity 项目的编辑器和游戏脚本。

### <a name="debug-in-the-unity-editor"></a>在 Unity 编辑器中调试

#### <a name="start-debugging"></a>“启动调试”
:::zone pivot="windows"

1. 若要将 Visual Studio 连接到 Unity，单击标记为“附加到 Unity”的“播放”按钮，或使用键盘快捷方式 F5。
![在 Visual Studio 中单击“播放”](../media/vs/vstu-play-button.png)

:::zone-end
:::zone pivot="macos"

1. 通过单击“Play”按钮、键入“Command + Return”或按“F5”将 Visual Studio 连接到 Unity    。
![在 Visual Studio for Mac 中单击“播放”](../media/vsm/using-vsmac-tools-unity-image5.png)

:::zone-end

2. 切换到 Unity 并单击“Play”按钮，在编辑器中运行游戏  。
:::zone pivot="windows"
![在 Windows 上的 Unity 中单击“播放”](../media/vs/vstu-unity-play-button.png)
:::zone-end
:::zone pivot="macos"
![在 macOS 上的 Unity 中单击“播放”](../media/vsm/using-vsmac-tools-unity-image6.png)
:::zone-end

3. 当游戏在连接到 Visual Studio 的情况下在 Unity 编辑器中运行时，遇到的任何断点都会中断游戏执行，并在 Visual Studio 中显示游戏遇到断点的代码行。

#### <a name="stop-debugging"></a>停止调试

:::zone pivot="windows"

单击 Visual Studio 中的“停止”按钮，或使用键盘快捷方式 Shift + F5。
![在 Visual Studio 中单击“停止”](../media/vs/vstu-stop-debugger.png)

:::zone-end
:::zone pivot="macos"

在 Visual Studio for Mac 中单击“停止”按钮，或按“Shift + Command + Return”。
![在 Visual Studio for Mac 中单击“停止”](../media/vsm/using-vsmac-tools-unity-image7.png)

:::zone-end

若要了解有关 Visual Studio 调试的详细信息，请参阅[首先看一下 Visual Studio 调试器](/visualstudio/debugger/debugger-feature-tour)。

#### <a name="attach-to-unity-and-play"></a>附加到 Unity 并播放

为方便起见，可以将“附加到 Unity”按钮改为“附加到 Unity 并播放”模式。

:::zone pivot="windows"

1. 单击“附加到 Unity”按钮旁边的小型向下箭头。
2. 从下拉菜单选择“附加到 Unity 并播放”。
   ![在 Visual Studio 中附加和播放](../media/vs/vstu-attach-and-play.png)

“播放”按钮标记将变为“附加到 Unity 并播放”。 单击此按钮或使用键盘快捷方式 F5，除了附加 Visual Studio 调试器，现在还会自动切换到 Unity 编辑器，并在编辑器中运行游戏。

:::zone-end
:::zone pivot="macos"
通过选择“附加到 Unity 并播放”配置，可通过一个步骤直接从 Visual Studio for Mac 完成启动调试和播放 Unity 编辑器。

![在 Visual Studio for Mac 中选择“附加到 Unity 并播放”](../media/vsm/using-vsmac-tools-unity-image8.png)
:::zone-end

> [!NOTE]
> 如果使用“附加到 Unity 并播放”配置启动调试，“停止”按钮也将停止 Unity 编辑器 。

### <a name="debug-unity-player-builds"></a>调试 Unity 播放器版本

可以在 Visual Studio 中调试 Unity 播放器的开发版本。

#### <a name="enable-script-debugging-in-a-unity-player"></a>在 Unity 播放器中启用脚本调试

1. 在 Unity 中，通过选择“文件”>“版本设置”打开“版本设置”。
2. 在“版本设置”窗口中，标记“开发版本”和“脚本调试”复选框。

   ![配置 Unity 生成设置以进行调试。](../media/vs/vstu-debugging-build-settings.png "vstu_debugging_build_settings")

#### <a name="select-a-unity-instance-to-attach-the-debugger-to"></a>选择要附加调试器的 Unity 实例

:::zone pivot="windows"

- 在 Visual Studio 的主菜单上选择“调试”>“附加 Unity 调试器”。

   ![附加 Unity 调试器。](../media/vs/vstu-debugging-attach-unity-debugger.png "vstu_debugging_attach_unity_debugger")

   “选择 Unity 实例”对话框将显示有关每个可以连接的 Unity 实例的信息。

   ![选择要连接的 Unity 实例。](../media/vs/vstu-attach-debugger.png "vstu_connection_to_unity")

   **Project**

   在此 Unity 实例中运行的 Unity 项目的名称。

   **Machine** 运行此 Unity 实例的计算机或设备的名称。

   **Type** 如果此 Unity 实例作为 Unity 编辑器的一部分运行，则为“编辑器”；如果此 Unity 实例是独立播放器，则为“播放器” 。

   **Port** 此 Unity 实例将用于通信的 UDP 套接字的端口号。

> [!IMPORTANT]
> 由于 Visual Studio Tools for Unity 和 Unity 实例正在通过 UDP 网络套接字进行通信，因而你的防火墙可能需要规则来允许它。 如果需要，你可能会看到一条提示，必须授权连接，以便 VSTU 和 Unity 可以进行通信。

:::zone-end
:::zone pivot="macos"

- 在 Visual Studio for Mac 的顶部菜单中，选择“运行”>“附加到进程”。 
- 在“附加到进程”对话框中，选择底部“调试器”下拉菜单中的“Unity 调试器”选项。
- 从列表中选择 Unity 实例，然后单击“附加”按钮。

:::zone-end

### <a name="debug-a-dll-in-your-unity-project"></a>调试 Unity 项目中的 DLL

许多 Unity 开发人员将代码组件编写为外部 Dll，以便可轻松地与其他项目共享开发的功能。 Visual Studio Tools for Unity 可以轻松无缝地调试这些 DLL 中的代码以及 Unity 项目中的其他代码。

> [!NOTE]
> Visual Studio Tools for Unity 此时仅支持托管 DLL。 它不支持调试本机代码 DLL，如使用 C++ 编写的代码。

请注意，此处所述的方案假定你具有源代码（即你正在开发或重用自己的第一方代码）或具有第三方库的源代码，并计划在 Unity 项目中将其作为 DLL 进行部署。 此方案未描述不具备源代码时的 DLL 调试。

#### <a name="to-debug-a-managed-dll-project-used-in-your-unity-project"></a>调试 Unity 项目中使用的托管 DLL 项目

1. 将现有的 DLL 项目添加到由 Visual Studio Tools for Unity 生成的 Visual Studio 解决方案中。 不太常见的情况是：你可能会启动一个新的托管 DLL 项目，以便在 Unity 项目中包含代码组件；如果是这种情况，则可将新的托管 DLL 项目添加到 Visual Studio 解决方案。

   ![将现有 DLL 项目添加到解决方案。](../media/vs/vstu-debugging-dll-add-existing.png "vstu_debugging_dll_add_existing")

   在任一情况下，Visual Studio Tools for Unity 均将维护项目引用，即使不得不再次重新生成项目和解决方案文件，所以你只需要执行一次这些步骤。

2. 引用 DLL 项目中正确的 Unity 框架配置文件。 在 Visual Studio 的 DLL 项目属性中，将“目标框架”属性设置为正在使用的 Unity 框架版本。 这是与你的项目作为目标的 API 兼容性相匹配的 Unity 基类库，如 Unity 完整、微型或 Web 基类库。 这可以防止你的 DLL 调用存在于其他框架或兼容性级别中而不存在于你正在使用的 Unity 框架版本中的框架方法。

> [!NOTE]
> 仅当使用 Unity 的旧版运行时的情况下，才需要使用以下配置文件。 如果使用的是新版 Unity 运行时，则无需再使用这些专用 3.5 配置文件。 使用与 Unity 版本兼容的 .NET 4.x 配置文件。

   ![将 DLL 的目标框架设置为 Unity 框架。](../media/vs/vstu-debugging-dll-target-framework.png "vstu_debugging_dll_target_framework")

3. 将 DLL 复制到 Unity 项目的资产文件夹。 在 Unity 中，资产是与 Unity 应用一起打包和部署的文件，所以可以在运行时加载它们。 由于 DLL 在运行时链接，因而必须将 DLL 作为资产部署。 若要部署为资产，Unity 编辑器需要将 DLL 放置在 Unity 项目的“资产”文件夹中。 可以采用两种方法执行此操作：

   - 修改 DLL 项目的生成设置，以包含将输出 DLL 和 PDB 文件从输出文件夹复制到 Unity 项目“资产”文件夹的生成后任务。

   - 修改 DLL 项目的生成设置，以将其输出文件夹设置为 Unity 项目的“资产”文件夹。 DLL 和 PDB 文件都将放置在“资产”文件夹中。

   需要调试 PDB 文件（因为它们包含 DLL 的调试符号），并将 DLL 代码映射到其源代码形式。 如果面向旧版运行时，Visual Studio Tools for Unity 将使用来自 DLL 和 PDB 的信息来创建一个 DLL.MDB 文件，此文件是旧版 Unity 脚本引擎所使用的调试符号格式。 如果面向新版运行时并使用可移植 PDB，Visual Studio Tools for Unity 将不会尝试执行任何符号转换，因为新版 Unity 运行时能够在本机使用可移植 PDB。

   有关 PDB 生成的详细信息，请访问[此处](/visualstudio/debugger/how-to-set-debug-and-release-configurations)。 如果面向新版运行时，请确保将“调试信息”设置为“可移植”，以便正确生成可移植 PDB。 如果面向旧版运行时，则需要使用“完整”。

4. 调试代码。 现在可以同时调试 DLL 源代码以及 Unity 项目的源代码，并使用所有熟悉的调试功能，如断点和单步调试代码。

## <a name="keyboard-shortcuts"></a>键盘快捷键

通过使用键盘快捷方式，可以快速访问 Unity Tools for Visual Studio 功能。 以下是可用快捷方式的摘要。

:::zone pivot="windows"

|命令|快捷键|快捷方式命令名|
|-------------|--------------|---------------------------|
|打开 Monobehavior 向导|Ctrl+Shift+M|**EditorContextMenus.CodeWindow.ImplementMonoBehaviours**|
|打开 Unity 项目资源管理器|Alt+Shift+E  |**View.UnityProjectExplorer**|
|访问 Unity 文档|Ctrl+Alt+M, Ctrl+H   |**Help.UnityAPIReference**|
|附加到 Unity 调试器（播放器或编辑器）|无默认值|**Debug.AttachUnityDebugger**|

如果不喜欢默认值，可以更改快捷键组合。 有关如何更改它的信息，请参阅[在 Visual Studio 中标识并自定义键盘快捷方式](/visualstudio/ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio)。

:::zone-end
:::zone pivot="macos"

|命令|快捷键|快捷方式命令名|
|-------------|--------------|---------------------------|
|打开 Monobehavior 向导|**Cmd**+**Shift**+**M**|**EditorContextMenus.CodeWindow.ImplementMonoBehaviours**|
|访问 Unity 文档|**Cmd+'**|**Help.UnityAPIReference**|

如果不喜欢默认值，可以更改快捷键组合。 有关如何更改它的信息，请参阅[自定义 IDE](/visualstudio/mac/customizing-the-ide#key-bingings)。

:::zone-end
