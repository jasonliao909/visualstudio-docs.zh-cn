---
title: 为项目创建自定义SharePoint步骤
description: 在此演练中，请创建自定义部署步骤，SharePoint运行 SharePoint 的服务器上升级项目SharePoint。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands
- SharePoint development in Visual Studio, extending deployment
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 4e445ecbc48abfd91149d45af7adb19eeaa7fe03
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122092704"
---
# <a name="walkthrough-create-a-custom-deployment-step-for-sharepoint-projects"></a>演练：为项目创建SharePoint步骤
  部署项目SharePoint，Visual Studio以特定顺序执行一系列部署步骤。 Visual Studio包括许多内置部署步骤，但也可以创建自己的部署步骤。

 本演练将创建自定义部署步骤，以升级运行 SharePoint。 Visual Studio包括许多任务的内置部署步骤，例如收回或添加解决方案，但不包括用于升级解决方案的部署步骤。 默认情况下，在部署 SharePoint解决方案时，Visual Studio先收回解决方案 (如果已部署) 则重新部署整个解决方案。 有关内置部署步骤详细信息，请参阅部署、发布和升级SharePoint[包](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)。

 本演练演示了下列任务：

- 创建一Visual Studio执行两个主要任务的扩展：

  - 该扩展定义了用于升级解决方案SharePoint步骤。

  - 该扩展创建一个项目扩展，用于定义新的部署配置，这是为给定项目执行的一组部署步骤。 新的部署配置包括自定义部署步骤和几个内置部署步骤。

