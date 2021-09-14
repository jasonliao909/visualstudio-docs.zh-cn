---
title: 如何：本地化代码|Microsoft Docs
description: 了解如何将硬编码SharePoint字符串替换为对 GetGlobalResourceObject（一种引用本地化资源的方法）的调用，从而本地化代码中的代码。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- localizing code [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: c65edab726fb0def889364f37f2eed41778bcfe6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663827"
---
# <a name="how-to-localize-code"></a>如何：本地化代码
  未本地化的代码使用硬编码的字符串值。 若要本地化代码字符串，请将其替换为对 的调用 <xref:System.Web.HttpContext.GetGlobalResourceObject%2A> ，这是引用本地化资源的方法。

## <a name="localize-code"></a>本地化代码

#### <a name="to-localize-code"></a>本地化代码

1. 在 **解决方案资源管理器** 中，打开项目项的快捷菜单，然后选择"**添加模块**  >  **"。**

     选择" **资源文件"** 模板。

    > [!NOTE]
    > 请确保将资源文件添加到SharePoint项，以便"部署类型"属性可用。 此过程稍后需要此属性。

2. 为默认语言资源文件指定一个你选择的名称，并追加 *.resx* 扩展名，例如 *MyAppResources.resx*。

3. 重复步骤 1 和步骤 2，向 SharePoint 项目项添加单独的资源文件：每种本地化语言各对应一个文件。

     请针对每个本地化资源文件使用相同的基名称，但添加区域性 ID。 例如，将德语本地化资源 MyAppResources.de *DE.resx*。

4. 打开每个资源文件并添加本地化字符串。 在每个文件中使用相同的字符串 ID。

5. 将每个资源文件的 **Deployment Type** 属性的值更改为 **AppGlobalResource，** 使每个文件部署到服务器的 App_GlobalResources 文件夹。

6. 将每个文件的 **"生成操作**"属性的值保留为 **"嵌入资源"。**

     嵌入的资源将编译到项目的 DLL 中。

7. 生成项目以创建资源附属 DLL。

8. 在包 **设计器中**，选择" **高级"** 选项卡，然后添加附属程序集。

9. 在 **"位置**"框中，将区域性 ID 文件夹预置到"位置"路径，例如 *de-DE \\ \<Project Item Name> .resources.dll。*

10. 如果解决方案尚未引用 System.Web 程序集，请添加对它的引用，在代码中将 指令添加到 <xref:System.Web> 。

11. 在你的代码中找到用户可见的所有硬编码的字符串，如 UI 文本、错误和消息文本。 使用以下语法将这些字符串替换为对 <xref:System.Web.HttpContext.GetGlobalResourceObject%2A> 方法的调用：

    ```csharp
    HttpContext.GetGlobalResourceObject("Resource File Name", "String ID")
    ```

12. 选择 **F5** 键以生成并运行应用程序。

13. 在SharePoint中，将显示语言从默认值更改为 。

     本地化字符串显示在应用程序中。 若要显示本地化资源，SharePoint服务器必须安装与资源文件区域性匹配的语言包。

## <a name="see-also"></a>另请参阅
- [本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)
- [如何：本地化功能](../sharepoint/how-to-localize-a-feature.md)
- [如何：本地化 ASPX 标记](../sharepoint/how-to-localize-aspx-markup.md)
- [如何：添加资源文件](../sharepoint/how-to-add-a-resource-file.md)
