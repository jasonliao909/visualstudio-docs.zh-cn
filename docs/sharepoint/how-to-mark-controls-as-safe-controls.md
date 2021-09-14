---
title: 如何：将控件标记为保险箱控件|Microsoft Docs
description: 添加程序集时，保险箱项目项的"SharePoint项"属性或"包设计器"中将控件标记为安全控件。
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665290"
---
# <a name="how-to-mark-controls-as-safe-controls"></a>如何：将控件标记为安全控件
  出于安全SharePoint，可区分受脚本注入保护的 Web 控件和未受脚本注入保护的 Web 控件。 不受信任用户可以 *访问* 受保护的控件或安全控件。 可以将控件标记为安全保险箱项目项的"SharePoint项"属性中，或在将程序集添加到包时，在包设计器中。 有关详细信息，请参阅

- [web.config文件设置将](/previous-versions/office/developer/sharepoint-2007/bb802890(v=office.12))Web 部件程序集注册为 保险箱[控件](/previous-versions/office/developer/sharepoint2003/dd587360(v=office.11))。

> [!IMPORTANT]
> 这些过程用于说明目的。 只有在确定控件是安全的时，才将控件标记为安全。

## <a name="marking-safe-controls-in-the-safe-control-entries-property"></a>在保险箱控件条目保险箱标记控件

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-safe-control-entries-property"></a>在安全控件条目属性中将控件标记为安全或不安全

1. 使用SharePoint Web 部件项目创建一个解决方案。

2. 向 Web 部件添加两个控件：文本框和按钮。 将名称分别保留为默认值 TextBox1 和 Button1。

3. 将两个条目添加到 Web 部件保险箱 **控件条目属性**。 为此，请选择"属性"窗口中" (ASP.NET **保险箱** 控件条目"属性旁边的省略号) 省略号按钮。 ![](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号") 

     将显示 **保险箱控件条目**"对话框。

4. 在 **"保险箱控件** 条目"对话框中，选择"添加"按钮两次，将两个安全控件条目添加到"成员"窗格：一个针对按钮，一个针对文本框。

5. 选择第一个安全控件条目，然后将其 **保险箱** 属性的值更改为 **False，** 将 Type **Name** 属性更改为 **Button1，** 将 保险箱 **Against Script** 属性更改为 **False**。

     此步骤将按钮控件标识为不安全的控件。

6. 选择列表中的第二个安全控件项。 将属性的值保留 **为 True，保险箱** Type  **Name** 属性设置为 **TextBox1，保险箱****脚本** 属性设置为 **True。**

     文本框控件现在被标记为可抵御脚本注入的控件。

7. 选择“确定”按钮关闭对话框。

## <a name="marking-safe-controls-in-the-package-designer"></a>在保险箱设计器中标记控件

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-package-designer"></a>在包设计器中将控件标记为安全或不安全

1. 使用SharePoint Web 部件项目创建一个解决方案。

2. 向 Web 部件添加两个控件：文本框和按钮。 将名称分别保留为默认值 TextBox1 和 Button1。

     记下 控件的命名空间，因为稍后会使用。

3. 在菜单栏上，选择 **"生成**  >  **生成解决方案**"以生成项目。

4. 创建另SharePoint解决方案。

5. 在 **解决方案资源管理器** 中，打开 *Package.Package* 文件的快捷菜单，然后选择"打开"以打开包 **设计器**。

6. 在包 **设计器中**，选择" **高级"** 选项卡。

7. 在 **"其他程序集"** 下，选择" **添加** "按钮，然后从列表中选择"添加 **现有** 程序集"。

8. 在"**添加现有程序集"** 对话框中，选择" (ASP.NET 设计器"![](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")旁边的省略号) **按钮**。

9. 从步骤 1 中创建SharePoint解决方案中选择程序集，然后选择"打开 **"** 按钮。

10. 对于此示例，将" **部署目标"** 选项保留为 GlobalAssemblyCache。

     此步骤使程序集部署到 GAC 数据库的全局程序集 (缓存) 。 如果希望将程序集部署到 Bin (文件夹) Web 应用程序，请改为选择该选项。 有关详细信息，请参阅[deploying Web 部件 in SharePoint Foundation。](/previous-versions/office/developer/sharepoint-2010/cc768621(v=office.14))

11. 在 **"保险箱控件"** 框中，选择"单击此处 **添加新项"** 按钮。

12. 输入下表中属性的值。

    |属性名称|Value|
    |-------------------|-----------|
    |命名空间|控件的完全限定命名空间，例如 **BdcModelProject1.VisualWebPart1。**|
    |类型名称|Button1|
    |程序集名称|强程序集名称，例如：Microsoft。Office。SharePoint。ClientExtensions，Version=14.0.0.0，Culture=neutral，PublicKeyToken=71e9bce111e9429c。|
    |Safe|清除保险箱 **复选框**。|
    |保险箱针对脚本|将 **"保险箱脚本"** 复选框保留为清除。|

    > [!NOTE]
    > 通过 **包设计器** 的"高级"选项卡添加的程序集的"程序集名称"值不能是令牌，它必须是强名称程序集。 有关详细信息，请参阅[创建和使用具有强名称的程序集](/previous-versions/dotnet/netframework-4.0/xwb8f617(v=vs.100))。

13. 选择 Tab **键** 以创建另一个安全控件项。

14. 再次 **选择"单击此处添加新项"** 按钮。

15. 输入下表中属性的值。

    |属性名称|Value|
    |-------------------|-----------|
    |命名空间|控件的完全限定命名空间，例如 **BdcModelProject1.VisualWebPart1。**|
    |类型名称|TextBox1|
    |程序集名称|强程序集名称，例如：Microsoft。Office。SharePoint。ClientExtensions，Version=14.0.0.0，Culture=neutral，PublicKeyToken=71e9bce111e9429c。|
    |Safe|选中 **"保险箱** 复选框。|
    |保险箱针对脚本|选中 **"保险箱脚本**"复选框。|

16. 选择 **Tab** 键，然后选择"确定 **"** 按钮关闭对话框。

## <a name="see-also"></a>另请参阅
- [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [打包和部署SharePoint解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
