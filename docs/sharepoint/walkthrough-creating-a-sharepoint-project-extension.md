---
title: 演练：创建 SharePoint Project 扩展|Microsoft Docs
description: 创建SharePoint扩展，可用于响应项目级事件，例如添加、删除或重命名项目时。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 9355e533e408be7f1ed0f9a744f2babe2c1c463f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122047512"
---
# <a name="walkthrough-create-a-sharepoint-project-extension"></a>演练：创建SharePoint扩展
  本演练演示如何为项目创建SharePoint扩展。 可以使用项目扩展来响应项目级事件，例如添加、删除或重命名项目时。 还可以添加自定义属性，或在属性值更改时做出响应。 与项目项扩展不同，项目扩展不能与项目类型SharePoint相关联。 创建项目扩展时，在 中打开任何类型的项目SharePoint将加载该扩展 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

 在此演练中，你将创建自定义布尔属性，该属性将添加到在 中创建的任何SharePoint项目 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 设置为 **True** 时，新属性会将 Images 资源文件夹添加或映射到项目中。 如果设置为 **False，** 则删除 Images 文件夹（如果存在）。 有关详细信息，请参阅 [如何：添加和删除映射的文件夹](../sharepoint/how-to-add-and-remove-mapped-folders.md)。

 本演练演示了下列任务：

- 为 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 执行以下操作SharePoint项目创建扩展：

  - 将自定义项目属性添加到属性窗口。 属性适用于任何SharePoint项目。

  - 使用SharePoint对象模型将映射文件夹添加到项目。

  - 使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 自动化对象模型 (DTE) 从项目中删除映射文件夹。

- 生成 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] VSIX (扩展) 包以部署项目属性的扩展程序集。

- 调试和测试项目属性。

## <a name="prerequisites"></a>必备条件
 需要开发计算机上以下组件才能完成本演练：

- 支持的 、 [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] SharePoint 和 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 版本。

