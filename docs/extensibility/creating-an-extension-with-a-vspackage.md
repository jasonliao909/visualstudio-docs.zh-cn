---
title: 使用 VSPackage 创建扩展|Microsoft Docs
description: 了解如何使用 VSPackage 创建 VSIX 项目并添加 VSPackage 项目项，以便获取 UI Shell 服务以显示消息框。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
ms.assetid: c0cc5e08-4897-44f2-8309-e3478f1f999e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 29b7dd4a3cd6da6a13d999419bfef5a7eafa839adc53df115860e0785d534f75
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121293516"
---
# <a name="create-an-extension-with-a-vspackage"></a>使用 VSPackage 创建扩展

本演练演示如何创建 VSIX 项目并添加 VSPackage 项目项。 我们将使用 VSPackage 获取 UI Shell 服务以显示消息框。

## <a name="prerequisites"></a>先决条件

从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-a-vspackage"></a>创建 VSPackage

1. 创建名为 **FirstPackage** 的 VSIX 项目。 可以通过搜索"vsix"在"新建Project"找到 VSIX 项目模板。 

2. 项目打开时，添加名为 **FirstPackage** Visual Studio包项模板。 在“解决方案资源管理器”中，右键单击项目节点并选择“添加” > “新建项”  。 在"**添加新项"对话框中**，转到 **"Visual C#** 扩展性"，然后选择  >  "Visual Studio **包"。** 在 **窗口底部的** "名称"字段中，将命令文件名更改为 *FirstPackage.cs*。

3. 生成项目并启动调试。

    将显示该实例Visual Studio实例。 有关实验实例的信息，请参阅 [实验实例](../extensibility/the-experimental-instance.md)。

4. 在实验实例中，打开"**工具**  >  **扩展和更新"** 窗口。 应在此处看到 **FirstPackage** 扩展。  (如果在 Visual Studio 的工作实例中打开"扩展和更新"，则看不到 **FirstPackage**) 。

## <a name="load-the-vspackage"></a>加载 VSPackage

此时，不会加载扩展，因为没有任何因素会导致它加载。 通常，可以在与 UI 交互时加载扩展 (单击菜单命令、打开工具窗口) 或指定 VSPackage 应加载到特定 UI 上下文中。 有关加载 VSPackage 和 UI 上下文的信息，请参阅[加载 VSPackage。](../extensibility/loading-vspackages.md) 对于此过程，我们将展示在解决方案打开时如何加载 VSPackage。

1. 打开 *FirstPackage.cs* 文件。 查找 类 `FirstPackage` 的声明。 将现有属性替换为以下属性：

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]
    [Guid(FirstPackage.PackageGuidString)]
    public sealed class FirstPackage : Package
    ```

2. 让我们添加一条消息，告知 VSPackage 已加载。 我们使用 VSPackage 的 方法来完成此操作，因为只有在站点Visual Studio `Initialize()` 才能获取服务。  (若要详细了解如何获取服务，请参阅 [如何：](../extensibility/how-to-get-a-service.md)获取服务 .) 将 的 方法替换为获取服务、获取 接口并调用 `Initialize()` 其 `FirstPackage` <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowMessageBox%2A> 方法的代码。

    ```csharp
    protected override void Initialize()
    {
        base.Initialize();

        IVsUIShell uiShell = (IVsUIShell)GetService(typeof(SVsUIShell));
        Guid clsid = Guid.Empty;
        int result;
        Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(uiShell.ShowMessageBox(
            0,
            ref clsid,
            "FirstPackage",
             string.Format(CultureInfo.CurrentCulture, "Inside {0}.Initialize()", this.GetType().FullName),
            string.Empty,
            0,
            OLEMSGBUTTON.OLEMSGBUTTON_OK,
            OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST,
            OLEMSGICON.OLEMSGICON_INFO,
            0,
            out result));
    }
    ```

3. 生成项目并启动调试。 这将显示实验实例。

4. 在实验实例中打开解决方案。 应会看到一个消息框，显示"初始化中第一个包 **() 。**
