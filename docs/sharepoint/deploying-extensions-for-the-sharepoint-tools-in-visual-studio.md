---
title: 在 Visual Studio | 中为 SharePoint Tools 部署Visual Studio |Microsoft Docs
description: 在 Visual Studio 中为 SharePoint 工具部署Visual Studio。 在 VSIX Visual Studio项目中 (扩展) 创建 VSIX 包。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying extensions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 26c2b23be3708f3e55b5559f06d3ae869c49764e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664160"
---
# <a name="deploy-extensions-for-the-sharepoint-tools-in-visual-studio"></a>在 Visual Studio 中部署 SharePoint 工具扩展

若要部署 SharePoint 工具扩展，请创建一个扩展 (VSIX) 包，其中包含扩展程序集以及要随扩展一起分发的 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 其他任何文件。 VSIX 包是一个压缩文件，它遵循 开放打包约定 (OPC) 标准。 VSIX 包具有 *.vsix* 扩展。

创建 VSIX 包后，其他用户可以运行 .vsix 文件来安装扩展。 当用户安装扩展时，所有文件将安装到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0\Extensions 文件夹中。 若要部署扩展，可以将 VSIX 包上传到 Visual Studio [Marketplace](https://marketplace.visualstudio.com/)网站，或者可以通过某种其他方式（例如，在网络共享或其他网站上托管包）将包分发给客户。

有关创建 VSIX 包以及将它们部署到 Visual Studio[市场，](https://marketplace.visualstudio.com/)请参阅 Shipping Visual Studio [Extensions。](../extensibility/shipping-visual-studio-extensions.md)

 可以使用 VISUAL STUDIO 中的 VSIX Project模板创建 **VSIX** 包，也可以手动创建 VSIX 包。

## <a name="use-vsix-projects-to-create-vsix-packages"></a>使用 VSIX 项目创建 VSIX 包

可以使用 PROJECT SDK **提供的 VSIX** Visual Studio模板为 SharePoint 扩展创建 VSIX 包。 与手动创建 VSIX 包相比，使用 VSIX 项目具有多个好处：

- Visual Studio生成项目时自动生成 VSIX 包。 将部署文件添加到包和为包创建 [Content_Types].xml 文件等任务已由你完成。

- 可以将 VSIX 项目配置为在 VSIX 包中包括扩展项目的生成输出和其他文件（如项目模板和项模板）。

有关使用 VSIX 项目的信息，请参阅[VSIX Project模板](../extensibility/vsix-project-template.md)。

### <a name="organize-your-projects"></a>组织项目

默认情况下，VSIX 项目仅生成 VSIX 包，而不是程序集。 因此，通常不会在 VSIX 项目中SharePoint工具扩展。 通常至少处理两个项目：

- VSIX 项目。

- 实现扩展的类库项目。

还可以为某些类型的扩展使用其他项目：

- 实现扩展使用的任何SharePoint命令的类库项目。 有关演示此方案的演练，请参阅演练：扩展服务器资源管理器以显示 [Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

- 创建项Project或项目模板的项模板或项目模板项目（如果扩展定义了新类型的SharePoint项目项）。 有关演示此方案的演练，请参阅演练：使用项模板创建自定义 [操作项目项，第 1 部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)。

- 实现项模板或项目模板的自定义向导的类库项目（如果扩展包含模板）。 有关演示此方案的演练，请参阅演练：使用项模板创建自定义 [操作项目项，第 2 部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)。

如果在同一个 Visual Studio 解决方案中包括所有项目，可以修改 VSIX 项目中的 source.extension.vsixmanifest 文件，以包含类库项目的生成输出。

### <a name="edit-the-vsix-manifest"></a>编辑 VSIX 清单

必须编辑 VSIX 项目中的 source.extension.vsixmanifest 文件，以包含要包括在扩展中的所有项的条目。 从快捷菜单打开 source.extension.vsixmanifest 文件时，该文件将显示在设计器中，该设计器提供用于编辑文件中 XML 的 UI。 有关详细信息，请参阅 [VSIX 清单设计器](../extensibility/vsix-manifest-designer.md)。

必须将以下项的条目添加到 source.extension.vsixmanifest 文件：

- 扩展程序集。

- 实现扩展所使用的SharePoint命令的程序集。

- 与扩展关联的任何项目模板或项模板。

- 与扩展关联的模板的自定义向导。

以下过程介绍如何为其中每个项将条目添加到 .vsixmanifest 文件。

#### <a name="to-include-the-extension-assembly"></a>包含扩展程序集

1. 在 VSIX 项目中，打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择"打开 **"。**

     该文件在设计器中打开

2. 在编辑器 **的"** 资产"选项卡上，选择"新建 **"** 按钮。

     " **添加新资产"** 对话框随即打开。

3. 在"**类型"** 列表中，选择 **"Microsoft.VisualStudio.MefComponent"。**

4. 在" **源** "列表中，执行以下步骤之一：

    - 如果扩展程序集基于与 VSIX 项目位于同一解决方案中的项目生成，请选择当前 **解决方案 中的项目**。 在 **Project** 列表中，选择项目的名称。

    - 如果扩展程序集作为文件包含在项目中，请选择 **"文件系统上的文件"。** 在"**路径**"列表中，输入扩展程序集文件的完整路径，或使用"浏览"按钮查找并选择程序集文件。

5. 选择 **“确定”** 按钮。

#### <a name="to-include-a-sharepoint-command-assembly"></a>包含 SharePoint 命令程序集

1. 在 VSIX 项目中，打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择"打开 **"** 按钮。

     该文件将在设计器中打开。

2. 在编辑器 **的"** 资产"部分中，选择"新建 **"** 按钮。

     " **添加新资产"** 对话框随即打开。

3. 在"**类型"** 框中，**输入SharePoint。Commands.v4**。

4. 在" **源** "列表中，执行以下步骤之一：

    - 如果命令程序集基于与 VSIX 项目位于同一解决方案中的项目生成，请选择当前 **解决方案 中的项目**。 在 **Project** 列表中，选择项目的名称。

    - 如果命令程序集作为文件包含在项目中，请选择"**文件系统上的文件"。** 在"**路径**"列表中，输入扩展程序集文件的完整路径，或使用"浏览"按钮查找并选择程序集文件。

5. 选择 **“确定”** 按钮。

#### <a name="to-include-a-template-that-you-create"></a>包含创建的模板

1. 在 VSIX 项目中，打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择"打开 **"** 按钮。

     该文件将在设计器中打开。

2. 在编辑器 **的"** 资产"部分中，选择"新建 **"** 按钮。

     " **添加新资产"** 对话框随即打开。

3. 在"**类型"** 列表中，选择 **"Microsoft.VisualStudio.ProjectTemplate"** 或 **"Microsoft.VisualStudio.ItemTemplate"。**

4. 在" **源"** 列表中， **选择当前解决方案 中的项目**。

5. 在Project **列表中**，选择项目的名称，然后选择"确定 **"** 按钮。

6. 在 **解决方案资源管理器** 中，打开"模板"或"Project模板"项目的快捷菜单，然后选择"卸载 **Project"。**

7. 再次打开项目节点的快捷菜单，然后选择 **"编辑**_YourTemplateProjectName_**.csproj"** 或"**编辑**_YourTemplateProjectName_**.vbproj"。**

8. 在项目 `VSTemplate` 文件中找到以下元素。

    ```xml
    <VSTemplate Include="YourTemplateName.vstemplate">
    ```

9. 将此元素替换为以下 XML。

    ```xml
    <VSTemplate Include="YourTemplateName.vstemplate">
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>
    </VSTemplate>
    ```

     `OutputSubPath`元素在生成项目时创建项目模板的路径中指定其他文件夹。 此处指定的文件夹可确保项模板仅在客户打开"添加新 Project"对话框、展开"SharePoint"节点，然后选择 **"2010"****节点时** 可用。

10. 保存并关闭该文件。

11. 在 **解决方案资源管理器** 中，打开"模板"或"Project模板"项目的快捷菜单，然后选择"重新加载 **Project"。**

#### <a name="to-include-a-template-that-you-create-manually"></a>包含手动创建的模板

1. 在 VSIX 项目中，向项目添加新文件夹以包含模板。

2. 在此新文件夹下，创建以下子文件夹，然后将模板 (.zip) 文件添加到 *区域设置 ID* 文件夹。

     *YourTemplateFolder*

     **SharePoint**

     **SharePoint14**

     *区域设置 ID*

     *YourTemplateName*.zip

     例如，如果有一个名为 ContosoCustomAction.zip 的项模板 (美国) 英语区域设置，则完整路径可能ItemTemplates\SharePoint\SharePoint14\1033\ContosoCustomAction.zip *。*

3. 在 **解决方案资源管理器** 中，选择 *YourTemplateName* (模板.zip) 。

4. 在"**属性"** 窗口中，将"**生成操作"** 属性设置为 **"内容"。**

5. 打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择"打开 **"。**

     该文件将在设计器中打开。

6. 在编辑器 **的"** 资产"部分中，选择"新建 **"** 按钮。

     " **添加新资产"** 对话框随即打开。

7. 在"**类型"** 列表中，选择 **"Microsoft.VisualStudio.ItemTemplate"** 或 **"Microsoft.VisualStudio.ProjectTemplate"。**

8. 在"**源"** 列表中，选择 **"文件系统上的文件"。**

9. 在"**路径**"字段中，输入程序集的完整 (例如ItemTemplates\SharePoint\SharePoint14\1033\ContosoCustomAction.zip，或使用"浏览 *"* 按钮查找并选择程序集，然后选择"确定 **"** 按钮。

#### <a name="to-include-a-wizard-for-a-project-template-or-item-template"></a>包含项目模板或项模板的向导

1. 在 VSIX 项目中，打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择"打开 **"。**

     该文件将在设计器中打开。

2. 在编辑器 **的"** 资产"部分中，选择"新建 **"** 按钮。

     " **添加新资产"** 对话框随即打开。

3. 在"**类型"** 列表中，选择 **"Microsoft.VisualStudio.Assembly"。**

4. 在" **源** "列表中，执行以下步骤之一：

    - 如果向导程序集基于与 VSIX 项目位于同一解决方案中的项目生成，请选择当前 **解决方案 中的项目**。 在 **Project** 列表中，选择项目的名称。

    - 如果向导程序集作为文件包含在项目中，请选择"**文件系统上的文件"。** 在"**路径**"字段中，输入程序集文件的完整路径，或使用"浏览"按钮查找并选择程序集。

5. 选择 **“确定”** 按钮。

### <a name="related-walkthroughs"></a>相关演练

下表列出了演示如何使用 VSIX 项目部署不同类型的 SharePoint 扩展的演练。

|扩展类型|相关演练|
|--------------------|--------------------------|
|仅包含扩展程序集的扩展|[演练：扩展SharePoint项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)<br /><br /> [演练：创建SharePoint Project扩展](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)<br /><br /> [演练：调用 SharePoint 扩展中的 服务器资源管理器 客户端对象模型](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)|
|包含命令SharePoint扩展|[演练：为项目创建SharePoint步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)<br /><br /> [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)<br /><br /> [演练：使用项目模板创建站点列项目项，第 2 部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)|
|包含自定义模板Visual Studio扩展|[演练：使用项模板创建自定义操作项目项，第 1 部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)<br /><br /> [演练：使用项目模板创建站点列项目项，第 1 部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)|
|包含模板向导的扩展|[演练：使用项模板创建自定义操作项目项，第 2 部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)<br /><br /> [演练：使用项目模板创建站点列项目项，第 2 部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)|

## <a name="create-vsix-packages-manually"></a>手动创建 VSIX 包

如果要手动为 SharePoint 工具扩展创建 VSIX 包，请执行以下步骤：

1. 创建新文件夹中的 extension.vsixmanifest 文件和 [Content_Types].xml 文件。 有关详细信息，请参阅 [VSIX 包剖析](../extensibility/anatomy-of-a-vsix-package.md)。

2. 在Windows资源管理器中，右键单击包含两个 XML 文件的文件夹，单击"发送到"，然后单击"压缩 (压缩) 文件夹" 。 将生成的 .zip 文件重命名为 Filename.vsix，其中 Filename 是用于安装包的可再发行文件的名称。

3. 将扩展程序集添加到 VSIX 包。 如果扩展包含 SharePoint 命令，则还要将实现 SharePoint 命令的程序集添加到 VSIX 包。

4. 修改 extension.vsixmanifest 文件：

    - 在 元素下添加 元素，然后将新元素的值设置为在 VSIX 包中实现扩展的程序集 `Microsoft.VisualStudio.MefComponent` `Assets` 的相对路径。 有关详细信息，请参阅[MEFComponent 元素 (VSX 架构) 。 ](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))

    - 如果扩展包含一SharePoint调用服务器对象模型的 SharePoint，请添加 `Microsoft.VisualStudio.Assembly` 元素下的 `Assets` 元素。 将新元素的值设置为在 VSIX 包中实现 SharePoint 命令的程序集的相对路径。 有关详细信息，请参阅[ASSET Element (VSX Schema) 。 ](/previous-versions/dd393737(v=vs.110))

    - 如果扩展包含项目模板或项模板，则添加 元素下的 `ProjectTemplate` `ItemTemplate` 或 `Assets` 元素。 将新元素的值设置为 VSIX 包中包含模板的文件夹的相对路径。 有关详细信息，请参阅[PROJECTTemplate 元素 (VSX](/previous-versions/visualstudio/visual-studio-2010/dd393735\(v\=vs.100\))架构) [ItemTemplate 元素 (VSX 架构) 。 ](/previous-versions/visualstudio/visual-studio-2010/dd393681\(v\=vs.100\))

    - 如果扩展包含项目模板或项模板的自定义向导，则添加 `Assembly` 元素下的 `Assets` 元素。 将新元素的值设置为 VSIX 包中程序集的相对路径，然后将 属性设置为完整的程序集名称 (包括版本、区域性和公钥 `AssemblyName`) 。 有关详细信息，请参阅[VSX 架构 (依赖项元素) 。 ](/previous-versions/dd393682(v=vs.110))

### <a name="example"></a>示例

以下示例显示了扩展工具扩展的 extension.vsixmanifest SharePoint的内容。 扩展在名为 Contoso.ProjectExtension.dll 的程序集中实现。 该扩展SharePoint名为 Contoso.ExtensionCommands.dll 的命令程序集，以及 VSIX 包中 **名为 ItemTemplates** 的文件夹下的项模板。 此示例假定两个程序集与 VSIX 包中的 extension.vsixmanifest 文件在同一文件夹中。

```xml
<PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011">
  <Metadata>
    <Identity Id="CustomActionProjectItem.Microsoft.b99efe4d-cef3-4afd-b9af-034ca0c52743" Version="1.0" Language="en-US" Publisher="Microsoft" />
    <DisplayName>CustomActionProjectItem</DisplayName>
    <Description>Empty VSIX Project.</Description>
  </Metadata>
  <Installation>
    <InstallationTarget Id="Microsoft.VisualStudio.Pro" Version="11.0" />
  </Installation>
  <Dependencies>
    <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" Version="4.5" />
  </Dependencies>
  <Assets>
    <Asset Type="Microsoft.VisualStudio.ItemTemplate" Path="ItemTemplates" />
    <Asset Type="Microsoft.VisualStudio.MefComponent" Path="ProjectItemDefinition.dll" />
  </Assets>
</PackageManifest>
```

## <a name="see-also"></a>另请参阅

- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
- [扩展服务器资源管理器中的“SharePoint 连接”节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [调用对象SharePoint模型](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [在 Visual Studio 中调试 SharePoint 工具扩展](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)