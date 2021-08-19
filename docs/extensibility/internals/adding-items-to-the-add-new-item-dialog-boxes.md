---
title: 向 "添加新项" 对话框添加项 |Microsoft Docs
description: 了解如何将项添加到 Visual Studio 中的 "添加新项" 对话框，以便您可以显示要在项目中使用的模板和项目元素。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Add New Item dialog box, adding items
ms.assetid: 2f70863b-425b-4e65-86b4-d6a898e29dc7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: bf57d1d20e16bf91fab3a790c2d2f717b3bfd8f7
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122029146"
---
# <a name="add-items-to-the-add-new-item-dialog-box"></a>向 "添加新项" 对话框添加项
将项添加到 " **添加新项** " 对话框的过程从注册表项开始。 如以下注册表项中所示， **AddItemTemplates** 部分包含在 " **添加新项** " 对话框中提供了项的目录的路径和名称。

> [!NOTE]
> 紧跟在代码段之后的表包含有关注册表项的其他信息。

 本部分位于 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0Exp\Projects** 下。

 第一个 GUID 是此类型的项目的 CLSID;第二个 GUID 指示添加项模板的已注册项目类型：

 **\\{C061DB26-5833-11D2-96F5-000000000000} \\AddItemTemplates \\ TemplatesDir \\ {ACEF4EB2-57CF-11D2-96F4-000000000000} \\ 1**

 **@** = #6

   =  \\ TemplatesDir &lt;Visual StudioSDK 安装路径 &gt; \\ VSIntegration \\ &lt; SomeFolder &gt; \\ &lt; SomePackage &gt; \\ &lt; SomeProject &gt; \\ &lt; SomeProjectItems&gt;

 **SortPriority** = dword：00000064

| 名称 | 类型 | 从 *.rgs* 文件 (的数据)  | 说明 |
|------------------|-----------| - | - |
| @ (默认值)  | REG_SZ | #% IDS_ADDITEM_TEMPLATES_ENTRY% | **添加项** 模板的资源 ID。 |
| Val TemplatesDir | REG_SZ | % TEMPLATE_PATH% \\ &lt; SomeProjectItems&gt; | 显示在 " **添加新项** " 向导的对话框中的项目项的路径。 |
| Val SortPriority | REG_DWORD | 100 ([!INCLUDE[vcprx64](../../extensibility/internals/includes/vcprx64_md.md)])  | 确定在 " **添加新项** " 对话框中显示的文件的树节点中的排序顺序。 |

> [!NOTE]
> Visual c # 和 Visual Basic 项目类型的 guid 如下所示：
> - [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]: {FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}
> - [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]: {F184B08F-C81C-45F6-A57F-5ABD9991F28F}

 为 **TemplatesDir** 列出的目录为 *% TEMPLATE_PATH% \\ &lt; SomeProjectItems &gt;*，它是 "**添加新项**" 对话框左侧的节点。 树中的其他元素基于该根目录中的子目录。 可添加到项目中的文件是 " **添加新项** " 对话框的右窗格中的项。

 通常，此文件夹将包含项目的模板文件（如模板 HTML 或 *.cpp* 文件）和任何用于启动向导的 *.vsz* 文件。 若要控制项的显示方式，还可以包含用于本地化目录名称和图标的 *vsdir* 文件。 本地化字符串是在 " **添加新项** " 对话框中表示此节点的对话框中显示的标题。

 但是，不需要在一个 *vsdir* 文件中包含任何内容。 目录中的每一项都有一个 *vsdir* 文件。 有关详细信息，请参阅 [向导 ( .vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md) 和 [模板目录说明 ( vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)。

> [!NOTE]
> 模板目录中的 *vsdir* 文件是可选的。 如果只想将一个项目元素放在目录中，并将其显示在 " **添加新项** " 对话框中，则可以将该文件放在 **TemplatesDir** 语句中指定的 templates 目录中。 然后，该文件将显示在该项目的 " **添加新项** " 对话框的右窗格中。 但是，如果要显示文件或图标的本地化标题，则在 templates 目录中必须至少包含一个 *vsdir* 文件。

## <a name="group-project-items"></a>对项目项进行分组
 如果要在 " **添加新项** " 对话框的文件夹中包含模板组，则根模板目录下必须有子目录，其中包含其中的项。 向用户显示 " **添加新项** " 对话框时，它们也会看到子文件夹，并能够从中选择项目元素。

 代码段中的排序优先级确定在树中相对于树节点的其他元素创建此模板目录的位置。 对于 " **添加新项** " 对话框，排序优先级就是您必须包含的所有内容，以便您的项将显示在对话框中正确的位置。

 您还可以实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> 接口来筛选 " **添加新项** " 对话框中显示的内容。 通过实现此接口，你可以在磁盘上设置一个包含50模板和向导文件的模板目录。 这样一来，你可以使用不同的项目类型，其中包含20个文件，这些文件属于一种项目类型、属于另一项目类型的其他30个文件以及常规项目类型中提供的所有文件。 通过这种方式，根据创建的项目模板，可以显示一组不同的模板文件。

 例如，在 Visual Basic 项目中，您可能有 Web 项目和客户端项目。 Web 窗体不是要添加到客户端项目中的有用项，windows 窗体不能用于添加到 Web 服务器项目中。 因此，你可以创建一个模板目录，其中包含两种类型的项目的所有文件。 然后，通过实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> ，可以隐藏不应根据项目中的项目或项目设置的类型显示的项。

## <a name="filter-project-items"></a>筛选项目项
 `IVsFilterAddProjectItemDlg2` 提供对树中的元素进行筛选 (左窗格) 和项目文件 (右窗格按以下方式) ：

- 按照本地化名称 (标题显示在包含在 *vsdir* 文件中的对话框中 `IVsFilterAddProjectItemDlg`) 由提供。

- 通过磁盘上的文件和文件夹的实际名称 (非本地化-不提供) 的 *vsdir* 文件 `IVsFilterAddProjectItemDlg` 。

- 按类别提供，由提供 `IVsFilterAddProjectItemDlg2` 。

  若要按类别进行筛选，请在 *vsdir* 文件中提供项的类别字符串，如 Visual Basic 中的 *Web 窗体* 或 *客户端项*。 然后，对话框代码从该 *vsdir* 文件中检索类别分类并将其传递给你。 然后，可以将该信息传递到的实现， `IVsFilterAddProjectItemDlg2` 以按类别筛选 " **添加新项** " 对话框。 你还可以筛选网页的项目或作为客户端 Win32 应用程序事例。 此外，还可以将 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 标记项标识为 Microsoft 基础类 (MFC) 或活动模板库 (ATL) 项。 标识这些项时，项目系统可以定义自己的分类，以便可以根据类别和分类筛选系统。

  如果实现此筛选器功能，则不必映射应隐藏的每个项的表。 您可以简单地将项分类为类型，并将分类置于 *vsdir* 文件中。 然后，可以通过实现接口来隐藏具有特定分类的任何项。 通过这种方式，您可以基于项目中的状态，使 " **添加新项** " 对话框中的项成为动态的。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [通常用于扩展项目的对象的 Catid](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [模板目录说明 ( 的 vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
- [向导 ( .vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
