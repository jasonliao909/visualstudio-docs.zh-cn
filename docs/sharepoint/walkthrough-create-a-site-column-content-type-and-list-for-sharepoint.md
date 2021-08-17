---
title: 为用户创建站点列、内容类型和SharePoint
titleSuffix: ''
description: 在此演练中，请创建一个自定义站点列 (字段) 、使用站点列的自定义内容类型，以及使用 SharePoint 中内容类型的列表。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.ListDesigner.GeneralMessageHelp
- Microsoft.VisualStudio.SharePoint.Designers.ListDesigner.ViewModels.ListViewModel.SortingAndGrouping
- VS.SharePointTools.ListDesigner.SortingGrouping
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, list definitions
- SharePoint development in Visual Studio, list instances
- SharePoint development in Visual Studio, fields
- SharePoint development in Visual Studio, content types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: aafbee5bd508930b2b7f5f260977791d0c111c2a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122092734"
---
# <a name="walkthrough-create-a-site-column-content-type-and-list-for-sharepoint"></a>演练：创建 SharePoint 的网站栏、内容类型和列表
  以下过程演示如何创建自定义SharePoint或字段）以及使用站点列的内容类型。  它还演示如何创建使用新内容类型的列表。

 本演练包含以下任务：

- [创建自定义站点列](#create-custom-site-columns)。

- [创建自定义内容类型](#create-a-custom-content-type)。

- [创建列表](#create-a-list)。

- [测试应用程序](#test-the-application)。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 支持的 Windows 和 SharePoint 版本。

- [!INCLUDE[vsprvs-current](../sharepoint/includes/vsprvs-current-md.md)]

## <a name="create-custom-site-columns"></a>创建自定义站点列
 此示例创建一个列表，用于管理医院中的患者。 首先，必须在 中SharePoint一个站点项目 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，并添加站点列，如下所示。

#### <a name="to-create-the-project"></a>创建项目

1. 在"文件 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] **"菜单** 上，选择"**新建**  >  Project"。
::: moniker range="=vs-2017"
2. 在"**新建Project"** 对话框中的 **"Visual C#"** 或"Visual Basic"下，展开"Office/SharePoint"节点，然后选择"SharePoint **解决方案"。**  

3. 在"**模板"** 窗格中，SharePoint已安装 **Project特定版本的**"空SharePoint" 。 例如，如果安装了 2016 SharePoint，请选择"SharePoint **2016 - 空** Project模板。  

4. 将项目的名称更改为 **"Clinic"，** 然后选择"确定 **"** 按钮。

5. 在 **"指定** 用于调试的站点和安全级别"对话框中，输入要添加新自定义字段项的本地 SharePoint 站点的 URL，或使用默认位置 (`http://<` *SystemName* `>/)` 。

6. 在 **"此解决方案的信任级别SharePoint？"** 部分中，使用默认值"部署 **为沙盒解决方案"。**

     有关沙盒和场解决方案的详细信息，请参阅 [沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

7. 选择 **“完成”** 按钮。 项目现在列在 **解决方案资源管理器。**
::: moniker-end
::: moniker range=">=vs-2019"
2.  在"**创建新Project"对话框中**，SharePoint已安装Project特定版本的SharePoint"空"选项。 例如，如果安装了 2016 SharePoint，请选择"SharePoint **2016 - 空** Project模板。
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

3. 将项目的名称更改为 **"Clinic"，** 然后选择"创建 **"** 按钮。

4. 在 **"指定** 用于调试的站点和安全级别"对话框中，输入要添加新自定义字段项的本地 SharePoint 站点的 URL，或使用默认位置 (`http://<` *SystemName* `>/)` 。

5. 在 **"此解决方案的信任级别SharePoint？"** 部分中，使用默认值"部署 **为沙盒解决方案"。**

     有关沙盒和场解决方案的详细信息，请参阅 [沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

6. 选择 **“完成”** 按钮。 项目现在列在 **解决方案资源管理器。**
::: moniker-end

#### <a name="to-add-site-columns"></a>添加站点列

1. 添加新的站点列。 为此，请在 **"解决方案资源管理器"中** 右键单击 **"Clinic"** 项目，然后选择"**添加新**  >  **项"。**

2. 在" **添加新项"对话框中** ，选择" **站点** 列"，将名称更改为 **PatientName**，然后选择"添加 **"** 按钮。

3. 在站点列的Elements.xml文件中，将"类型"设置保留为 **"** 文本 *"，* 将"组"设置更改为 **"临床站点列"。** 完成后，站点 *列Elements.xml文件* 应如以下示例所示。

    ```xml
    <Field
         ID="{f9ba60d1-5631-41fb-b016-a38cf48eef63}"
         Name="PatientName"
         DisplayName="Patient Name"
         Type="Text"
         Required="FALSE"
         Group="Clinic Site Columns">
    </Field>
    ```

    > [!TIP]
    > Visual Studio站点列的名称使用 camel 大小写，则系统会自动在 DisplayName 中添加一个空格。
    > 建议不要将空格用于"站点列名称"，因为尝试将解决方案部署到站点列名称时SharePoint。

4. 使用相同的过程，向项目再添加两个站点列 **：PatientID** (Type = "Integer") **和 DoctorName** (Type = "Text") 。 将"组"值设置为 **"Clinic 站点列"。**

## <a name="create-a-custom-content-type"></a>创建自定义内容类型
 接下来，根据"联系人"内容类型创建一个内容类型，其中包括在上一过程中创建的站点列。 将内容类型基于现有内容类型可以节省时间，因为基本内容类型提供了多个站点列用于新内容类型。

#### <a name="to-create-a-custom-content-type"></a>创建自定义内容类型

1. 向项目添加内容类型。 为此，**请选择解决方案资源管理器节点**

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 在 **Visual C#** 或 **Visual Basic** 下，展开 **SharePoint节点，** 然后选择 **"2010"** 节点。

4. 在" **模板"** 窗格中，选择" **内容类型** "模板，将名称更改为 **"患者** 信息"，然后选择"添加 **"** 按钮。

     随即 **SharePoint自定义向导**。

5. 在"**此内容类型应** 继承自哪个基内容类型"列表中，选择"联系人"作为新内容类型的基础内容类型，然后选择"完成 **"** 按钮。

     这样做可以访问"联系人"内容类型中其他可能有用的站点列，以及之前定义的站点列。

6. 显示内容类型设计器后，在"列"选项卡中，添加之前定义的三个站点 **列：患者** 名称、**患者 ID** 和 **医生名称**。 若要添加这些列，请选择"显示名称"下的站点列列表中的第一个列表框，然后一次选择列表中的每个站点列。

    > [!TIP]
    > 若要更快速地选择站点列，请通过输入列名的前几个字母来筛选列表。

7. 除了三个自定义站点列，请 **从站点列** 列表中添加"注释站点"列。

8. 选中" **患者姓名** " **和"患者** **ID"** 站点列的"必需"复选框，使它们成为必填字段。

9. 在"**内容类型**"选项卡上，确保内容类型名称为 **"患者** 信息"，然后将说明更改为 **"患者信息卡"。**

10. 将 **"组名称****"更改为"临床** 内容类型"，并保留其他设置默认值。

11. 在菜单栏上，选择"**文件**  >  **全部保存**"，然后关闭"内容类型"设计器。

## <a name="create-a-list"></a>创建列表
 现在，创建使用新内容类型和站点列的列表。

#### <a name="to-create-a-list"></a>创建列表

1. 向项目添加列表。 为此， **请选择解决方案资源管理器节点**。

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 在 **Visual C#** 或 **Visual Basic** 下，**展开SharePoint节点**。

4. 在" **模板"** 窗格中，选择" **列表"** 模板，将名称更改为 **"患者**"，然后选择"添加 **"** 按钮。

5. 将" **基于自定义列表"设置** 保留为"默认 (**列表) "，** 然后选择"完成 **"** 按钮。

6. 在列表设计器中，选择"**内容类型**"按钮以显示"内容类型 **设置** 对话框。

7. 选择新行，在内容类型列表中选择 **"患者信息** "内容类型，然后选择"确定 **"** 按钮。

     执行此操作会将"患者信息" **内容类型的所有** 站点列添加到列表中。

8. 删除列表中除以下列之外的所有站点列：

    - 患者 ID

    - 患者姓名

    - 住宅电话

    - 电子邮件

    - 医生姓名

    - 注释

9. 在 **"列显示名称**"下，选择一个空行，添加一个自定义列表列，将其命名为 **"医院"。** 将数据类型保留为 **"单行文本"。**

     自定义列表列仅适用于此列表。 将自定义列表列添加到列表时，将创建一个新的列表内容类型（包括添加到列表中的所有列）并设置为默认列表。

    > [!TIP]
    > 如果从站点列列表中选择列，则使用现有站点列。 但是，如果在未在列表中选择任何列的情况下输入列名称值，则即使列表中已存在同名的列，也创建一个自定义列表列。

     （可选）可以改为将自定义列表列的数据类型设置为"查找"，而不是将自定义列表列的数据类型设置为"单行文本"，而是从表或其他列表中检索其值。  有关查找列的信息，请参阅 SharePoint [2010](/previous-versions/msp-n-p/ff798514(v=pandp.10))中的列表关系和[查找和列表关系](/previous-versions/office/developer/sharepoint-2010/ff623048(v=office.14))。

10. 在" **患者 ID"和** " **患者名称** "框旁边，选中" **必需** "复选框。

11. 在" **视图"** 选项卡上，选择一个空行以创建视图。 在 **"查看名称** "列下的空白行 **中输入患者** 详细信息。

     在 **"视图**"选项卡上，可以指定要显示在"视图"列表中的SharePoint列。

12. 选择新的" **患者详细信息"** 行，然后选择" **设置为默认"** 按钮。

     新视图现在是列表的默认视图。

13. 按以下顺序将以下列 **添加到"** 所选列"列表中：

    - 患者 ID

    - 患者名称

    - 住宅电话

    - 电子邮件

    - 医生名称

    - 医院

    - 注释

14. 在 " **属性** " 列表中，选择 " **排序和分组** " 属性，然后选择省略号按钮 ![省略号图标](../sharepoint/media/ellipsisicon.gif "“省略号”图标") 以显示 " **排序和分组** " 对话框。

15. 在 " **列名称** " 列表中，选择 " **患者名称**"，确保 " **排序依据** " 列设置为 " **升序**"，然后选择 **"确定"** 按钮。

## <a name="test-the-application"></a>测试应用程序
 自定义网站列、内容类型和列表就绪后，请将其部署到 SharePoint，并运行应用程序进行测试。

#### <a name="to-test-the-application"></a>测试应用程序

1. 在菜单栏上，依次选择“文件” > “全部保存”。

2. 选择 **F5** 键以运行应用程序。

     将编译应用程序，然后将其功能部署到 SharePoint 和激活。

3. 在快速导航栏上，选择 " **患者** " 链接以显示 **患者** 列表。

     列表中的列名应与您在中的 " **视图** " 选项卡上输入的名称相匹配 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

4. 选择 " **添加新项** " 链接以创建患者信息卡。

5. 在字段中输入信息，然后选择 " **保存** " 按钮。

     新记录将显示在列表中。

## <a name="see-also"></a>请参阅
- [创建 SharePoint 的站点栏、内容类型和列表](../sharepoint/creating-site-columns-content-types-and-lists-for-sharepoint.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [如何：创建自定义字段类型](/previous-versions/office/developer/sharepoint-2010/bb862248(v=office.14))
- [内容类型](/previous-versions/office/developer/sharepoint-2010/ms479905(v=office.14))
- [“列”](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))
