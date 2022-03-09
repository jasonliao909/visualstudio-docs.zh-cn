---
title: 脱机帮助文档
description: 使用 Microsoft Help Viewer 安装和查看各种产品和技术（如 Visual Studio 和 .NET）的脱机帮助文档。
ms.date: 11/02/2017
ms.topic: conceptual
f1_keywords:
- hv_general
helpviewer_keywords:
- Microsoft Help Viewer Help
- Help Viewer, printing a topic
- printing a topic [Help Viewer]
- Help Viewer, toolbar
- Help on Help [Help Viewer]
- Help Viewer, window components
- Help Viewer, navigating
- toolbar [Help Viewer]
ms.assetid: 74e41666-2ce8-4ac0-a0e5-3723d1e322c2
author: jasonchlus
ms.author: jasonchlus
manager: jmartens
ms.technology: vs-help-viewer
ms.workload:
- multiple
ms.openlocfilehash: f9b980b653c4e7f4bc34079154dc25fd22c3a18b
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139551334"
---
# <a name="microsoft-help-viewer"></a>Microsoft Help Viewer

你可以通过使用 Microsoft Help Viewer 在本地计算机上安装和查看各种产品和技术的相关内容。 这些产品包括 Visual Studio、.NET、语言引用、SQL Server 和 Windows 开发。 Help Viewer 可用于：

- 下载内容集，这也称为丛书。 如果需要“脱机”工作时仍可以访问文档，则这会很有用。

- 浏览并搜索目录以按标题查找主题。

- 查找索引中的主题。

- 使用全文搜索查找信息。

- 查找、标记和打印主题。

若要安装 Help Viewer，请参阅 [Microsoft Help Viewer 安装](../help-viewer/installation.md)。 若要开始阅读 Help Viewer 中的帮助主题，而不是联机帮助主题，请转到 Visual Studio 中的“帮助”菜单，然后选择“设置帮助首选项” > “在 Help Viewer 中启动”。

> [!TIP]
> 若要在没有 Internet 连接时查看内容，另一种内容本地下载方法是下载其 PDF 版本。 docs.microsoft.com 上的许多文档集在目录 (TOC) 的底部包含一个链接，通过该链接可下载包含此 TOC 所有文章的 PDF 文件。
>
> ![下载 Visual Studio 文档 PDF](media/overview/download-pdf.png)

## <a name="help-viewer-tour"></a>Help Viewer 导览

可以使用导航选项卡查找已安装内容中的信息，在一个或多个主题选项卡中查看已安装的内容，然后使用“管理内容”选项卡管理内容。还可以通过使用工具栏上的按钮执行其他任务，并在窗口的右下角查找其他信息。

### <a name="navigation-tabs"></a>导航选项卡

|选项卡|说明|
|---|-----------|
|目录|以层次结构（目录）的形式显示已安装的内容。 可指定用于筛选所示标题的条件。|
|索引|显示索引词的字母顺序列表。 可搜索索引，指定用于筛选条目的条件，并要求索引条目包含所指定的文本或以此文本开头。|
|收藏夹|可选择“添加到收藏夹”按钮“收藏”主题，这些主题会显示在该选项卡中。“历史记录”部分显示最近查看的主题列表。|
|搜索|提供一个文本框，可在其中搜索内容中任何位置的词，包括代码和主题标题。|

### <a name="view-topics"></a>查看主题

每个主题显示在单独的选项卡中，可以同时打开多个主题。

### <a name="manage-content"></a>管理内容

通过使用“管理内容”选项卡，可安装、更新、移动和删除内容。在选项卡顶部，可使用“安装源”控件指定是从网络位置还是从磁盘或 URI 安装丛书。 “本地存储路径”框显示了丛书在本地计算机上的安装位置，可通过选择“移动”按钮将它们移动到其他位置。

内容列表显示了可安装或已安装的丛书、更新是否可用以及每个丛书的大小。 可通过以下方式安装或删除一本或多本丛书：选择合适的“添加”或“删除”链接，然后选择“挂起的更改”窗格下的“更新”按钮。 如果已安装的任何丛书有可用更新，则可选择窗口底部的“单击此处立即下载”链接刷新此内容。 此外，如果安装其他丛书时有可用更新，将刷新所有已安装的丛书。

> [!NOTE]
> 如果 Help Viewer 管理员停用了这些功能或没有可用的 Internet 访问，“管理内容”选项卡的功能可能有所不同。

### <a name="toolbar-buttons"></a>工具栏按钮

Help Viewer 窗口中的工具栏包含以下按钮：

- “在目录中显示主题”按钮，用于显示“内容”选项卡中的主题位置。

- “添加到收藏夹”按钮，用于将活动主题添加到“收藏夹”选项卡。

- “在主题中查找”按钮，用于突出显示活动主题中的搜索文本。

- “打印”按钮，用于打印或显示活动主题的预览。

- “查看器选项”按钮，用于显示设置，例如，文本显示大小、返回的搜索结果数、历史记录中显示的主题数以及是否联机检查更新。

- “管理内容”按钮，用于激活“管理内容”选项卡。

- 右侧的小三角形可以打开选项卡列表，包括主题选项卡和“管理内容”选项卡。可以选择选项卡名称激活该选项卡。

## <a name="see-also"></a>另请参阅

- [Microsoft Help Viewer 安装](../help-viewer/installation.md)
- [Help Viewer 管理员指南](../help-viewer/administrator-guide.md)
- [安装和管理本地内容](../help-viewer/install-manage-local-content.md)
