---
title: 如何：从文档中删除托管代码扩展
description: 以编程方式从文档或工作簿中删除属于文档级自定义项的文档或工作簿，Microsoft Word Excel。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- managed code extensions [Office development in Visual Studio], removing
- documents [Office development in Visual Studio], managed code extensions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 233024b9e5dbd42908f8cd4b7a76cfd5a6901977
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664951"
---
# <a name="how-to-remove-managed-code-extensions-from-documents"></a>如何：从文档中删除托管代码扩展
  可以编程方式从文档或工作簿中删除自定义程序集，该文档或工作簿是 Word 或 Microsoft Office 文档级自定义Microsoft Office Excel。 然后，用户可以打开文档并查看内容，但 (添加到) UI 的任何自定义用户界面将不会显示，并且代码不会运行。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 可以使用 提供的方法之一 `RemoveCustomization` 删除自定义程序集 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。 使用哪种方法取决于是否要在 Word 文档或 Excel 工作簿打开) 时，通过运行自定义项中的代码来删除运行时 (的自定义项，或者是否要从已关闭的文档或未安装 Microsoft Office 的服务器上删除自定义项。

## <a name="to-remove-the-customization-assembly-at-run-time"></a>运行时删除自定义程序集

1. 在自定义代码中，为 Word (调用) 方法，或调用 (<xref:Microsoft.Office.Tools.Word.Document.RemoveCustomization%2A> <xref:Microsoft.Office.Tools.Excel.Workbook.RemoveCustomization%2A> for Excel) 。 只有在不再需要自定义项后，才应调用此方法。

     在代码中调用此方法的方式取决于自定义项的使用方式。 例如，如果客户使用自定义项的功能，直到他们准备好将文档发送到仅需要文档本身的其他客户端 (而不是自定义) ，则你可以提供一些在客户单击时调用的 UI。 `RemoveCustomization` 或者，如果自定义项在首次打开文档时使用数据填充文档，但自定义项不提供客户直接访问的其他任何功能，则一旦自定义项完成文档初始化，就可以调用 RemoveCustomization。

## <a name="to-remove-the-customization-assembly-from-a-closed-document-or-a-document-on-a-server"></a>从已关闭的文档或服务器上的文档中删除自定义程序集

1. 在不需要创建Microsoft Office（如控制台应用程序或 Windows Forms 项目）中，添加对Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll *的引用。*

2. 将以下 **Imports** **或 using** 语句添加到代码文件的顶部。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb" id="Snippet1":::

3. 调用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.RemoveCustomization%2A> 类的静态 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 方法，并指定 参数的解决方案文档路径。

     下面的代码示例假定你要从桌面上名为 *WordDocument1.docx的文档中删除* 自定义项。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb" id="Snippet2":::

4. 生成项目，并运行要删除自定义项的计算机上的应用程序。 计算机必须安装 Visual Studio 2010 Tools for Office 运行时。

## <a name="see-also"></a>另请参阅
- [使用 ServerDocument 类管理服务器上的文档](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [如何：将托管代码扩展附加到文档](../vsto/how-to-attach-managed-code-extensions-to-documents.md)
