---
title: 如何：将控件标记为保险箱控件 |Microsoft Docs
description: 添加程序集时，将控件标记为 SharePoint 项目项保险箱控件项属性中的安全控件或包设计器中的安全控件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, safe controls
- SharePoint development in Visual Studio, advanced packaging tools
- safe controls [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: e96a27be0ae8a71125964e27da99270d9142886c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122092977"
---
# <a name="how-to-mark-controls-as-safe-controls"></a>如何：将控件标记为安全控件
  为安全而言，SharePoint 区分不同的 web 控件，这些控件不受脚本注入和 web 控件的保护。 不受信任的用户可以访问受保护的控件或 *安全控件*。 在将程序集添加到包中时，可以将控件标记为安全，在 SharePoint 项目项的保险箱控件项属性或 **包设计器** 中。 有关详细信息，请参阅

- [web.config 文件设置更改并将](/previous-versions/office/developer/sharepoint-2007/bb802890(v=office.12)) [Web 部件程序集注册为保险箱控件](/previous-versions/office/developer/sharepoint2003/dd587360(v=office.11))。

> [!IMPORTANT]
> 这些过程用于说明目的。 仅在确定控件安全时才将其标记为安全。

## <a name="marking-safe-controls-in-the-safe-control-entries-property"></a>在保险箱控件项属性中标记保险箱控件

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-safe-control-entries-property"></a>将控件标记为安全控件项属性中的安全或不安全

1. 使用可视 Web 部件项目创建 SharePoint 解决方案。

2. 将两个控件添加到 Web 部件：文本框和按钮。 将名称分别保留为默认值 TextBox1 和 Button1。

3. 将两个项添加到 Web 部件的 **保险箱控件项**"属性中。 为此，请在 "**属性**" 窗口中选择 "**保险箱控制项**" 属性旁边的省略号 (![ASP.NET Mobile 设计器 "椭圆形](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")") "按钮。

     此时将显示 "**保险箱控件项**" 对话框。

4. 在 **保险箱控件项**"对话框中，选择"**添加**"按钮两次，将两个安全控件项添加到"**成员**"窗格中：一个用于按钮，一个用于文本框。

5. 选择第一个安全控制项，然后将其 **保险箱** 属性的值更改为 " **false**"，将其 "**类型名称**" 属性更改为 " **Button1**"，保险箱并将其 "**脚本**" 属性设置为 " **false**"。

     此步骤将按钮控件标识为不安全控件。

6. 选择列表中的第二个安全控件项。 将其 **保险箱** 属性的值保留为 **true** ，并将其 "**类型名称**" 属性设置为 " **TextBox1** " 保险箱，并将其 "**脚本**" 属性设置为 " **true**"。

     文本框控件现在被标记为可安全应对脚本注入的控件。

7. 选择“确定”按钮关闭对话框。

## <a name="marking-safe-controls-in-the-package-designer"></a>在包设计器中标记保险箱控件

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-package-designer"></a>在包设计器中将控件标记为安全或不安全

1. 使用可视 Web 部件项目创建 SharePoint 解决方案。

2. 将两个控件添加到 Web 部件：文本框和按钮。 将名称分别保留为默认值 TextBox1 和 Button1。

     记下控件的命名空间，因为稍后将用到它。

3. 在菜单栏上，选择 "**生成**" "生成  >  **解决方案**" 以生成项目。

4. 创建另一个 SharePoint 解决方案。

5. 在 **解决方案资源管理器** 中，打开 *包* 文件的快捷菜单，然后选择 " **打开** " 以打开 **包设计器**。

6. 在 **包设计器** 中，选择 " **高级** " 选项卡。

7. 在 " **其他程序集**" 下，选择 " **添加** " 按钮，然后从列表中选择 " **添加现有程序集** "。

8. 在 "**添加现有程序集**" 对话框中，选择 "**源路径**" 旁边的 "![移动设计器椭圆 ASP.NET](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号") (的省略号) " 按钮。

9. 从你在步骤1中创建的 SharePoint 解决方案中选择程序集，然后选择 "**打开**" 按钮。

10. 对于本示例，请将 " **部署目标** " 选项保留为 "GlobalAssemblyCache"。

     此步骤将导致程序集部署到系统全局程序集缓存 (GAC) 。 若要将程序集部署到 Web 应用程序 (Bin) 文件夹中，请改为选择该选项。 有关详细信息，请参阅[在 SharePoint Foundation 中部署 Web 部件](/previous-versions/office/developer/sharepoint-2010/cc768621(v=office.14))。

11. 在 "**保险箱控件**" 框中，选择 "**单击此处添加新项**" 按钮。

12. 输入下表中属性的值。

    |属性名称|Value|
    |-------------------|-----------|
    |命名空间|控件的完全限定命名空间，例如 **BdcModelProject1. VisualWebPart1**。|
    |类型名称|Button1|
    |程序集名称|强程序集名称，例如： Microsoft。Office。SharePoint。ClientExtensions，Version = 14.0.0.0，Culture = 中立，PublicKeyToken = 71e9bce111e9429c。|
    |Safe|清除 "**保险箱**" 复选框。|
    |保险箱针对脚本|清除 "**保险箱针对脚本**" 复选框。|

    > [!NOTE]
    > 通过 **包设计器** 的 "**高级**" 选项卡添加的程序 **集的程序集名称** 值不能是标记，它必须是具有强名称的程序集。 有关详细信息，请参阅[创建和使用具有强名称的程序集](/previous-versions/dotnet/netframework-4.0/xwb8f617(v=vs.100))。

13. 选择 **Tab** 键以创建另一个安全控件项。

14. 再次选择 " **单击此处添加新项"** 按钮。

15. 输入下表中属性的值。

    |属性名称|Value|
    |-------------------|-----------|
    |命名空间|控件的完全限定命名空间，例如 **BdcModelProject1. VisualWebPart1**。|
    |类型名称|TextBox1|
    |程序集名称|强程序集名称，例如： Microsoft。Office。SharePoint。ClientExtensions，Version = 14.0.0.0，Culture = 中立，PublicKeyToken = 71e9bce111e9429c。|
    |Safe|选中 "**保险箱**" 复选框。|
    |保险箱针对脚本|选中 "**保险箱针对脚本**" 复选框。|

16. 选择 **Tab** 键，然后选择 " **确定"** 按钮关闭对话框。

## <a name="see-also"></a>请参阅
- [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
