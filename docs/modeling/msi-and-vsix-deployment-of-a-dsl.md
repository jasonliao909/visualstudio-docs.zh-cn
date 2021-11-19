---
title: DSL 的 MSI 和 VSIX 部署
description: 了解如何在自己的计算机或其他计算机上安装 (DSL) 域特定语言。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 65df491989278f768f44cb0f768a216e082a6570
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663945"
---
# <a name="msi-and-vsix-deployment-of-a-dsl"></a>DSL 的 MSI 和 VSIX 部署
可以在自己的计算机或其他计算机上安装域特定语言。 Visual Studio 必须已安装在目标计算机上。

## <a name="choosing-between-vsix-and-msi-deployment"></a><a name="which"></a> 在 VSIX 和 MSI 部署之间选择
 部署域特定语言的方法有两种：

|方法|好处|
|-|-|
|VSX (Visual Studio 扩展) |易于部署：从 DslPackage 项目复制并执行 **.vsix** 文件。<br /><br /> 有关详细信息，请参阅 [使用 VSX 安装和卸载 DSL](#Installing)。|
|MSI (安装程序文件) |-允许用户通过双击 DSL 文件来打开 Visual Studio。<br />-将图标与目标计算机中的 DSL 文件类型相关联。<br />-将 XSD (XML 架构) 与 DSL 文件类型相关联。 这可以避免在将文件加载到 Visual Studio 时出现警告。<br /><br /> 必须将安装项目添加到解决方案才能创建 MSI。<br /><br /> 有关详细信息，请参阅 [使用 MSI 文件部署 DSL](#msi)。|

## <a name="install-and-uninstall-a-dsl-by-using-the-vsx"></a><a name="Installing"></a> 使用 VSX 安装和卸载 DSL

此方法安装 dsl 后，用户可以从 Visual Studio 中打开 dsl 文件，但无法从 Windows 资源管理器打开该文件。

### <a name="to-install-a-dsl-by-using-the-vsx"></a>使用 VSX 安装 DSL

1. 找到 DSL 包项目生成的 **.vsix** 文件：

   1. 在 **解决方案资源管理器** 中，右键单击 **DslPackage** 项目，然后单击 " **在文件资源管理器中打开文件夹**"。

   2. 找到 _项目_ 文件 **\\ \* \\****。DslPackage**

2. 将 **.vsix** 文件复制到要安装 DSL 的目标计算机。 该计算机可以是自己的计算机或其他计算机。

   - 目标计算机必须具有在 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 运行时支持 dsl 的版本之一。 有关详细信息，请参阅[& 建模 SDK 支持的可视化 Visual Studio 版本](../modeling/supported-visual-studio-editions-for-visualization-amp-modeling-sdk.md)。

   - 目标计算机必须具有 **DslPackage\source.extensions.manifest** 中指定的其中一个 Visual Studio 版本。

3. 在目标计算机上，双击 **.vsix** 文件。

    “” 将会打开并安装扩展。

4. 启动或重启 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]。

5. 若要测试 DSL，请使用 Visual Studio 创建新文件，该文件具有你为 DSL 定义的扩展。

### <a name="to-uninstall-a-dsl-that-was-installed-by-using-vsx"></a>卸载使用 VSX 安装的 DSL

1. 在“工具”  菜单上，选择“扩展和更新” 。

2. 展开“已安装的扩展” 。

3. 选择在其中定义 DSL 的扩展，然后单击 " **卸载**"。

   在极少数情况下，有错误的扩展无法加载并在错误窗口中创建报告，但不显示在扩展管理器中。 在这种情况下，可以通过从以下位置删除文件来删除扩展：

   *LocalAppData* **\Microsoft\VisualStudio\10.0\Extensions**

## <a name="deploying-a-dsl-in-an-msi"></a><a name="msi"></a> 在 MSI 中部署 DSL
 通过为 DSL 定义 MSI (Windows Installer) 文件，可允许用户从 Windows 资源管理器打开 dsl 文件。 你还可以将图标和简短说明与你的文件扩展名相关联。 此外，MSI 还可以安装可用于验证 DSL 文件的 XSD。 如果需要，可以将其他组件添加到将在其中同时安装的 MSI。

 有关 MSI 文件和其他部署选项的详细信息，请参阅 [部署应用程序、服务和组件](../deployment/deploying-applications-services-and-components.md)。

 若要生成 MSI，请将安装项目添加到 Visual Studio 解决方案中。 创建安装项目最简单的方法是使用 CreateMsiSetupProject.tt 模板，该模板可从 [VMSDK 站点](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)下载。

### <a name="to-deploy-a-dsl-in-an-msi"></a>在 MSI 中部署 DSL

1. 设置 `InstalledByMsi` 在扩展清单中。 这会阻止除 MSI 之外安装和卸载 VSX。 如果你将在 MSI 中包含其他组件，则这一点非常重要。

   1. 打开 DslPackage\source.extension.tt

   2. 在之前插入以下行 `<SupportedProducts>` ：

       ```xml
       <InstalledByMsi>true</InstalledByMsi>
       ```

2. 在 Windows 资源管理器中创建或编辑将表示 DSL 的图标。 例如，编辑 **DslPackage\Resources\File.ico**

3. 请确保 DSL 的以下属性是正确的：

   - 在 DSL 资源管理器中，单击 "根" 节点，然后在属性窗口中查看：

       - 说明

       - 版本

   - 单击 " **编辑器** " 节点，然后在 "属性窗口中，单击" **图标**"。 设置值以引用 **DslPackage\Resources** 中的图标文件，如 **file .ico**

   - 在 " **生成** " 菜单上，打开 **Configuration Manager**，然后选择要生成的配置，例如 " **发布** " 或 " **调试**"。

4. 请参阅 [可视化和建模 SDK 主页](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)，然后在 " **下载** " 选项卡上下载 **CreateMsiSetupProject.tt**。

5. 将 **CreateMsiSetupProject.tt** 添加到 Dsl 项目。

    Visual Studio 将创建一个名为 **.vdproj** 的文件。

6. 在 Windows 资源管理器中，将 Dsl \\ .vdproj 复制到名为 Setup 的新文件夹。

     (如果需要，现在可以从 Dsl 项目中排除 CreateMsiSetupProject.tt。 ) 

7. 在 **解决方案资源管理器** 中，**将 \\ \* .vdproj** 添加为现有项目。

8. 在 " **Project** " 菜单上，单击 " **Project 依赖关系**"。

    在 " **Project 依赖关系**" 对话框中，选择 "安装" 项目。

    选中 " **DslPackage**" 旁边的框。

9. 重新生成解决方案。

10. 在 Windows 资源管理器中，在安装项目中找到生成的 MSI 文件。

     将 MSI 文件复制到要安装 DSL 的计算机。 双击 MSI 文件。 安装程序运行。

11. 在目标计算机上，创建一个具有 DSL 文件扩展名的新文件。 验证：

    - 在 Windows 资源管理器列表视图中，会显示文件，其中包含你定义的图标和说明。

    - 双击该文件时，Visual Studio 启动，然后在 dsl 编辑器中打开 dsl 文件。

    如果愿意，可以手动创建安装项目，而不是使用文本模板。 有关包括此过程的演练，请参阅 [可视化和建模 SDK 实验室](https://code.msdn.microsoft.com/DSLToolsLab/Release/ProjectReleases.aspx?ReleaseId=4207)的第5章。

### <a name="to-uninstall-a-dsl-that-was-installed-from-an-msi"></a>卸载从 MSI 安装的 DSL

1. 在 Windows 中，打开 "**程序和功能**" 控制面板。

2. 卸载 DSL。

3. 重新启动 Visual Studio。
