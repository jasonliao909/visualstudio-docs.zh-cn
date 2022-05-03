---
title: 在项目中包括 NuGet 包
description: 本文档介绍如何使用 Visual Studio for Mac 在项目中包含 NuGet 包。 它逐步讲解如何查找和下载包，并介绍 IDE 集成功能。
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 05/02/2022
ms.assetid: 5C800815-0B13-4B27-B017-95FCEF1A0EA2
ms.custom: conceptual, devdivchpfy22
ms.openlocfilehash: febd55d770efe53b63f0172803abcacd26d23e82
ms.sourcegitcommit: 3034382894e610b55f3ad07e737fa59b91680869
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2022
ms.locfileid: "144547976"
---
# <a name="install-and-manage-nuget-packages-in-visual-studio-for-mac"></a>在 Visual Studio for Mac 中安装和管理 NuGet 包

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

通过 Visual Studio for Mac 中的 NuGet 包管理器 UI，可轻松安装、卸载和更新项目和解决方案中的 NuGet 包。 可以搜索包和将包添加到 .NET Core、ASP.NET Core 和 Xamarin 项目。

本文介绍如何在项目中包括 NuGet 包并演示实现此流程无缝的工具链。

有关在 Visual Studio for Mac 中使用 NuGet 的简介，请参阅[快速入门：在 Visual Studio for Mac 中安装和使用包](/nuget/quickstart/install-and-use-a-package-in-visual-studio-mac)

## <a name="find-and-install-a-package"></a>查找并安装包

1. 对于 Visual Studio for Mac 中打开的项目，右键单击“解决方案窗口”中的“依赖项”文件夹（如果使用 Xamarin 项目，则为“包”文件夹）并选择“管理 NuGet 包...”   。

    ![此屏幕截图是“添加新NuGet包上下文操作”。](media/nuget-walkthrough-packages-menu.png)

2. “**管理NuGet包**”对话框出现。 确保对话框左下角的 **“包源**”下拉列表设置为`nuget.org`“，以便搜索中心NuGet包存储库。

    ![此屏幕截图是“管理NuGet包”对话框 - 列出NuGet包。 包源选项设置为 nuget.org。](media/nuget-walkthrough-add-packages1.png)

3. 例如，使用右上角的 **搜索** 框查找特定包 `EntityFramework`。 找到要使用的包后，请选择它并选择 **“添加包** ”按钮以开始安装。

    ![此屏幕截图是添加 EntityFramework NuGet 包。](media/nuget-walkthrough-add-packages2.png)

4. 下载包后，会将其添加到项目中。 解决方案将根据正在编辑的项目类型而发生变化：

    **Xamarin 项目**
    * “引用”节点包含属于 NuGet 包的所有程序集列表。
    * “**包”** 节点显示已下载的每个NuGet包。 可以更新该列表中的包，或从列表中删除包。
    
    **.NET Core 项目**
    * **依赖项> NuGet** 节点显示已下载的每个NuGet包。 可以更新该列表中的包，或从列表中删除包。

## <a name="using-nuget-packages"></a>使用 NuGet 包

添加 NuGet 包并更新项目引用后，可以如针对任何项目引用一样根据 API 对其进行编程。

请确保将任何所需的 `using` 指令添加到文件顶部：

```csharp
using Newtonsoft.Json;
```

<a name="Package_Updates" class="injected"></a>

## <a name="updating-packages"></a>更新包

通过右键单击“依赖项”节点（对于 Xamarin 项目为“包”节点）可以一次性完成所有包更新，也可以在每个包上单独进行包更新。 当新版本的 NuGet 包可用时，将显示![更新图标：这是更新新版本 NUGet 包的更新图标 - 带圆的向上箭头。](media/nuget-walkthrough-update-icon.png)

右键单击“依赖项”，以访问上下文菜单，然后选择“更新”以更新所有包：

![此屏幕截图显示了“依赖项”上下文菜单，其中突出显示了“更新”菜单。](media/nuget-walkthrough-packages-menu-update.png)

* **管理 NuGet 包** - 打开窗口，将更多包添加到项目。
* 更新 - 检查每个包的源服务器并下载任何更新版本。
* 还原 - 下载任何缺少的包（无需将现有包升级到更新版本）。

**更新** 和 **还原** 选项也可以在解决方案级别使用，并影响解决方案中的所有项目。

### <a name="updating-to-pre-release-versions-of-packages"></a>更新为包的预发行版本
若要更新为包的较新预发行版本，可以右键单击“依赖项”以打开上下文菜单，然后选择“管理 NuGet 包...”菜单 。

![此屏幕截图显示了“管理NuGet包”的“依赖项”上下文菜单...突出显示了菜单。](media/nuget-walkthrough-packages-menu-manage-nuget-packages.png)

选中对话框底部的 **“包括预发布”** 复选框。

![此屏幕截图显示了打开的“管理NuGet包”对话框，其中选中了“包括预发布”选项。](media/nuget-walkthrough-show-pre-release-packages.png)

