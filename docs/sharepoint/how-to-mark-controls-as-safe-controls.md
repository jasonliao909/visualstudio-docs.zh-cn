---
title: 如何：将控件标记为安全控件 | Microsoft Docs
description: 添加程序集时，在 SharePoint 项目项的安全控件项属性或包设计器中将控件标记为安全控件。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665290"
---
# <a name="how-to-mark-controls-as-safe-controls"></a>如何：将控件标记为安全控件
  为了安全起见，SharePoint 区分了受脚本注入保护的 Web 控件和不受保护的 Web 控件。 不受信任用户可以访问受保护的控件或安全控件。 将程序集添加到包时，可以在 SharePoint 项目项的安全控件项属性或包设计器中将控件标记为安全。 有关详细信息，请参阅

- [web.config 文件设置更改](/previous-versions/office/developer/sharepoint-2007/bb802890(v=office.12))和[将 Web 部件程序集注册为安全控件](/previous-versions/office/developer/sharepoint2003/dd587360(v=office.11))。

> [!IMPORTANT]
> 这些过程用于说明目的。 只有确定控件是安全的时，才将控件标记为安全。

## <a name="marking-safe-controls-in-the-safe-control-entries-property"></a>在安全控件项属性中标记安全控件

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-safe-control-entries-property"></a>在安全控件项属性中将控件标记为安全或不安全

1. 使用可视 Web 部件项目创建 SharePoint 解决方案。

2. 向 Web 部件添加两个控件：文本框和按钮。 将名称分别保留为默认值 TextBox1 和 Button1。

3. 将两个项添加到 Web 部件的“安全控件项”属性。 为此，请选择“属性”窗口中“安全控件项”属性旁边的省略号 (![ASP.NET 移动设计器中的省略号](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")) 按钮。

     “安全控件项”对话框随即出现。

4. 在“安全控件项”对话框中，选择“添加”按钮两次，向“成员”窗格中添加两个安全控件项：一个用于按钮，一个用于文本框。

5. 选择第一个安全控件项，并将其“安全”属性的值更改为“False”，将其“类型名称”属性更改为“Button1”，并将其“安全应对脚本”属性更改为“False”。

     此步骤将按钮控件标识为不安全控件。

6. 选择列表中的第二个安全控件项。 将其“安全”属性的值保留为“True”，将其“类型名称”属性设置为“TextBox1”，并将其“安全应对脚本”属性设置为“True”。

     文本框控件现在被标记为安全应对脚本注入的控件。

7. 选择“确定”按钮关闭对话框。

## <a name="marking-safe-controls-in-the-package-designer"></a>在包设计器中标记控件

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-package-designer"></a>在包设计器中将控件标记为安全或不安全

1. 使用可视 Web 部件项目创建 SharePoint 解决方案。

2. 向 Web 部件添加两个控件：文本框和按钮。 将名称分别保留为默认值 TextBox1 和 Button1。

     记下控件的命名空间，因为稍后会使用。

3. 在菜单栏上，依次选择“生成” > “生成解决方案”以生成项目。

4. 创建另一个 SharePoint 解决方案。

5. 在“解决方案资源管理器”中，打开 Package.Package 文件的快捷菜单，然后选择“打开”以打开“包设计器”。

6. 在“包设计器”中，选择“高级”选项卡。

7. 在“其他程序集”下，选择“添加”按钮，然后从列表中选择“添加现有程序集”。

8. 在“添加现有程序集”对话框中，选择“源文件路径”旁边的省略号 (![ASP.NET 移动设计器中的省略号](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")) 按钮。

9. 从在步骤 1 中创建的 SharePoint 解决方案中选择程序集，然后选择“打开”按钮。

10. 对于此示例，将“部署目标”选项保留为 GlobalAssemblyCache。

     此步骤会导致程序集部署到系统全局程序集缓存 (GAC)。 如果希望将程序集部署到 Web 应用程序 (Bin) 文件夹，请改为选择该选项。 有关详细信息，请参阅[在 SharePoint Foundation 中部署 Web 部件](/previous-versions/office/developer/sharepoint-2010/cc768621(v=office.14))。

11. 在“安全控件”框中，选择“单击此处添加新项”按钮。

12. 输入下表中属性的值。

    |属性名称|Value|
    |-------------------|-----------|
    |命名空间|控件的完全限定命名空间，例如 BdcModelProject1.VisualWebPart1。|
    |类型名称|Button1|
    |程序集名称|强程序集名称，例如：Microsoft.Office.SharePoint.ClientExtensions, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c。|
    |Safe|清除“安全”复选框。|
    |安全应对脚本|清除“安全应对脚本”复选框。|

    > [!NOTE]
    > 通过“包设计器”的“高级”选项卡添加的程序集的“程序集名称”值不能是令牌，它必须是具有强名称的程序集。 有关详细信息，请参阅[创建和使用具有强名称的程序集](/previous-versions/dotnet/netframework-4.0/xwb8f617(v=vs.100))。

13. 选择 Tab键创建另一个安全控件项。

14. 再次选择“单击此处添加新项”按钮。

15. 输入下表中属性的值。

    |属性名称|Value|
    |-------------------|-----------|
    |命名空间|控件的完全限定命名空间，例如 BdcModelProject1.VisualWebPart1。|
    |类型名称|TextBox1|
    |程序集名称|强程序集名称，例如：Microsoft.Office.SharePoint.ClientExtensions, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c。|
    |Safe|选中“安全”复选框。|
    |安全应对脚本|选中“安全应对脚本”复选框。|

16. 选择 Tab 键，然后选择“确定”按钮关闭对话框。

## <a name="see-also"></a>另请参阅
- [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