- 创建扩展SharePoint调用的两个自定义命令。 SharePoint命令是扩展程序集可调用的方法，以在服务器对象模型中使用 API 进行SharePoint。 有关详细信息，请参阅[调用对象SharePoint模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

- 使用 VSIX Visual Studio生成 () 扩展以部署这两个程序集。

- 测试新的部署步骤。

## <a name="prerequisites"></a>必备条件
 需要开发计算机上以下组件才能完成本演练：

- 支持的 Windows、SharePoint 和 Visual Studio 版本。

- Visual Studio SDK。 本演练使用 SDK 中的 **VSIX Project** 模板创建 VSIX 包来部署扩展。 有关详细信息，请参阅扩展 SharePoint[中的 Visual Studio。](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)

  了解以下概念有助于完成演练，但这不是必需的：

- 使用服务器对象模型SharePoint。 有关详细信息，请参阅使用[SharePoint Foundation Server-Side 对象模型](/previous-versions/office/developer/sharepoint-2010/ee538251(v=office.14))。

- SharePoint解决方案。 有关详细信息，请参阅解决方案 [概述](/previous-versions/office/developer/sharepoint-2010/aa543214(v=office.14))。

- 升级SharePoint解决方案。 有关详细信息，请参阅 [升级解决方案](/previous-versions/office/developer/sharepoint-2010/aa543659(v=office.14))。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，必须创建三个项目：

- 一个 VSIX 项目，用于创建 VSIX 包以部署扩展。

- 实现 扩展的类库项目。 此项目必须面向 .NET Framework 4.5。

- 一个类库项目，用于定义自定义SharePoint命令。 此项目必须面向 .NET Framework 3.5。

  通过创建项目来开始演练。

#### <a name="to-create-the-vsix-project"></a>创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

3. 在 **"新建Project"** 对话框中，展开 **Visual C#** 或Visual Basic **节点，** 然后选择"**扩展性"** 节点。

    > [!NOTE]
    > "**扩展性"** 节点仅在安装 Visual Studio SDK 时可用。 有关详细信息，请参阅本主题前面的先决条件部分。

4. 在对话框顶部，在.NET Framework **版本列表中选择"4.5".NET Framework。**

5. 选择 **VSIX Project** 模板，将项目命名 **UpgradeDeploymentStep**，然后选择"确定 **"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将 **UpgradeDeploymentStep 项目** 添加到 **解决方案资源管理器。**

#### <a name="to-create-the-extension-project"></a>创建扩展项目

1. 在 **解决方案资源管理器** 中，打开 UpgradeDeploymentStep 解决方案节点的快捷菜单，选择"添加"，然后选择"新建 **Project"。**

2. 在"**新建Project"** 对话框中，展开 **Visual C#** **或** Visual Basic节点，然后选择 **Windows节点。**

3. 在对话框顶部，在.NET Framework **版本列表中选择"4.5".NET Framework。**

4. 选择" **类库** "项目模板，将项目 **"DeploymentStepExtension"** 命名，然后选择"确定 **"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **DeploymentStepExtension** 项目添加到解决方案，并打开默认的 Class1 代码文件。

5. 从项目中删除 Class1 代码文件。

#### <a name="to-create-the-sharepoint-command-project"></a>创建 SharePoint 命令项目

1. 在 **解决方案资源管理器** 中，打开 UpgradeDeploymentStep 解决方案节点的快捷菜单，选择"添加"，然后选择"新建 **Project"。**

2. 在"**新建Project"** 对话框中，展开 **"Visual C#"** 或 **Visual Basic"，** 然后选择 **Windows节点。**

3. 在对话框顶部，选择.NET Framework **版本列表中的"3.5** .NET Framework" 。

4. 选择类 **库** 项目模板，将项目命名 **SharePointCommands**，然后选择"确定 **"** 按钮。

     Visual Studio **SharePointCommands** 项目添加到解决方案，并打开默认的 Class1 代码文件。

5. 从项目中删除 Class1 代码文件。

## <a name="configure-the-projects"></a>配置项目
 在编写代码以创建自定义部署步骤之前，必须添加代码文件和程序集引用，并且必须配置项目。

#### <a name="to-configure-the-deploymentstepextension-project"></a>配置 DeploymentStepExtension 项目

1. 在 **DeploymentStepExtension** 项目中，添加两个具有以下名称的代码文件：

    - UpgradeStep

    - DeploymentConfigurationExtension

2. 打开 DeploymentStepExtension 项目的快捷菜单，然后选择"添加 **引用"。**

3. 在" **框架** "选项卡上，选中"System.ComponentModel.Composition"程序集的复选框。

4. 在"**扩展"** 选项卡上，选中"Microsoft.VisualStudio"的复选框。SharePoint，然后选择"确定 **"** 按钮。

#### <a name="to-configure-the-sharepointcommands-project"></a>配置 SharePointCommands 项目

1. 在 **SharePointCommands** 项目中，添加名为 Commands 的代码文件。

2. 在 **解决方案资源管理器** 中，打开 **SharePointCommands** 项目节点上的快捷菜单，然后选择"**添加引用"。**

3. 在 **"扩展"** 选项卡上，选中以下程序集的复选框，然后单击"确定 **"** 按钮

    - 微软。SharePoint

    - Microsoft.VisualStudio。SharePoint。命令

## <a name="define-the-custom-deployment-step"></a>定义自定义部署步骤
 创建定义升级部署步骤的类。 若要定义部署步骤，类实现 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep> 接口。 每当要定义自定义部署步骤时，都实现此接口。

#### <a name="to-define-the-custom-deployment-step"></a>定义自定义部署步骤

1. 在 **DeploymentStepExtension** 项目中，打开 UpgradeStep 代码文件，然后将以下代码粘贴到该文件中。

    > [!NOTE]
    > 添加此代码后，项目将发生一些编译错误，但在稍后的步骤中添加代码时，这些错误将消失。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/upgradestep.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/upgradestep.vb" id="Snippet1":::

## <a name="create-a-deployment-configuration-that-includes-the-custom-deployment-step"></a>创建包含自定义部署步骤的部署配置
 为新的部署配置创建项目扩展，其中包括多个内置部署步骤和新的升级部署步骤。 通过创建此扩展，SharePoint开发人员在项目中使用升级SharePoint步骤。

 若要创建部署配置，类实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 接口。 每当要创建项目扩展时，SharePoint接口。

#### <a name="to-create-the-deployment-configuration"></a>创建部署配置

1. 在 **DeploymentStepExtension** 项目中，打开 DeploymentConfigurationExtension 代码文件，然后将以下代码粘贴到该文件中。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/deploymentconfigurationextension.cs" id="Snippet2":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/deploymentconfigurationextension.vb" id="Snippet2":::

## <a name="create-the-custom-sharepoint-commands"></a>创建自定义SharePoint命令
 创建两个自定义命令，用于调用服务器对象模型SharePoint。 一个命令确定是否已部署解决方案;另一个命令升级解决方案。

#### <a name="to-define-the-sharepoint-commands"></a>定义SharePoint命令

1. 在 **SharePointCommands** 项目中，打开"命令"代码文件，然后将以下代码粘贴到该文件中。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/SharePointCommands/Commands.cs" id="Snippet4":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/sharepointcommands/commands.vb" id="Snippet4":::

## <a name="checkpoint"></a>Checkpoint
 在演练的此时，自定义部署步骤和 SharePoint 命令的所有代码现在都位于项目中。 生成它们以确保编译时不会出错。

#### <a name="to-build-the-projects"></a>生成项目

1. 在 **解决方案资源管理器** 中，打开 **DeploymentStepExtension** 项目的快捷菜单，然后选择"生成 **"。**

2. 打开 **SharePointCommands 项目的快捷菜单**，然后选择"生成 **"。**

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>创建 VSIX 包以部署扩展
 若要部署扩展，请使用解决方案中的 VSIX 项目创建 VSIX 包。 首先，通过修改 VSIX 项目中的 source.extension.vsixmanifest 文件来配置 VSIX 包。 然后通过生成解决方案来创建 VSIX 包。

#### <a name="to-configure-and-create-the-vsix-package"></a>配置和创建 VSIX 包

1. 在 **解决方案资源管理器** 中，在 **UpgradeDeploymentStep** 项目下，打开 **source.extension.vsixmanifest** 文件的快捷菜单，然后选择"打开 **"。**

     Visual Studio在清单编辑器中打开文件。 source.extension.vsixmanifest 文件是所有 VSIX 包都需要的 extension.vsixmanifest 文件的基础。 有关此文件的信息，请参阅 [VSIX 扩展架构 1.0 参考](/previous-versions/dd393700(v=vs.110))。

2. 在"**产品名称"** 框中，**输入"升级部署步骤SharePoint项目"。**

3. 在"**创作"** 框中，输入 **"Contoso"。**

4. 在"**说明**"框中 **，输入"提供** 可在项目中使用的自定义升级SharePoint步骤。

5. 在编辑器 **的"** 资产"选项卡中，选择"新建 **"** 按钮。

     将出现 **"添加新资产** "对话框。

6. 在"**类型"** 列表中，选择 **"Microsoft.VisualStudio.MefComponent"。**

    > [!NOTE]
    > 此值对应于 `MefComponent` extension.vsixmanifest 文件中的元素。 此元素指定 VSIX 包中扩展程序集的名称。 有关详细信息，请参阅[MEFComponent 元素 (VSX 架构) 。 ](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))

