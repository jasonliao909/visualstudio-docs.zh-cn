---
title: DSL 的 MSI 和 VSIX 部署
description: 了解如何在你自己的计算机或其他计算机上安装特定于域 (DSL) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 879028746eac10160492f03651ef8b51714e9c6a
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112391005"
---
# <a name="msi-and-vsix-deployment-of-a-dsl"></a>DSL 的 MSI 和 VSIX 部署
可以在自己的计算机或其他计算机上安装特定于域的语言。 Visual Studio必须已安装在目标计算机上。

## <a name="choosing-between-vsix-and-msi-deployment"></a><a name="which"></a> 在 VSIX 和 MSI 部署之间选择
 有两种部署域特定语言的方法：

|方法|优点|
|-|-|
|VSX (Visual Studio 扩展) |部署非常简单：从 DslPackage 项目复制并执行 **.vsix** 文件。<br /><br /> 有关详细信息，请参阅[使用 VSX 安装和卸载 DSL。](#Installing)|
|MSI (安装程序文件) |- 允许用户通过双击 DSL Visual Studio打开数据。<br />- 将图标与目标计算机中的 DSL 文件类型关联。<br />- 将 XSD (XML 架构) DSL 文件类型关联。 这样可以避免在将文件加载到 Visual Studio。<br /><br /> 必须将安装项目添加到解决方案，以创建 MSI。<br /><br /> 有关详细信息，请参阅使用[MSI 文件 部署 DSL。](#msi)|

## <a name="install-and-uninstall-a-dsl-by-using-the-vsx"></a><a name="Installing"></a> 使用 VSX 安装和卸载 DSL

使用此方法安装 DSL 时，用户可以从 Visual Studio 中打开 DSL 文件，但不能从 Windows 资源管理器。

### <a name="to-install-a-dsl-by-using-the-vsx"></a>使用 VSX 安装 DSL

1. 找到 DSL 包项目构建的 **.vsix** 文件：

   1. 在 **解决方案资源管理器** 中，右键单击 **DslPackage** 项目，然后单击 **"打开** 文件资源管理器"。

   2. 找到文件 **bin \\ \* \\**_YourProject_**。DslPackage.vsix**

2. 将 **.vsix** 文件复制到要安装 DSL 的目标计算机。 该计算机可以是自己的计算机或其他计算机。

   - 目标计算机必须具有运行时支持 DLL 的 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 版本之一。 有关详细信息，请参阅支持的[可视化Visual Studio版本&建模 SDK。](../modeling/supported-visual-studio-editions-for-visualization-amp-modeling-sdk.md)

   - 目标计算机必须具有 **DslPackage\source.extensions.manifest** Visual Studio中指定的版本之一。

3. 在目标计算机上，双击 **.vsix** 文件。

    “” 将会打开并安装扩展。

4. 启动或重启 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]。

5. 若要测试 DSL，Visual Studio创建具有为 DSL 定义的扩展名的新文件。

### <a name="to-uninstall-a-dsl-that-was-installed-by-using-vsx"></a>卸载使用 VSX 安装的 DSL

1. 在“工具”  菜单上，选择“扩展和更新” 。

2. 展开“已安装的扩展” 。

3. 选择定义 DSL 的扩展，然后单击"卸载 **"。**

   在极少数情况下，有错误的扩展无法加载并在错误窗口中创建报告，但不显示在扩展管理器中。 在这种情况下，可以通过从以下位置删除文件来删除扩展：

   *LocalAppData* **\Microsoft\VisualStudio\10.0\Extensions**

## <a name="deploying-a-dsl-in-an-msi"></a><a name="msi"></a> 在 MSI 中部署 DSL
 通过为 DSL 定义 MSI (Windows Installer) 文件，可以允许用户从 DSL 文件打开 DSL Windows 资源管理器。 还可以将图标和简短说明与文件扩展名关联。 此外，MSI 可以安装可用于验证 DSL 文件的 XSD。 如果需要，可以将其他组件添加到将同时安装的 MSI 中。

 有关 MSI 文件和其他部署选项的详细信息，请参阅 [部署应用程序、服务和组件](../deployment/deploying-applications-services-and-components.md)。

 若要生成 MSI，需要将安装程序项目添加到Visual Studio解决方案。 创建安装程序项目的最简单方法是使用 CreateMsiSetupProject.tt 模板，可从 [VMSDK 站点 下载该模板](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)。

### <a name="to-deploy-a-dsl-in-an-msi"></a>在 MSI 中部署 DSL

1. 在 `InstalledByMsi` 扩展清单中设置 。 这可以防止安装和卸载 VSX，MSI 除外。 如果将其他组件包括在 MSI 中，这一点很重要。

   1. 打开 DslPackage\source.extension.tt

   2. 在 之前插入以下行 `<SupportedProducts>` ：

       ```xml
       <InstalledByMsi>true</InstalledByMsi>
       ```

2. 创建或编辑一个图标，该图标将在 Windows 资源管理器。 例如，编辑 **DslPackage\Resources\File.ico**

3. 请确保 DSL 的以下属性正确：

   - 在 DSL 资源管理器中，单击根节点，在属性窗口中查看：

       - 说明

       - 版本

   - 单击"**编辑器"** 节点，在属性窗口单击"图标 **"。** 设置 值以引用 **DslPackage\Resources** 中的图标文件，例如 **File.ico**

   - 在"**生成**"菜单 **配置服务器，** 然后选择要构建的配置，例如"发布"或"**调试"。**

4. 转到可视化 [和建模 SDK 主页，然后](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)**从"下载**"选项卡下载 **CreateMsiSetupProject.tt。**

5. 将 **CreateMsiSetupProject.tt** 添加到 Dsl 项目。

    Visual Studio创建名为 **CreateMsiSetupProject.vdproj 的文件**。

6. 在Windows 资源管理器中，将 Dsl \\ *.vdproj 复制到名为 Setup 的新文件夹。

     (如果需要，现在可以从 Dsl CreateMsiSetupProject.tt 排除该) 

7. 在 **解决方案资源管理器** 中，将 **Setup \\ \* .vdproj** 添加为现有项目。

8. 在"**项目"** 菜单上，单击 **"项目依赖项"。**

    在" **项目依赖项"** 对话框中，选择安装项目。

    选择 **DslPackage 旁边的框**。

9. 重新生成解决方案。

10. 在Windows 资源管理器中，找到安装程序项目中的生成 MSI 文件。

     将 MSI 文件复制到要安装 DSL 的计算机。 双击 MSI 文件。 安装程序运行。

11. 在目标计算机中，创建一个扩展名为 DSL 的新文件。 验证：

    - 在Windows 资源管理器视图中，文件将显示，并包含定义的图标和说明。

    - 双击该文件时，将Visual Studio DSL 编辑器中打开 DSL 文件。

    如果需要，可以手动创建安装程序项目，而不是使用文本模板。 有关包含此过程的演练，请参阅可视化和建模 SDK 实验室的第 5 [章](https://code.msdn.microsoft.com/DSLToolsLab/Release/ProjectReleases.aspx?ReleaseId=4207)。

### <a name="to-uninstall-a-dsl-that-was-installed-from-an-msi"></a>卸载从 MSI 安装的 DSL

1. 在 Windows 中，打开 **"程序和功能"** 控制面板。

2. 卸载 DSL。

3. 重启 Visual Studio。
