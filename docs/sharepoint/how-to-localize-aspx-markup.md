---
title: 如何：本地化 ASPX 标记 | Microsoft Docs
description: 了解如何通过将硬编码的字符串值替换为引用本地化资源的表达式，在 SharePoint 中本地化 ASPX 标记。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- localizing XML [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: d80157fc2468c5d6fe78ae88cfa0f940917888a8
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664145"
---
# <a name="how-to-localize-aspx-markup"></a>如何：本地化 ASPX 标记
  [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] (.aspx) 页通常使用硬编码的字符串值。 若要本地化这些字符串，请将其替换为引用本地化资源的表达式。

## <a name="localize-aspx-markup"></a>本地化 ASPX 标记

#### <a name="to-localize-aspx-markup"></a>本地化 ASPX 标记

1. 添加单独的资源文件：一个用于默认语言，另一个用于每种本地化语言。

     如果要仅本地化标记而不是代码，请添加全局资源文件项目项。 如果要本地化代码和标记，请添加资源文件项目项。

    1. 若要添加全局资源文件，请在“解决方案资源管理器”中打开 SharePoint 项目项的快捷菜单，然后选择“添加” > “新建项”。 在 SharePoint“2010”节点下，选择“全局资源文件”模板。

    2. 若要添加资源文件，请在“解决方案资源管理器”中打开 SharePoint 项目项的快捷菜单，然后选择“添加” > “新建项”。 在“Visual Basic”或“Visual C#”节点下，选择“资源文件”模板。

    > [!NOTE]
    > 请确保将资源文件添加到 SharePoint 项目项以启用“部署类型”属性。 稍后在此过程中需要此属性。 如果解决方案没有 SharePoint 项目项，则可以添加空的 SharePoint 项目并删除其默认 Elements.xml 文件。

2. 请为默认语言资源文件指定一个你选择的名称，并追加 .resx 扩展名，如 MyAppResources.resx。 对每个本地化资源文件使用同一基名称，但添加区域性 [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]。 例如，将德语本地化资源命名为 MyAppResources.de-DE.resx。

3. 将每个资源文件的“部署类型”属性值更改为“AppGlobalResource”，使每个文件都部署到服务器的 App_GlobalResources 文件夹。

4. 如果要使用资源来本地化除 ASPX 标记之外的代码，请将每个文件的“生成操作”属性的值保留为“嵌入的资源”。 如果仅使用资源文件来本地化标记，则可以选择将文件的属性值更改为“内容”。 有关详细信息，请参阅[本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)。

5. 在每个文件中使用相同的字符串 ID，打开每个资源文件并添加已本地化的字符串。

6. 在 ASPX 页或控件的 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 标记中，将硬编码的字符串替换为使用以下格式的值：

    ```aspx-csharp
    <%$Resources:Resource File Name, String ID%>
    ```

     例如，若要本地化应用程序页上标签控件的文本，可以更改：

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
    <asp:Label ID="lbl" runat="server" Text="Label text"></asp:Label>
    </asp:Content>
    ```

     to

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
    <asp:Label ID="lbl" runat="server" Text="<%$Resources:MyAppResources,String1%>"></asp:Label>
    </asp:Content>
    ```

7. 选择 F5 键生成并运行应用程序。

8. 在 SharePoint 中，从默认值更改显示语言。

     本地化字符串将显示在应用程序中。 若要显示本地化资源，SharePoint 服务器必须已安装与资源文件的区域性匹配的语言包。

## <a name="see-also"></a>另请参阅
- [本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)
- [如何：本地化功能](../sharepoint/how-to-localize-a-feature.md)
- [如何：添加资源文件](../sharepoint/how-to-add-a-resource-file.md)
- [如何：本地化代码](../sharepoint/how-to-localize-code.md)
