---
title: 绑定到外接程序项目中VSTO服务的数据
description: 了解如何将控件添加到Microsoft Word文档、将控件绑定到从 MSDN 内容服务检索到的数据，以及运行时响应事件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- databases [Office development in Visual Studio], scrolling records
- records [Office development in Visual Studio], scrolling
- data [Office development in Visual Studio], scrolling database records
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 1a80c4f6dea1861bd91cfcfe4985975fc7a5e10e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122082668"
---
# <a name="walkthrough-bind-to-data-from-a-service-in-a-vsto-add-in-project"></a>演练：绑定到外接程序项目中VSTO服务的数据
  可以将数据绑定到 VSTO 外接程序项目中的宿主控件。 本演练演示如何在运行时将控件添加到 Microsoft Office Word 文档中、将控件绑定到从 MSDN Content Service 检索到的数据以及响应事件。

 **适用于：** 本主题中的信息适用于 Word 2010 的应用程序级项目。 有关详细信息，请参阅[按 Office 应用程序和项目类型提供的功能](../vsto/features-available-by-office-application-and-project-type.md)。

 本演练演示以下任务：

- 在运行时将 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 控件添加到文档中。

- 将 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 控件绑定到 Web 服务的数据。

- 响应 <xref:Microsoft.Office.Tools.Word.ContentControlBase.Entering> 控件的 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 事件。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 或 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-a-new-project"></a>创建新项目
 第一步是创建 Word VSTO 外接程序项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 使用 Visual Basic 或 C# 创建一个名为 **MTPS Content Service** 的 Word VSTO 外接程序项目。

     有关详细信息，请参阅[如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

     Visual Studio 会打开 `ThisAddIn.vb` 或 `ThisAddIn.cs` 文件并将项目添加到“解决方案资源管理器” 中。

## <a name="add-a-web-service"></a>添加 Web 服务
 对于本演练，请使用名为 MTPS 内容服务的 Web 服务。 此 Web 服务以 XML 字符串或纯文本的形式从指定的 MSDN 项目返回信息。 下一步演示如何在内容控件中显示返回的信息。

### <a name="to-add-the-mtps-content-service-to-the-project"></a>将 MTPS 内容服务添加到项目

1. 在 **“数据”** 菜单上，单击 **“添加新数据源”**。

2. 在“数据源配置向导” 中单击“服务” ，再单击“下一步” 。

3. 在“地址”  字段中键入下面的 URL：

   `http://services.msdn.microsoft.com/ContentServices/ContentService.asmx`

4. 单击“转到”。

5. 在“命名空间”  字段中键入“ContentService” ，再单击“确定” 。

6. 在“添加引用向导”  对话框中单击“完成” 。

## <a name="add-a-content-control-and-bind-to-data-at-run-time"></a>添加内容控件并运行时绑定到数据
 在 VSTO 外接程序项目中，在运行时添加和绑定控件。 对于本演练，请配置内容控件，以在用户单击控件内部时从 Web 服务检索数据。

### <a name="to-add-a-content-control-and-bind-to-data"></a>添加内容控件并绑定到数据

1. 在 `ThisAddIn` 类中，分别为 MTPS Content Service、内容控件和数据绑定声明变量。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb" id="Snippet2":::

2. 将以下方法添加到 `ThisAddIn` 类。 此方法会在活动文档的开始处创建一个内容控件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb" id="Snippet4":::

3. 将以下方法添加到 `ThisAddIn` 类。 此方法初始化创建请求并将请求发送到 Web 服务所需的对象。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb" id="Snippet6":::

4. 创建一个事件处理程序，当用户在内容控件内单击时检索有关内容控件的 MSDN Library 文档，并将数据绑定到内容控件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb" id="Snippet5":::

5. 从 `AddRichTextControlAtRange` 方法调用 `InitializeServiceObjects` 和 `ThisAddIn_Startup` 方法。 对于 C# 程序员，添加一个事件处理程序。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb" id="Snippet3":::

## <a name="test-the-add-in"></a>测试外接程序
 打开 Word 后， <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 控件会随即显示。 当在该控件内单击时，该控件中的文本会发生变化。

### <a name="to-test-the-vsto-add-in"></a>若要测试 VSTO 外接程序

1. 按 **F5**。

2. 在内容控件内单击。

     随即从 MTPS Content Service 下载信息并将信息显示在内容控件中。

## <a name="see-also"></a>请参阅
- [将数据绑定到解决方案中的Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)
