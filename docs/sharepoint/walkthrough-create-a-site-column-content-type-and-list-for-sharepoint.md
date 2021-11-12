---
title: 创建 SharePoint 网站栏、内容类型和列表
titleSuffix: ''
description: 在本演练中，将在 SharePoint 中创建一个自定义网站栏（字段）、使用网站栏的自定义内容类型，以及使用内容类型的列表。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665007"
---
# <a name="walkthrough-create-a-site-column-content-type-and-list-for-sharepoint"></a>演练：创建 SharePoint 的网站栏、内容类型和列表
  下面的过程演示如何创建自定义 SharePoint 网站栏或字段，以及使用网站栏的内容类型。 它还演示如何创建列表来使用新内容类型。

 本演练包含以下任务：

- [创建自定义网站栏](#create-custom-site-columns)。

- [创建自定义内容类型](#create-a-custom-content-type)。

- [创建列表](#create-a-list)。

- [测试应用程序](#test-the-application)。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 支持的 Windows 和 SharePoint 版本。

- [!INCLUDE[vsprvs-current](../sharepoint/includes/vsprvs-current-md.md)]

## <a name="create-custom-site-columns"></a>创建自定义网站栏
 此示例将创建一个列表，用于管理医院中的患者。 首先，必须在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中创建 SharePoint 项目并向其添加网站栏，如下所示。

#### <a name="to-create-the-project"></a>创建项目

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]“文件”菜单上，选择“新建” > “项目”  。
::: moniker range="=vs-2017"
2. 在“新建项目”对话框中，展开 Visual C# 或 Visual Basic 下的 Office/SharePoint 节点，然后选择“SharePoint 解决方案”    。

3. 在“模板”窗格中，为已安装的 SharePoint 的特定版本选择“SharePoint 空项目” 。 例如，如果安装了 SharePoint 2016，请选择“SharePoint 2016 - 空项目”模板。  

4. 将项目名称更改为“诊所”，然后选择“确定”按钮 。

5. 在“指定用于调试的网站和安全级别”对话框中，输入要向其添加新自定义字段项的本地 SharePoint 网站的 URL，或使用默认位置 (`http://<`SystemName`>/)`。

6. 在“此 SharePoint 解决方案的信任级别是什么?”部分中，使用默认值“部署为沙盒解决方案” 。

     有关沙盒解决方案与场解决方案的详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

7. 选择 **“完成”** 按钮。 现在，该项目会在“解决方案资源管理器”中列出。
::: moniker-end
::: moniker range=">=vs-2019"
2.  在“创建新项目”对话框中，为已安装的 SharePoint 的特定版本选择“SharePoint 空项目” 。 例如，如果安装了 SharePoint 2016，请选择“SharePoint 2016 - 空项目”模板。
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

3. 将项目名称更改为“诊所”，然后选择“创建”按钮 。

4. 在“指定用于调试的网站和安全级别”对话框中，输入要向其添加新自定义字段项的本地 SharePoint 网站的 URL，或使用默认位置 (`http://<`SystemName`>/)`。

5. 在“此 SharePoint 解决方案的信任级别是什么?”部分中，使用默认值“部署为沙盒解决方案” 。

     有关沙盒解决方案与场解决方案的详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

6. 选择 **“完成”** 按钮。 现在，该项目会在“解决方案资源管理器”中列出。
::: moniker-end

#### <a name="to-add-site-columns"></a>添加网站栏

1. 添加新的网站栏。 为此，在“解决方案资源管理器”中，右键单击“诊所”项目，然后选择“添加” > “新建项”   。

2. 在“添加新项”对话框中，选择“网站栏”，将名称更改为“PatientName”，然后选择“添加”按钮   。

3. 在网站栏的 Elements.xml 文件中，将“类型”设置保留为“Text”，将“组”设置更改为“诊所网站栏”   。 完成后，网站栏的 Elements.xml 文件应如下例所示。

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
    > 如果你在网站栏名称中使用驼峰式大小写，则 Visual Studio 会自动在 DisplayName 中添加一个空格。
    > 建议不要在“网站栏”名称中使用空格，因为在你尝试将解决方案部署到 SharePoint 时，这可能会导致问题。

4. 使用相同的过程，向项目添加另外两个网站栏：PatientID (Type = “Integer”) 和 DoctorName (Type = “Text”) 。 将其“组”值设置为“诊所网站栏”。

## <a name="create-a-custom-content-type"></a>创建自定义内容类型
 接下来，根据联系人内容类型创建内容类型，其中包括你在上一过程中创建的网站栏。 使内容类型基于现有内容类型可以节省时间，因为基内容类型提供了多个可在新内容类型中使用的网站栏。

#### <a name="to-create-a-custom-content-type"></a>创建自定义内容类型

1. 向项目中添加内容类型。 在“解决方案资源管理器”中，选择项目节点

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 展开 Visual C# 或 Visual Basic 下的 SharePoint 节点，然后选择“2010”节点   。

4. 在“模板”窗格中，选择“内容类型”模板，将名称更改为“患者信息”然后选择“添加”按钮   。

     “SharePoint 自定义向导”随即打开。

5. 在“此内容类型应从哪一个基内容类型继承”列表中，选择“联系人”作为新内容类型的基础，然后选择“完成”按钮  。

     这样，你就可以访问联系人内容类型中其他可能有用的网站栏，此外还有你之前定义的网站栏。

6. 在内容类型设计器显示后，请在“栏”选项卡中添加前面定义的三个网站栏：“患者姓名”、“患者 ID”和“医生姓名”   。 若要添加这些栏，请在“显示名称”下的网站栏列表中选择第一个列表框，然后逐一选择该列表中的每个网站栏。

    > [!TIP]
    > 若要更快地选择网站栏，请输入栏名称的前几个字来筛选该列表。

7. 除了三个自定义网站栏外，还可从网站栏列表中添加“注释”网站栏。

8. 为“患者姓名”和“患者 ID”网站栏选择“必需”复选框，以使其成为必填字段  。

9. 在“内容类型”选项卡上，确保内容类型名称为“患者信息”，然后将描述更改为“患者信息卡”  。

10. 将“组名称”更改为“诊所内容类型”，将其他设置保留为其默认值 。

11. 在菜单栏上，选择“文件” > “全部保存”，然后关闭内容类型设计器 。

## <a name="create-a-list"></a>创建列表
 现在，创建一个使用新的内容类型和网站栏的列表。

#### <a name="to-create-a-list"></a>创建列表

1. 向项目添加一个列表。 在“解决方案资源管理器”中，选择项目节点。

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 展开 Visual C# 或 Visual Basic 下的 SharePoint 节点  。

4. 在“模板”窗格中，选择“列表”模板，将名称更改为“患者”，然后选择“添加”按钮   。

5. 将“自定义列表基于”设置保留为“默认值(自定义列表)”，然后选择“完成”按钮  。

6. 在列表设计器中，选择“内容类型”按钮以显示“内容类型设置”对话框 。

7. 选择新行，在内容类型列表中选择“患者信息”内容类型，然后选择“确定”按钮 。

     执行此操作会将“患者信息”内容类型的所有网站栏添加到列表中。

8. 删除列表中所有网站栏，但以下网站栏除外：

    - 患者 ID

    - 患者姓名

    - 住宅电话

    - 电子邮件

    - 医生姓名

    - 注释

9. 在“栏显示名称”下，选择一个空行，添加自定义列表栏，然后将其命名为“医院” 。 将其数据类型保留为“单行文本”。

     自定义列表栏仅适用于此列表。 将自定义列表栏添加到列表中时，新的列表内容类型（包括添加到列表中的所有栏）将创建并设置为默认列表。

    > [!TIP]
    > 如果从网站栏列表中选择某一栏，将使用现有的网站栏。 但是，如果在不选择列表中任何栏的情况下输入栏名称值，则会创建自定义列表栏，即使列表中已存在同名的栏。

     可选择将自定义列表栏的数据类型设置为“查找”，而不是将此栏的数据类型设置为“单行文本”，并且其值将从表或另一个列表中进行检索。 有关“查找”栏的信息，请参阅 [SharePoint 2010 中的列表关系](/previous-versions/msp-n-p/ff798514(v=pandp.10))和[查阅和列表关系](/previous-versions/office/developer/sharepoint-2010/ff623048(v=office.14))。

10. 选择“患者 ID”和“患者姓名”框旁的“必需”复选框  。

11. 在“视图”选项卡上，选择一个空行来创建视图。 在“视图名称”栏下的空白行中输入“患者详细信息” 。

     在“视图”选项卡上，可指定要在 SharePoint 列表中显示的栏。

12. 选择新的“患者详细信息”行，然后选择“设置为默认”按钮 。

     新视图现在为该列表的默认视图。

13. 按照以下顺序将以下栏添加到“所选栏”列表中：

    - 患者 ID

    - 患者姓名

    - 住宅电话

    - 电子邮件

    - 医生姓名

    - 医院

    - 注释

14. 在“属性”列表中，选择“排序和分组”属性，然后选择省略号按钮 ![省略号图标](../sharepoint/media/ellipsisicon.gif "“省略号”图标") 以显示“排序和分组”对话框  。

15. 在“栏名称”列表中，选择“患者姓名”列，确保“排序”栏设置为“升序”，然后选择“确定”按钮    。

## <a name="test-the-application"></a>测试应用程序
 在自定义网站栏、内容类型和列表就绪后，请将它们部署到 SharePoint，并运行应用程序进行测试。

#### <a name="to-test-the-application"></a>测试应用程序

1. 在菜单栏上，依次选择“文件” > “全部保存”。

2. 按 F5 运行应用程序。

     应用程序将进行编译，然后其功能将部署到 SharePoint 并激活。

3. 在快速启动栏上，选择“患者”链接以显“患者”列表 。

     列表中的栏名称应与你在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的“视图”选项卡上输入的名称相匹配。

4. 选择“添加新项”链接以创建患者信息卡。

5. 在字段中输入信息，然后选择“保存”按钮。

     新记录将显示在列表中。

## <a name="see-also"></a>另请参阅
- [创建 SharePoint 的站点栏、内容类型和列表](../sharepoint/creating-site-columns-content-types-and-lists-for-sharepoint.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [操作说明：创建自定义字段类型](/previous-versions/office/developer/sharepoint-2010/bb862248(v=office.14))
- [内容类型](/previous-versions/office/developer/sharepoint-2010/ms479905(v=office.14))
- [“列”](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))