- [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)] 本演练使用 中的 **VSIX Project** 模板 [!INCLUDE[TLA2#tla_sdk](../sharepoint/includes/tla2sharptla-sdk-md.md)] 创建 VSIX 包以部署项目属性扩展。 有关详细信息，请参阅扩展 SharePoint[中的 Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)工具。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，必须创建两个项目：

- 一个 VSIX 项目，用于创建 VSIX 包以部署项目扩展。

- 实现项目扩展的类库项目。

  通过创建项目来开始演练。

#### <a name="to-create-the-vsix-project"></a>创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

3. 在"**新建Project"** 对话框中，展开 **Visual C#** 或Visual Basic **节点，** 然后选择"**扩展性"** 节点。

    > [!NOTE]
    > 此节点仅在安装 Visual Studio SDK 时可用。 有关详细信息，请参阅本主题前面的先决条件部分。

4. 在对话框顶部，在 .NET Framework 版本列表中选择".NET Framework **4.5"，** 然后选择 **VSIX Project** 模板。

5. 在" **名称** "框中，输入 **ProjectExtensionPackage**，然后选择"确定 **"** 按钮。

     **ProjectExtensionPackage** 项目显示在 **解决方案资源管理器。**

#### <a name="to-create-the-extension-project"></a>创建扩展项目

1. 在 **解决方案资源管理器** 中，打开解决方案节点的快捷菜单，选择"添加"，然后选择"新建 **Project"。** 

2. 在"**新建Project"** 对话框中，展开 **"Visual C#"** 或 **Visual Basic节点，** 然后选择"Windows"。 

3. 在对话框顶部，选择.NET Framework版本列表中的".NET Framework **4.5"，** 然后选择"类 **库**"项目模板。

4. 在" **名称** "框中，输入 **"ProjectExtension"，** 然后选择"确定 **"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **ProjectExtension** 项目添加到解决方案，并打开默认的 Class1 代码文件。

5. 从项目中删除 Class1 代码文件。

## <a name="configure-the-project"></a>配置项目
 在编写代码以创建项目扩展之前，请添加对扩展项目的代码文件和程序集引用。

#### <a name="to-configure-the-project"></a>配置项目

1. 将名为 **CustomProperty** 的代码文件添加到 ProjectExtension 项目。

2. 打开 **ProjectExtension** 项目的快捷菜单，然后选择"**添加引用"。**

3. 在"**引用管理器 - CustomProperty"** 对话框中，选择"**框架**"节点，然后选择"System.ComponentModel.Composition 和 System"旁边的复选框。Windows。窗体程序集。

4. 选择 **"扩展"** 节点，选中"Microsoft.VisualStudio"旁边的复选框。SharePoint和 EnvDTE 程序集，然后选择"确定 **"** 按钮。

5. 在 **解决方案资源管理器** 中，在 **ProjectExtension 项目的"引用**"文件夹下，选择 **"EnvDTE"。** 

6. 在" **属性"** 窗口中，将" **嵌入互操作类型"属性** 更改为 **False**。

## <a name="define-the-new-sharepoint-project-property"></a>定义新的 SharePoint 项目属性
 创建一个类，用于定义项目扩展名和新项目属性的行为。 若要定义新项目扩展，类实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 接口。 每当你想要为项目定义扩展时，SharePoint接口。 此外，将 <xref:System.ComponentModel.Composition.ExportAttribute> 添加到 类。 此属性允许 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 发现和加载 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 类型传递给特性的构造函数。

#### <a name="to-define-the-new-sharepoint-project-property"></a>定义新的 SharePoint 项目属性

1. 将以下代码粘贴到 CustomProperty 代码文件中。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectextension/customproperty.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectextension/customproperty.cs" id="Snippet1":::

## <a name="build-the-solution"></a>生成解决方案
 接下来，生成解决方案以确保它在编译时不会出错。

#### <a name="to-build-the-solution"></a>生成解决方案

1. 在菜单栏上，依次选择“生成” > “生成解决方案” 。

## <a name="create-a-vsix-package-to-deploy-the-project-property-extension"></a>创建 VSIX 包以部署项目属性扩展
 若要部署项目扩展，请使用解决方案中的 VSIX 项目创建 VSIX 包。 首先，通过修改 VSIX 项目中包含的 source.extension.vsixmanifest 文件来配置 VSIX 包。 然后，通过生成解决方案创建 VSIX 包。

#### <a name="to-configure-and-create-the-vsix-package"></a>配置和创建 VSIX 包

1. 在 **解决方案资源管理器** 中，打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择"打开 **"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 在清单设计器中打开文件。 "元数据"选项卡中 **显示** 的信息也会显示在"扩展 **和更新"中**。 所有 VSIX 包都需要 extension.vsixmanifest 文件。 有关此文件的信息，请参阅 [VSIX 扩展架构 1.0 参考](/previous-versions/dd393700(v=vs.110))。

2. 在"**产品名称"** 框中，输入 **"自定义Project属性"。**

3. 在"**创作"** 框中，输入 **"Contoso"。**

4. 在"**说明"** 框中，**输入自定义SharePoint项目属性**，该属性将 Images 资源文件夹的映射切换为项目 。

5. 选择" **资产"** 选项卡，然后选择"新建 **"** 按钮。

     将出现 **"添加新资产** "对话框。

6. 在"**类型"** 列表中，选择 **"Microsoft.VisualStudio.MefComponent"。**

    > [!NOTE]
    > 此值对应于 `MEFComponent` extension.vsixmanifest 文件中的元素。 此元素指定 VSIX 包中扩展程序集的名称。 有关详细信息，请参阅[MEFComponent 元素 (VSX 架构) 。 ](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))

7. 在" **源"** 列表中，选择" **当前解决方案中的 A 项目"** 选项按钮。

8. 在 **"Project"** 列表中，选择 **"ProjectExtension"。**

     此值标识在项目中构建的程序集的名称。

9. 选择 **"确定** "以关闭 **"添加新资产** "对话框。

10. 在菜单栏上，选择"完成 **时** 全部保存文件  >  "，然后关闭清单设计器。

11. 在菜单栏上，选择"**生成**  >  **生成解决方案**"，并确保项目编译时不会出错。

12. 在 **解决方案资源管理器** 中，打开 **ProjectExtensionPackage** 项目的快捷菜单，然后选择"打开文件夹中的文件资源管理器 **按钮。**

13. 在 **文件资源管理器** 中，打开 ProjectExtensionPackage 项目的生成输出文件夹，然后验证该文件夹是否包含名为 ProjectExtensionPackage.vsix 的文件。

     默认情况下，生成输出文件夹为 。包含项目文件的文件夹下的 \bin\Debug 文件夹。

## <a name="test-the-project-property"></a>测试项目属性
 现在可以测试自定义项目属性了。 在 的实验实例中调试和测试新项目属性扩展是最简单的 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 方法。 此实例 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 是在运行 VSIX 或其他扩展性项目时创建的。 调试项目后，可以在系统上安装该扩展，然后继续在的一个实例中对其进行调试和测试 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

#### <a name="to-debug-and-test-the-extension-in-an-experimental-instance-of-visual-studio"></a>在的实验实例中调试和测试扩展 Visual Studio

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]用管理凭据重新启动，然后打开 ProjectExtensionPackage 解决方案。

2. 通过选择 **F5** 键，或在菜单栏上选择 "**调试**" "  >  **启动调试**"，启动项目的调试版本。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]安装%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Custom Project Property\1.0 的扩展，并启动实验实例 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

3. 在的实验实例中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，为场解决方案创建 SharePoint 项目，并使用向导中其他值的默认值。

    1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

    2. 在 "**新建 Project** " 对话框的顶部，选择 .NET Framework 版本列表中 **.NET Framework 3.5** 。

         SharePoint 工具扩展需要此版本中的功能 [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)] 。

    3. 在 "**模板**" 节点下，展开 " **Visual c #** " 或 " **Visual Basic** " 节点，选择 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

    4. 选择 **SharePoint 2010 Project** 模板，然后输入 **ModuleTest** 作为项目名称。

4. 在 **解决方案资源管理器** 中，选择 " **ModuleTest** " 项目节点。

     "**属性**" 窗口中将显示一个新的自定义属性 "**地图图像" 文件夹**，默认值为 " **False**"。

5. 将该属性的值更改为 **True**。

     将映像资源文件夹添加到 SharePoint 项目。

6. 将该属性的值更改回 **False**。

     如果在 "**删除图像" 文件夹** 中选择 "**是"** 按钮，则会从 SharePoint 项目中删除 images 资源文件夹。

7. 关闭 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的实验实例。

## <a name="see-also"></a>请参阅
- [扩展 SharePoint 项目](../sharepoint/extending-sharepoint-projects.md)
- [如何：将属性添加到 SharePoint 项目中](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [SharePoint 项目系统类型和其他 Visual Studio 项目类型之间进行转换](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
- [在 SharePoint 项目系统的扩展中保存数据](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)
- [将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)