7. 在" **源"** 列表中， **选择当前解决方案 中的项目**。

8. 在 **"Project"** 列表中，选择 **"DeploymentStepExtension"，** 然后选择"确定 **"** 按钮。

9. 在清单编辑器中，再次 **选择"新建"** 按钮。

     将出现 **"添加新资产** "对话框。

10. 在"**类型"** 列表中，输入 **SharePoint。Commands.v4**。

    > [!NOTE]
    > 此元素指定要包括在扩展插件中的自定义扩展Visual Studio扩展。 有关详细信息，请参阅[ASSET Element (VSX Schema) 。 ](/previous-versions/dd393737(v=vs.110))

11. 在" **源"** 列表中， **选择当前解决方案 中的项目**。

12. 在 **"Project"** 列表中，选择 **"SharePointCommands"，** 然后选择"确定 **"** 按钮。

13. 在菜单栏上，选择"**生成** 生成解决方案"，并确保解决方案  >  编译时不会出错。

14. 确保 UpgradeDeploymentStep 项目的生成输出文件夹现在包含 UpgradeDeploymentStep.vsix 文件。

     默认情况下，生成输出文件夹为 。包含项目文件的文件夹下的 \bin\Debug 文件夹。

## <a name="prepare-to-test-the-upgrade-deployment-step"></a>准备测试升级部署步骤
 若要测试升级部署步骤，必须先将示例解决方案部署到 SharePoint 站点。 首先，在 Visual Studio 试验实例中调试扩展。 然后创建列表定义和列表实例以用于测试部署步骤，然后将它们部署到SharePoint站点。 接下来，修改列表定义和列表实例并重新部署它们，以演示默认部署过程如何覆盖SharePoint解决方案。

 本演练稍后将修改列表定义和列表实例，然后在 SharePoint 升级它们。

