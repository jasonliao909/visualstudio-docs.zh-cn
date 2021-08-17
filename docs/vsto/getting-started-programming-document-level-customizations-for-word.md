---
title: 开始为 Word 编程文档级自定义项
description: 了解开始使用 word 创建文档级自定义项时Microsoft Office Word 使用Visual Studio。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word solutions in Visual Studio
- Word projects [Office development in Visual Studio], getting started
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 9142781a7e06e2cf1f2546324551be7b5dc436ea
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122026429"
---
# <a name="get-started-programming-document-level-customizations-for-word"></a>开始为 Word 编程文档级自定义项
  如果刚开始使用 Microsoft Office Word 创建文档级自定义Visual Studio，则需要了解以下内容。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

## <a name="understand-how-document-level-customizations-for-word-work"></a>了解 Word 的文档级自定义项如何工作
 创建的每个 Word 自定义都基于单个文档。 若要开始使用自定义项，最终用户打开文档，或者从 Word 模板创建文档。 文档中的事件（例如，将光标移到特定区域或单击按钮和菜单项）可以调用程序集中的事件处理方法。 当文档关闭时，自定义项提供的功能在 Word 中不再可用。

 有关详细信息，请参阅 [文档级自定义的体系结构](../vsto/architecture-of-document-level-customizations.md)。

## <a name="create-document-level-projects-for-word"></a>为 Word 创建文档级项目
 若要为 Word 创建文档级自定义项，请使用"新建文档"对话框中的"Word 文档"或"word 模板 **Project模板。** 这些模板包括所需程序集引用和项目文件。

 若要详细了解如何为 Word 创建文档级项目，请参阅如何：在 Office[创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md) 有关项目模板详细信息，请参阅Office[模板概述](../vsto/office-project-templates-overview.md)。

## <a name="program-word-documents-by-using-host-items-host-controls"></a>使用宿主项宿主控件对 Word 文档进行编程
 *宿主项**和宿主* 控件是为文档级自定义项提供编程模型的类。

 主机项为代码提供入口点，并且它们还可以充当宿主控件和 Windows控件的容器。 在 Word 的文档级项目中，宿主项由 类 `ThisDocument` 表示。

 宿主控件基于本机 Word 对象，例如内容控件、书签和 XML 节点。 宿主控件提供与本机 Word 对象类似的功能，但它们也具有新的事件、设计器支持和数据绑定功能。 它们在项目代码和 IntelliSense 中显示为第一类对象，这使得直接在代码中引用特定对象更容易，而无需导航 Word 对象模型。

 有关详细信息，请参阅以下主题：

- [计划文档级自定义项](../vsto/programming-document-level-customizations.md)

- [使用扩展对象自动执行 Word](../vsto/automating-word-by-using-extended-objects.md)

- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)

## <a name="customize-the-user-interface-of-word"></a>自定义 Word 的用户界面
 大多数Microsoft Office解决方案修改 (UI) 用户界面Office为用户提供与解决方案交互的某种方式。 可以通过多种方式使用文档级自定义项修改 Word 的 UI。 例如，可以将控件添加到功能区，并显示操作窗格。 有关详细信息，请参阅自定义[Office UI。](../vsto/office-ui-customization.md)

 还可以直接在 Visual Studio 中打开与项目关联的文档。 当文档在 Visual Studio 中打开时，可以使用 Word 用户界面修改文档。 还可以将文档用作设计图面，从而将控件拖动到该图面上。 有关详细信息，请参阅 Office[环境中Visual Studio项目](../vsto/office-projects-in-the-visual-studio-environment.md)。

## <a name="bind-controls-to-data"></a>将控件绑定到数据
 内容控件和 控件在可以从"数据源"窗口拖动的 <xref:Microsoft.Office.Tools.Word.Bookmark> **控件列表中** 。 按此方式添加内容控件和书签会自动将它们绑定到使用 窗口设置的数据源。 无需编写任何代码，即可显示来自数据库、服务和业务对象的数据。 有关详细信息，请参阅将数据绑定到解决方案 中的[Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)。

## <a name="next-steps"></a>后续步骤
 若要了解如何为 Word 创建文档级自定义项，请参阅 [演练：为 Word](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)创建第一个文档级自定义项。 本演练介绍了 Office 开发工具Visual Studio Word 文档级自定义项的编程模型。

 有关演练 Word 项目中一些常见任务的主题列表，请参阅编程中的[Office任务](../vsto/common-tasks-in-office-programming.md)。

## <a name="see-also"></a>请参阅
- [如何：在 Office 创建Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [计划文档级自定义项](../vsto/programming-document-level-customizations.md)
- [Word 解决方案](../vsto/word-solutions.md)
- [演练：为 Word 创建第一个文档级自定义项](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [Word 对象模型概述](../vsto/word-object-model-overview.md)
- [在解决方案中Office代码](../vsto/writing-code-in-office-solutions.md)
