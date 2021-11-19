---
title: 操作说明：本地化代码 | Microsoft Docs
description: 了解如何通过将硬编码字符串替换为对 GetGlobalResourceObject 的调用（一种引用本地化资源的方法）来本地化 SharePoint 中的代码。
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663827"
---
# <a name="how-to-localize-code"></a>如何：本地化代码
  未本地化的代码使用硬编码字符串值。 若要对代码字符串进行本地化，请将其替换为对 <xref:System.Web.HttpContext.GetGlobalResourceObject%2A> 的调用，这是引用本地化资源的方法。

## <a name="localize-code"></a>本地化代码

#### <a name="to-localize-code"></a>本地化代码

1. 在“解决方案资源管理器”中，打开一个项目项的快捷菜单，然后选择“添加” > “模块”。

     选择“资源文件”模板。

    > [!NOTE]
    > 请确保将资源文件添加到 SharePoint 项目项，以便“部署类型”属性可用。 稍后在此过程中需要此属性。

2. 请为默认语言资源文件指定一个你选择的名称，并追加 .resx 扩展名，如 MyAppResources.resx。

3. 重复步骤 1 和步骤 2，向 SharePoint 项目项添加单独的资源文件：每种本地化语言各对应一个文件。

     对每个本地化资源文件使用同一基名称，但添加区域性 ID。 例如，将德语本地化资源命名为 MyAppResources.de-DE.resx。

4. 打开每个资源文件，并添加已本地化的字符串。 在每个文件中使用相同的字符串 ID。

5. 将每个资源文件的“部署类型”属性值更改为“AppGlobalResource”，使每个文件都部署到服务器的 App_GlobalResources 文件夹。

6. 将每个文件的“生成操作”属性值保留为“嵌入的资源”。

     嵌入的资源将编译到项目的 DLL 中。

7. 生成项目以创建资源附属 DLL。

8. 在“包设计器”中，选择“高级”选项卡，然后添加附属程序集。

9. 在“位置”框中，在位置路径前面添加区域性 ID 文件夹，例如 de-DE\\\<Project Item Name>.resources.dll。

10. 如果解决方案尚未引用 System.Web 程序集，请添加对该程序集的引用，并在代码中向 <xref:System.Web> 添加一个指令。

11. 在你的代码中找到用户可见的所有硬编码的字符串，如 UI 文本、错误和消息文本。 使用以下语法将这些字符串替换为对 <xref:System.Web.HttpContext.GetGlobalResourceObject%2A> 方法的调用：

    ```csharp
    HttpContext.GetGlobalResourceObject("Resource File Name", "String ID")
    ```

12. 选择 F5 键生成并运行应用程序。

13. 在 SharePoint 中，从默认值更改显示语言。

     本地化字符串将显示在应用程序中。 若要显示本地化资源，SharePoint 服务器必须已安装与资源文件的区域性匹配的语言包。

## <a name="see-also"></a>另请参阅
- [本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)
- [如何：本地化功能](../sharepoint/how-to-localize-a-feature.md)
- [如何：本地化 ASPX 标记](../sharepoint/how-to-localize-aspx-markup.md)
- [如何：添加资源文件](../sharepoint/how-to-add-a-resource-file.md)
