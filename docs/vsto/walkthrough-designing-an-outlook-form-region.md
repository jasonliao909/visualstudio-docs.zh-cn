---
title: 演练：设计Outlook区域
description: 了解如何设计自定义 Microsoft Outlook窗体区域，该区域在联系人项的"检查器"窗口中显示为新页面。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 2ae0560f34e7cd303aeee3e9f7d8a82d23d68e14
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122147539"
---
# <a name="walkthrough-design-an-outlook-form-region"></a>演练：设计Outlook区域
  自定义窗体区域扩展标准或自定义 Microsoft Office Outlook 窗体。 在本演练中，你将设计作为新页出现在联系人项目的检查器窗口中的自定义窗体区域。 通过将地址信息发送到 Windows Live 本地搜索网站，此窗体区域将显示为联系人列出的每个地址的映射。 有关窗体区域的信息，请参阅[创建Outlook窗体区域](../vsto/creating-outlook-form-regions.md)。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 本演练演示以下任务：

- 创建新的 Outlook VSTO 外接程序项目。

- 将窗体区域添加到 VSTO 外接程序项目。

- 设计窗体区域的布局。

- 自定义窗体区域的行为。

- 测试 Outlook 窗体区域。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Outlook_14_short](../vsto/includes/outlook-14-short-md.md)] 或更高版本。

  ![视频链接](../vsto/media/playvideo.gif "链接到视频")有关本主题的视频版本，请参阅[视频如何：设计Outlook窗体区域](/previous-versions/visualstudio/visual-studio-2008/cc837160(v=vs.90))。

## <a name="create-a-new-outlook-vsto-add-in-project"></a>创建新的Outlook VSTO外接程序项目
 首先创建基本的 VSTO 外接程序项目。

### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>创建新的 Outlook VSTO 外接程序项目

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中，创建Outlook VSTO名称 **为 MapItAddIn 的外接程序项目**。

2. 在 **“新建项目”** 对话框中，选择 **“创建解决方案的目录”**。