#### <a name="to-start-debugging-the-extension"></a>开始调试扩展

1. 重启Visual Studio管理凭据，然后打开 UpgradeDeploymentStep 解决方案。

2. 在 DeploymentStepExtension 项目中，打开 UpgradeStep 代码文件，然后将断点添加到 和 方法的第一行 `CanExecute` `Execute` 代码。

3. 通过选择 **F5** 键或在菜单栏上选择"调试开始调试"  >  **来开始调试**。

4. Visual Studio将扩展安装到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Upgrade Deployment Step for SharePoint Projects\1.0 并启动 Visual Studio 的实验实例。 你将在此实例中测试升级部署Visual Studio。

#### <a name="to-create-a-sharepoint-project-with-a-list-definition-and-a-list-instance"></a>使用列表SharePoint列表实例创建项目

1. 在 Visual Studio 实验实例中的菜单栏上，选择"文件""新建  >    >  **Project"。**

2. 在 **"新建Project"** 对话框中，展开 **"Visual C#"** 节点或Visual Basic节点，展开"SharePoint"节点，然后选择 **"2010"** 节点。 

3. 在对话框顶部，确保 .NET Framework **3.5** 出现在版本列表中.NET Framework。

    和 的项目 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] 需要此版本的 .NET Framework。

4. 在项目模板列表中，选择 **"SharePoint 2010** Project"，将项目命名 **EmployeesListDefinition**，然后选择"确定 **"** 按钮。

5. 在 **SharePoint自定义向导**"中，输入要用于调试的站点的 URL。

6. 在 **"此解决方案的信任级别是什么SharePoint，** 选择"部署 **为场解决方案"** 选项按钮。

   > [!NOTE]
   > 升级部署步骤不支持沙盒解决方案。

