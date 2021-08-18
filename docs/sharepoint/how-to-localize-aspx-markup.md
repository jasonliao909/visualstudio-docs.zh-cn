---
title: 如何：本地化 ASPX 标记|Microsoft Docs
description: 了解如何将硬编码的字符串SharePoint引用本地化资源的表达式，从而在代码中本地化 ASPX 标记。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122084267"
---
# <a name="how-to-localize-aspx-markup"></a>如何：本地化 ASPX 标记
  [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] (.aspx) 页通常使用硬编码字符串值。 若要本地化这些字符串，请将其替换为引用本地化资源的表达式。

## <a name="localize-aspx-markup"></a>本地化 ASPX 标记

#### <a name="to-localize-aspx-markup"></a>本地化 ASPX 标记

1. 添加单独的资源文件：一个资源文件用于默认语言，另一个针对每个本地化语言。

     如果仅本地化标记而不是代码，请添加全局资源文件项目项。 如果要本地化代码和标记，请添加资源文件项目项。

    1. 若要添加全局资源文件，解决方案资源管理器，**打开** 项目项的快捷SharePoint，然后选择"**添加新**  >  **项"。** 在"SharePoint **2010"节点** 下，选择"**全局资源文件"** 模板。

    2. 若要添加资源文件，解决方案资源管理器，**打开** 项目项的快捷SharePoint，然后选择"**添加新**  >  **项"。** 在 **"Visual Basic** **Visual C#"节点下**，选择"**资源文件"** 模板。

    > [!NOTE]
    > 请务必将资源文件添加到项目SharePoint以启用"部署类型"属性。 此过程稍后需要此属性。 如果解决方案没有项目SharePoint，可以添加"空"SharePoint Project并删除 *其默认Elements.xml* 文件。

2. 为默认语言资源文件指定一个你选择的名称，并追加 *.resx* 扩展名，例如 MyAppResources.resx。 对每个本地化资源文件使用同一基名称，但添加区域性 [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]。 例如，将德语本地化资源 MyAppResources.de *DE.resx*。

3. 将每个资源文件的 **Deployment Type** 属性的值更改为 **AppGlobalResource，** 使它们部署到服务器的 App_GlobalResources 文件夹。

4. 如果使用资源来本地化代码以及 ASPX 标记，请保留每个文件的"生成操作"属性的值作为 **"嵌入资源"。** 如果仅使用资源文件来本地化标记，可以选择将文件的 属性值更改为 **Content**。 有关详细信息，请参阅[本地化SharePoint解决方案](../sharepoint/localizing-sharepoint-solutions.md)。

5. 打开每个资源文件并添加本地化字符串，在每个文件中使用相同的字符串标识。

6. 在 ASPX 页或控件的标记中，将硬编码字符串替换为 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 使用以下格式的值：

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

7. 选择 **F5** 键以生成并运行应用程序。

8. 在SharePoint中，将显示语言从默认值更改为 。

     本地化字符串显示在应用程序中。 若要显示本地化资源，SharePoint服务器必须安装与资源文件区域性匹配的语言包。

## <a name="see-also"></a>请参阅
- [本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)
- [如何：本地化功能](../sharepoint/how-to-localize-a-feature.md)
- [如何：添加资源文件](../sharepoint/how-to-add-a-resource-file.md)
- [如何：本地化代码](../sharepoint/how-to-localize-code.md)