3. 将项目保存到任一目录。

     有关详细信息，请参阅[如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

## <a name="add-a-form-region-to-the-outlook-vsto-add-in-project"></a>向外接程序项目Outlook VSTO窗体区域
 Outlook VSTO 外接程序解决方案可包含一个或多个 Outlook 窗体区域项。 使用"新建窗体区域"向导向项目 **Outlook区域** 项。

### <a name="to-add-a-form-region-to-the-outlook-vsto-add-in-project"></a>向 Outlook VSTO 外接程序项目添加窗体区域

1. 在 **解决方案资源管理器** 中，选择 **MapItAddIn** 项目。

2. 在 **“项目”** 菜单上，单击 **“添加新项”**。

3. 在"**添加新项"对话框中**，选择"Outlook **区域"，** 将文件命名 **MapIt**，然后单击"添加 **"。**

     **NewOutlook 窗体区域向导** 将启动。

4. 在"**选择创建窗体区域** 的方式"页上，单击"设计 **新的窗体区域**"，然后单击"下一步 **"。**

5. 在"**选择要创建的窗体区域** 的类型"页上，单击"单独 **"，** 然后单击"下一步 **"。**

     单独的 *窗体* 区域将新页面添加到Outlook窗体。 有关窗体区域类型的信息，请参阅[创建Outlook区域](../vsto/creating-outlook-form-regions.md)。

6. 在" **提供描述性文本并选择显示** 首选项"页上，在" **名称"框中键入** " **映射它** "。

     打开联系人项目时，此名称将显示在检查器窗口的功能区中。

7. 选择 **"撰写"模式下的**"检查器"和"读取模式中的检查器 **"，** 然后单击"下一 **步"。**

8. 在"**标识将显示此窗体区域** 的消息类"页上，清除"邮件"，选择"**联系人**"，然后单击"完成 **"。**

     *将 MapIt.cs* 或 *MapIt.vb* 文件添加到项目中。

## <a name="design-the-layout-of-the-form-region"></a>设计窗体区域布局
 使用窗体区域设计器 直观地 *开发窗体区域*。 可将托管的控件拖到窗体区域设计器图面。 使用设计器和" **属性"** 窗口可以调整控件布局和外观。

### <a name="to-design-the-layout-of-the-form-region"></a>设计窗体区域的布局

1. 在 **解决方案资源管理器** 中，展开 **MapItAddIn** 项目，然后双击 *MapIt.cs* 或 *MapIt.vb* 打开窗体区域设计器。

2. 右键单击设计器，然后单击"属性 **"。**

3. 在"**属性"** 窗口中，将 **"大小**"设置为 **"664，469"。**

     这可确保窗体区域的大小足以显示映射。

4. 在“视图”菜单上，单击“工具箱”。

5. 从" **工具箱"的** "公共控件 **"选项卡中**，将 **WebBrowser** 添加到窗体区域。

     **WebBrowser** 将显示为联系人列出的每个地址的地图。

## <a name="customize-the-behavior-of-the-form-region"></a>自定义窗体区域的行为
 将代码添加到窗体区域事件处理程序，从而自定义窗体区域在运行时的行为方式。 对于此窗体区域而言，代码将检查 Outlook 项的属性，并确定是否显示 Map It 窗体区域。 如果它显示该窗体区域，代码将导航到 Windows Live 本地搜索并加载 Outlook 联系人项目中列出的每个地址的映射。

### <a name="to-customize-the-behavior-of-the-form-region"></a>自定义窗体区域的行为

1. 在 **解决方案资源管理器** 中，右键单击 *"MapIt.cs"* 或 *"MapIt.vb"，* 然后单击"**查看代码"。**

    *MapIt.cs* 或 *MapIt.vb* 在代码编辑器中打开。

2. 展开" **窗体区域工厂"** 代码区域。

    将公开名为 `MapItFactory` 的窗体区域工厂类。

3. 将以下代码添加到 `MapItFactory_FormRegionInitializing` 事件处理程序中。 将在用户打开联系人项目时调用此事件处理程序。 下面的代码确定联系人项目是否包含地址。 如果联系人项不包含地址，此代码将 类的 属性设置 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 为 <xref:Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs> **true，** 并且不显示窗体区域。 否则，VSTO 外接程序将引发 <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> 事件，并显示窗体区域。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs" id="Snippet1":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb" id="Snippet1":::

4. 将以下代码添加到 <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> 事件处理程序中。 此代码执行以下任务：

   - 将联系人项目中的每个地址连接起来，并创建一个 URL 字符串。

   - 调用 <xref:System.Windows.Forms.WebBrowser> 对象的 <xref:System.Windows.Forms.WebBrowser.Navigate%2A> 方法，并将 URL 字符串作为参数传递。

     本地搜索网站将在 Map It 窗体区域中出现，并在便笺本中显示每个地址。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb" id="Snippet2":::

## <a name="test-the-outlook-form-region"></a>测试Outlook区域
 运行项目时，Visual Studio 将打开 Outlook。 打开联系人项目以查看 Map It 窗体区域。 Map It 窗体区域显示为包含地址的任何联系人项目的窗体中的页面。

### <a name="to-test-the-map-it-form-region"></a>测试 Map It 窗体区域

1. 按 **F5** 运行项目。

     Outlook 将打开。

2. 在Outlook"主页 **"选项卡上**，单击"**新建项**"，然后单击"联系 **"。**

3. 在联系人表单中，键入 **"Ann Beebe"** 作为联系人姓名，然后指定以下三个地址。

    |地址类型|地址|
    |------------------|-------------|
    |**业务**|**4567 纽约市圣多美州主区**|
    |**Home**|**1234 北圣维纳州，纽约**|
    |**其他**|**3456 华盛顿州西雅图市主区**|

4. 保存并关闭联系人项目。

5. 重新打开 **"Ann Beebe"** 联系人项。

    在Outlook中，可以通过打开"联系人"通讯簿或键入"搜索人员"中的"Ann Beebe"，在"查找"组中 **完成此操作**。

6. 在 **项的功能** 区的"显示"组中，单击"映射 **它** "以打开"映射它"窗体区域。

     Map It 窗体区域出现，并显示本地搜索网站。 "**业务****"、"** 主页 **"** 和"其他"地址显示在暂存板中。 在便笺本中，选择需映射的地址。

## <a name="next-steps"></a>后续步骤
 可从以下主题了解有关如何自定义 Outlook 应用程序 UI 的详细信息：

- 若要了解如何自定义项目的功能区Outlook，请参阅[自定义自定义项目的功能Outlook。](../vsto/customizing-a-ribbon-for-outlook.md)

## <a name="see-also"></a>请参阅
- [运行时访问窗体区域](../vsto/accessing-a-form-region-at-run-time.md)
- [创建Outlook窗体区域](../vsto/creating-outlook-form-regions.md)
- [创建表单Outlook指南](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [演练：导入在窗体中设计的窗体Outlook](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
- [如何：将窗体区域添加到Outlook外接程序项目](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [将窗体区域与Outlook类关联](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
- [窗体Outlook中的自定义操作](../vsto/custom-actions-in-outlook-form-regions.md)
- [如何：Outlook窗体区域](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)