7. 选择 **“完成”** 按钮。

    [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建 EmployeesListDefinition 项目。

8. 打开 EmployeesListDefinition 项目的快捷菜单，选择"**添加**"，然后选择"**新建项"。**

9. 在"**添加新项 - EmployeesListDefinition"** 对话框中，展开 **"SharePoint"节点**，然后选择 **"2010"** 节点。

10. 选择" **列表** 项"模板，将项"员工 **列表**"命名，然后选择"添加 **"** 按钮。

     将显示SharePoint自定义向导

11. 在"**选择列表设置** 页上，验证以下设置，然后选择"完成 **"** 按钮：

    1. **"员工列表** " **显示在"要为列表显示什么名称？"** 框中。

    2. 选择 **"基于以下项创建可** 自定义列表"选项按钮。

    3. **默认 (") "** 基于以下项创建可 **自定义列表"列表中** 选择了"空白区域"。

       [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建具有标题列和单个空实例的员工列表项，并打开列表设计器。

12. 在列表设计器的"列"选项卡上，选择"键入新的或现有的列名行"，然后在"列显示名称"列表中 **添加以下** 列：

    1. 名字

    2. Company

    3. 商务电话

    4. 电子邮件

13. 保存所有文件，然后关闭列表设计器。

14. 在 **解决方案资源管理器** 中，展开" **员工列表"** 节点，然后展开" **员工列表实例"** 子节点。

15. 在 *Elements.xml* 文件中，将此文件中的默认 XML 替换为以下 XML。 此 XML 将列表的名称更改为 **Employees，** 并添加名为 Jim Hance 的员工的信息。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <ListInstance Title="Employees"
                    OnQuickLaunch="TRUE"
                    TemplateType="10000"
                    Url="Lists/Employees"
                    Description="Simple list to test upgrade deployment step">
        <Data>
          <Rows>
            <Row>
              <Field Name="Title">Hance</Field>
              <Field Name="FirstName">Jim</Field>
              <Field Name="Company">Contoso</Field>
              <Field Name="Business Phone">555-555-5555</Field>
              <Field Name="E-Mail">jim@contoso.com</Field>
            </Row>
          </Rows>
        </Data>
      </ListInstance>
    </Elements>
    ```

16. 保存并关闭 *Elements.xml* 文件。

17. 打开 EmployeesListDefinition 项目的快捷菜单，然后选择"**打开"或**"属性 **"。**

     "属性设计器"随即打开。

18. 在 **"SharePoint"** 选项卡上，清除"调试后自动收回 **"复选框，** 然后保存属性。

#### <a name="to-deploy-the-list-definition-and-list-instance"></a>部署列表定义和列表实例

1. 在 **解决方案资源管理器"** 中，选择 **"EmployeesListDefinition"** 项目节点。

2. 在"**属性**"窗口中，确保"**活动部署配置**"属性设置为"默认 **"。**

3. 选择 **F5** 键，或在菜单栏上选择"**调试**  >  **开始调试"。**

4. 验证项目是否成功生成、Web 浏览器是否打开到 SharePoint 站点、快速启动 栏中的"列表"项是否包括"新员工"列表，以及"员工"列表是否包含Jim Hance 的条目。 

5. 关闭 Web 浏览器。

#### <a name="to-modify-the-list-definition-and-list-instance-and-redeploy-them"></a>修改列表定义和列表实例并重新部署它们

1. 在 EmployeesListDefinition 项目中，Elements.xml"员工列表实例"项目项的 **子级文件**。 

2. 删除 `Data` 元素及其子元素，以从列表中删除 Jim Hance 的条目。

     完成后，该文件应包含以下 XML。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <ListInstance Title="Employees"
                    OnQuickLaunch="TRUE"
                    TemplateType="10000"
                    Url="Lists/Employees"
                    Description="Simple list to test upgrade deployment step">
      </ListInstance>
    </Elements>
    ```

3. 保存并关闭 *Elements.xml* 文件。

4. 打开"员工列表"项目项 **的** 快捷菜单，然后选择"**打开"或**"属性 **"。**

5. 在"列表设计器"中，选择" **视图"** 选项卡。

6. 在" **所选列"** 列表中，选择" **附件**"，然后选择<键以将列移动到"可用 **列"** 列表。

7. 重复上一步，将"业务电话"列 **从"所选** 列"列表移动到"可用 **列"** 列表。

     此操作会从站点中的"员工"列表的默认视图中删除SharePoint字段。

8. 通过选择 **F5** 键或在菜单栏上选择"调试开始调试"  >  **来开始调试**。

9. 验证是否 **显示"部署冲突** "对话框。

     当用户尝试将Visual Studio解决方案 (列表实例) 部署到SharePoint已部署到的站点时，将显示此对话框。 本演练稍后执行升级部署步骤时，不会显示此对话框。

10. 在" **部署冲突** "对话框中，选择" **自动解决"** 选项按钮。

     Visual Studio删除 SharePoint 站点上的列表实例，在项目中部署列表项，然后打开SharePoint站点。

11. 在 **栏的** "快速启动"部分中，选择" **员工** "列表，然后验证以下详细信息：

    - "**附件****电话** 主页"列不会出现在此列表视图中。

    - 该列表为空。 使用默认 **部署配置** 重新部署解决方案时，"员工"列表已替换为项目中的新空列表。

## <a name="test-the-deployment-step"></a>测试部署步骤
 现在可以测试升级部署步骤。 首先，将项添加到 SharePoint 中的列表实例。 然后更改列表定义和列表实例，在 SharePoint 站点上升级它们，并确认升级部署步骤不会覆盖新项。

#### <a name="to-manually-add-an-item-to-the-list"></a>手动将项添加到列表

1. 在 SharePoint 站点的功能区中的"列表工具"选项卡下，选择"**项"** 选项卡。

2. 在"新建 **"** 组中，选择"**新建项"。**

     或者，可以在项列表本身 **中选择"添加新** 项"链接。

3. 在"**员工 - 新建项**"窗口的"**标题"框中**，输入 **"Facilities Manager"。**

4. 在" **名字"框中** ，输入 **Andy**。

5. 在"**公司"** 框中，键入 **"Contoso"。**

6. 选择" **保存** "按钮，验证新项是否显示在列表中，然后关闭 Web 浏览器。

     本演练稍后将使用此项来验证升级部署步骤是否未覆盖此列表的内容。

#### <a name="to-test-the-upgrade-deployment-step"></a>测试升级部署步骤

1. 在 Visual Studio 实验实例 **解决方案资源管理器，打开** **EmployeesListDefinition** 项目节点的快捷菜单，然后选择"属性 **"。**

    "属性编辑器/设计器"随即打开。

2. 在 **"SharePoint"** 选项卡上，将 **"活动部署配置"属性** 设置为"**升级"。**

    此自定义部署配置包括新的升级部署步骤。

3. 打开"员工列表"项目项 **的** 快捷菜单，然后选择"属性 **"或**"打开 **"。**

    "属性编辑器/设计器"随即打开。

4. 在"**视图**"选项卡上，选择"**电子邮件**"列，然后选择用于将列从"所选列"列表移动到" **<** 可用列 **"列表** 的键。 

    此操作会从站点中的"员工"列表的默认视图中删除SharePoint字段。

5. 通过选择 **F5** 键或在菜单栏上选择"调试开始调试"  >  **来开始调试**。

6. 验证其他 实例中的代码Visual Studio在之前在 方法中设置的断 `CanExecute` 点处停止。

7. 再次选择 **F5** 键，或在菜单栏上选择"**调试继续**  >  **"。**

8. 验证代码是否停止于之前在 方法中设置的断 `Execute` 点。

9. 选择 **F5** 键，或在菜单栏上选择"**调试**  >  **""继续** 最后一次"。

     Web 浏览器将打开SharePoint站点。

10. 在 **"员工** "快速启动"部分中，选择" **员工"** 列表，然后验证以下详细信息：

    - 前面为 Andy 手动添加 (，"设施管理器") 仍在列表中。

    - **"电话"** 列和"**电子邮件地址**"列不会出现在此列表视图中。

      升级 **部署** 配置修改 **现有站点中的** 现有员工SharePoint实例。 如果使用了默认 **部署** 配置而不是 **升级配置，** 则会遇到部署冲突。 Visual Studio替换"员工"列表来解决冲突，而设施经理 Andy 的项将被删除。

## <a name="clean-up-the-development-computer"></a>清理开发计算机
 完成升级部署步骤测试后，从 SharePoint 站点中删除列表实例和列表定义，并从该站点中删除部署Visual Studio。

#### <a name="to-remove-the-list-instance-from-the-sharepoint-site"></a>从站点中删除SharePoint实例

1. 如果 **该列表** 尚未打开SharePoint，请打开该站点上的"员工"列表。

2. 在 SharePoint 站点的功能区中，选择"列表 **工具**"选项卡，然后选择"**列表"** 选项卡。

3. 在 **"设置"** 组中，选择"**列出设置** 项。

4. 在 **"权限和管理"** 下，选择"删除此列表"命令，选择"确定"以确认想要将列表发送到回收站，然后关闭 Web 浏览器。

#### <a name="to-remove-the-list-definition-from-the-sharepoint-site"></a>从站点中删除SharePoint定义

1. 在实验实例的 Visual Studio菜单栏上，选择"生成 **收回**  >  **"。**

     Visual Studio从站点收回SharePoint定义。

#### <a name="to-uninstall-the-extension"></a>卸载扩展

1. 在 Visual Studio实验实例的菜单栏上，选择"**工具**  >  **扩展和更新"。**

     此时，“扩展和更新”对话框打开。

2. 在扩展列表中，为"项目"选择"升级 **SharePoint步骤"，** 然后选择"**卸载"** 命令。

3. 在出现的对话框中，选择"是"以确认要卸载扩展，然后选择"立即重启"以完成卸载。 

4. 关闭实验Visual Studio (实例和 Visual Studio，其中 UpgradeDeploymentStep 解决方案在) 。

## <a name="see-also"></a>请参阅
- [扩展SharePoint打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)