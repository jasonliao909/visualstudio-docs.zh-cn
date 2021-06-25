---
title: 将项添加到"添加新项"对话框|Microsoft Docs
description: 了解如何将项添加到 Visual Studio 中的"添加新项"对话框，以便可以显示模板和项目元素以在项目中使用。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Add New Item dialog box, adding items
ms.assetid: 2f70863b-425b-4e65-86b4-d6a898e29dc7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 70bc1a0c4d90d8cab0b2193550773745fc2dd47e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904404"
---
# <a name="add-items-to-the-add-new-item-dialog-box"></a>将项添加到"添加新项"对话框
将项添加到"添加新项" **对话框的过程** 从注册表项开始。 如以下注册表项所示 **，AddItemTemplates** 部分包含"添加新项"对话框中提供的项所位于的目录的路径和名称。 

> [!NOTE]
> 紧随代码段的表包含有关注册表项的其他信息。

 本部分位于HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0Exp\Projects **下。**

 第一个 GUID 是此类型的项目的 CLSID;第二个 GUID 指示"添加项"模板的已注册项目类型：

 **\\{C061DB26-5833-11D2-96F5-000000000000} \\AddItemTemplates \\ TemplatesDir \\ {ACEF4EB2-57CF-11D2-96F4-000000000000} \\ 1**

 **@** = #6

 **TemplatesDir**  =  \\ &lt;Visual Studio SDK 安装路径 &gt; \\ VSIntegration \\ &lt; SomeFolder &gt; \\ &lt; SomePackage &gt; \\ &lt; SomeProject &gt; \\ &lt; SomeProjectItems&gt;

 **SortPriority** = dword：00000064

| 名称 | 类型 | 数据 (*.rgs 文件*)  | 描述 |
|------------------|-----------| - | - |
| @ (默认)  | REG_SZ | #%IDS_ADDITEM_TEMPLATES_ENTRY% | 添加项 **模板的资源** ID。 |
| Val TemplatesDir | REG_SZ | %TEMPLATE_PATH% \\ &lt; SomeProjectItems&gt; | "添加新项"向导的对话框中显示 **的项目项** 的路径。 |
| Val SortPriority | REG_DWORD | 100 ([!INCLUDE[vcprx64](../../extensibility/internals/includes/vcprx64_md.md)])  | 确定"添加新项"对话框中显示的文件树节点 **中的** 排序顺序。 |

> [!NOTE]
> Visual C# 和Visual Basic的 GUID 如下所示：
> - [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]：{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}
> - [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]：{F184B08F-C81C-45F6-A57F-5ABD9991F28F}

 为 **TemplatesDir** 列出的目录为 *%TEMPLATE_PATH% \\ &lt; &gt; SomeProjectItems*，是"添加新项"对话框树 **左侧的节点**。 树中的其他元素基于该根目录中的子目录。 可添加到项目的文件是"添加新项"对话框右 **窗格中的项** 。

 通常，此文件夹将包含项目的模板文件，例如模板 HTML 或 *.cpp* 文件，以及用于启动向导的任何 *.vsz* 文件。 若要控制项的显示方式，还可以包括用于本地化目录名称和图标的 *.vsdir* 文件。 本地化字符串是在"添加新项"对话框树中表示此节点的 **对话框中显示的标题** 。

 但是，不需要在一个 *.vsdir 文件中拥有所有* 内容。 目录中每个 *项都可以有一个 .vsdir* 文件。 有关详细信息，请参阅向导文件 [ (.vsz) ](../../extensibility/internals/wizard-dot-vsz-file.md) 和模板目录说明 [ (.vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)。

> [!NOTE]
> 模板 *目录中的 .vsdir* 文件是可选的。 如果只想将项目元素放入目录中，将其显示在"添加新项"对话框中，可以将该文件放在 **TemplatesDir** 语句中指定的 templates 目录中。 然后，该文件将显示在该项目的"添加新 **项"对话框** 的右窗格中。 但是，如果要显示文件或图标的本地化标题，则必须在 templates 目录中包含至少一 *个 .vsdir* 文件。

## <a name="group-project-items"></a>对项目项进行分组
 如果要在"添加新项"对话框树的文件夹中包含模板组，则必须在根模板目录下具有子目录，其中包含这些子目录的项。 向 **用户显示** "添加新项"对话框时，他们还会看到子文件夹，并能够从中选择项目元素。

 代码段中的排序优先级确定相对于树节点的其他元素将在树中创建此模板目录的哪个位置。 对于 **"添加新项** "对话框，排序优先级是必须包含的所有项，以便项将显示在对话框中的正确位置。

 还可以实现 接口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> 来筛选"添加新项"对话框中显示的内容。 通过实现此接口，可以在包含 50 个模板和向导文件的磁盘上设置一个模板目录。 这样，就可以拥有不同的项目类型，其中 20 个文件属于一个项目类型，其他 30 个文件属于另一个项目类型，所有文件在常规项目类型中可用。 这样，根据所创建的项目模板，可以显示一组不同的模板文件。

 例如，在Visual Basic项目中，你可能有 Web 项目和客户端项目。 Web 窗体不是要添加到客户端项目的有用项，而 Windows 窗体不是要添加到 Web 服务器项目的有用项。 因此，可以创建一个模板目录，其中包含这两种类型的项目的所有文件。 然后，通过实现 ，可以隐藏不应基于项目中的项目或项目设置类型显示的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> 项。

## <a name="filter-project-items"></a>筛选项目项
 `IVsFilterAddProjectItemDlg2` 提供用于筛选树中的元素 (左窗格) 和 (窗格中) 以下列方式显示：

- 通过本地化名称 (*显示在 .vsdir* 文件中包含的对话框中的标题) 由 `IVsFilterAddProjectItemDlg` 提供。

- 根据磁盘上文件和文件夹的实际名称 (非本地化 - 没有 *.vsdir*) 由 提供 `IVsFilterAddProjectItemDlg` 。

- 按类别，由 提供 `IVsFilterAddProjectItemDlg2` 。

  若要按类别进行筛选，请提供 *.vsdir* 文件中某个项的类别字符串，例如 web *窗体* 或 Visual Basic。  然后，对话框代码从 *.vsdir* 文件中检索类别分类，并传递给你。 然后，可以将该信息传递给 的实现， `IVsFilterAddProjectItemDlg2` 以按类别筛选"添加新项"对话框。 还可以筛选网页或客户端 Win32 应用程序事例的项。 此外，可以将标记的项标识为MICROSOFT 基础类 (MFC) 或活动模板库 ([!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] ATL) 项。 识别这些项时，项目系统可以定义自己的分类，以便系统可以基于类别和分类进行筛选。

  如果实现此筛选器功能，则不需要映射应隐藏的每个项的表。 只需将项分类为类型，将分类放入 *.vsdir* 文件或文件中。 然后，可以通过实现 接口隐藏具有特定分类的任何项。 这样，就可以根据项目中的状态使"添加新项"对话框中的项动态。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [通常用于扩展项目的 对象的 CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [模板目录说明 (.vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
- [向导 (.vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