最后，从对话框的“ **更新** ”选项卡中，选择要更新的包，然后从“ **新版本** ”下拉列表中选择新的预发行版本，然后选择“ **更新包**”。

![此屏幕截图显示了打开“已安装”选项卡的“管理NuGet包”对话框，其中已选择包，此时会打开“新版本”下拉列表。](media/nuget-walkthrough-packages-nuget-dialog-update-installed-package.png)

### <a name="locating-outdated-packages"></a>查找过时的包
在 **解决方案** 窗口中，可以查看当前安装的包版本。 右键单击要更新的包。

![此屏幕截图显示“包”菜单，其中包含“更新”、“删除”、“刷新”选项。](media/nuget-walkthrough-PackageMenu.png)

当包的新版本可用时，你还将看到包名称旁边的通知。 可以决定是否要更新它。

![此屏幕截图显示了新包版本可用时显示的通知。](media/nuget-walkthrough-package-update-available.png)

显示的菜单中包含两个选项：

* 更新 - 检查源服务器并下载更新版本（如果存在）。
* 删除 - 从此项目中删除包，并从项目引用中删除相关的程序集。

## <a name="manage-packages-for-the-solution"></a>管理解决方案的包

管理解决方案的包是同时处理多个项目的便捷方式。

1. 右键单击解决方案，并选择“管理 NuGet 包…”：

    ![此屏幕截图显示了管理解决方案的NuGet包。](media/nuget-walkthrough-manage-packages-solution.png)

1. 管理解决方案包时，UI 允许你选择受操作影响的项目：

    ![此屏幕截图显示管理解决方案包时Project选择器。](media/nuget-walkthrough-add-to-projects.png)

### <a name="consolidate-tab"></a>“合并”选项卡

使用多个项目的解决方案时，请确保在每个项目中使用同一NuGet包的任何位置，也使用相同的包版本号。 Visual Studio for Mac当你选择管理解决方案的包时，通过在 程序包管理器 UI 中提供 **“合并**”选项卡来帮助简化。 使用 **“合并** ”选项卡，可以轻松查看解决方案中不同项目使用具有不同版本号的包的位置：

![此屏幕截图显示了“程序包管理器 UI 合并”选项卡。](media/nuget-walkthrough-consolidate-tab.png)

在此示例中，NuGetDemo 项目使用的是 Microsoft.EntityFrameworkCore 3.1.23，而 NuGetDemo.Shared 使用的是 Microsoft.EntityFrameworkCore 5.0.2。 若要合并包版本，请执行以下步骤：

1. 在项目列表中选择要更新的项目。
1. 选择要在 **新版本** 列表中所有这些项目中使用的版本，例如 Microsoft.EntityFrameworkCore 6.0.3。
1. 选择“合并包”按钮。

包管理器将选定的包版本安装到所有选定的项目中，之后包不再显示在“合并”选项卡上。

## <a name="adding-package-sources"></a>添加包源

最初从 nuget.org 检索安装包。然而，可以将其他包位置添加到 Visual Studio for Mac。 它可用于测试正在开发的你自己的NuGet包，或使用公司或组织内的专用NuGet服务器。

在 Visual Studio for Mac 中，导航到“Visual Studio”>“首选项”>“NuGet”>“源”，查看和编辑包源的列表。 **源** 可以是由 URL) 或本地目录指定的远程服务器 (。

![此屏幕截图显示包源，用于将其他包位置添加到Visual Studio for Mac。 ](media/nuget-walkthrough-PackageSource.png)

选择 **“添加”** 以设置新源。 输入友好 **名称和****位置**， (包源的 URL 或文件路径) 。 如果源是安全的 Web 服务器，则输入 **用户名和密码**，否则请将这些条目留空：

![此屏幕截图显示了“添加包源”对话框，其中提示输入名称、位置 URL、用户名和密码。](media/nuget-walkthrough-PackageSource2.png)

搜索包时可以选择不同的源：

![此屏幕截图显示了“添加包源”对话框，其中显示了包含包源列表的下拉列表。](media/nuget-walkthrough-PackageSource3.png)

## <a name="version-control"></a>版本控制

NuGet 文档讨论了[在不将包提交到源控件的情况下使用 NuGet](/nuget/consume-packages/packages-and-source-control)。 如果不希望将二进制文件和未使用信息存储到源代码管理中，可以将 Visual Studio for Mac 配置为自动从服务器还原包。 当开发人员第一次从源代码管理检索项目时，Visual Studio for Mac将自动下载并安装所需的包。

![此屏幕截图显示打开解决方案时自动还原包的“首选项”屏幕。](media/nuget-walkthrough-AutoRestore.png)

有关如何使 `packages` 目录不受跟踪的详细信息，请参阅特定的源控件文档。

## <a name="related-video"></a>相关视频

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Using-NuGet/player]

## <a name="see-also"></a>另请参阅

* [在 Windows) 上的 Visual Studio (中安装和使用包的视频](/nuget/quickstart/install-and-use-a-package-in-visual-studio)