---
title: Office 编程中的常见任务
description: 了解如何对文档级自定义项中的数据进行编程，而无需使用 Microsoft Office Word 或 Office Excel 的对象模型。
ms.custom: SEO-VS-2020SS
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, getting started
- FAQs (frequently asked questions) [Office development in Visual Studio]
- Office development in Visual Studio, frequently asked questions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: e7282fbd105491edb0aac45e116d10da5abf3d1ca77f16a75ae63d6b8c863f04
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121424458"
---
# <a name="common-tasks-in-office-programming"></a>Office 编程中的常见任务
  本主题旨在帮助针对使用 Visual Studio 对 Office 解决方案编程的下列常见问题找到解决方法。

- [安装和常规任务](#projects)。

- [用户界面自定义任务](#ui)。

- [Excel 自动化任务](#excel)。

- [Word 自动化任务](#word)。

- [数据任务](#data)。

- [服务器端文档管理任务](#server)。

- [安全任务](#security)。

- [部署任务](#deployment)。

## <a name="setup-and-general-tasks"></a><a name="projects"></a> 安装和常规任务

- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

- [如何升级 Office 解决方案](/previous-versions/4bez6837(v=vs.140))。

- [如何：安装 Office 主互操作程序集](../vsto/how-to-install-office-primary-interop-assemblies.md)。

- [如何：通过主互操作程序集面向 Office 应用程序](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)。

- [如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

- [如何：在不运行代码的情况下打开 Office 解决方案](../vsto/how-to-open-office-solutions-without-running-code.md)。

- [如何：为 Office 解决方案设置配置信息](../vsto/how-to-set-up-configuration-information-for-an-office-solution.md)。

- [如何：在功能区上显示 "开发人员" 选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

- [如何：显示外接程序用户界面错误](../vsto/how-to-show-add-in-user-interface-errors.md)。

## <a name="user-interface-customization-tasks"></a><a name="ui"></a> 用户界面自定义任务

### <a name="controls-on-documents-and-worksheets"></a>文档和工作表上的控件

- [如何：向 Office 文档添加 Windows 窗体控件](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)。

- [如何：将 NamedRange 控件添加到工作表](../vsto/how-to-add-namedrange-controls-to-worksheets.md)。

- [如何：将 ListObject 控件添加到工作表](../vsto/how-to-add-listobject-controls-to-worksheets.md)。

- [如何：向 Office 文档添加 Windows 窗体控件](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)。

- [如何：向 Word 文档添加内容控件](../vsto/how-to-add-content-controls-to-word-documents.md)。

- [如何：将书签控件添加到 Word 文档](../vsto/how-to-add-bookmark-controls-to-word-documents.md)。

### <a name="task-panes-in-document-level-customizations"></a>文档级自定义项中的任务窗格

- [如何：向 Word 文档或 Excel 工作簿添加操作窗格](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)。

### <a name="task-panes-in-vsto-add-ins"></a>VSTO 外接程序中的任务窗格

- [如何：向应用程序添加自定义任务窗格](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)。

### <a name="ribbon-customizations"></a>功能区自定义

- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)。

- [如何：更改功能区上选项卡的位置](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)。

- [如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)。

- [如何：向 Backstage 视图添加控件](../vsto/how-to-add-controls-to-the-backstage-view.md)。

- [如何：将功能区从功能区设计器导出到功能区 XML](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)。

### <a name="outlook-form-regions"></a>Outlook 窗体区域

- [如何：向 Outlook 外接程序项目中添加窗体区域](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)。

- [如何：阻止 Outlook 显示窗体区域](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)。

### <a name="custom-menus"></a>自定义菜单

- [如何：向快捷菜单添加命令](../vsto/how-to-add-commands-to-shortcut-menus.md)。

## <a name="excel-automation-tasks"></a><a name="excel"></a>Excel 自动化任务

- [如何：以编程方式在工作表单元格中显示字符串](../vsto/how-to-programmatically-display-a-string-in-a-worksheet-cell.md)。

- [如何：以编程方式创建新的工作簿](../vsto/how-to-programmatically-create-new-workbooks.md)。

- [如何：以编程方式打开工作簿](../vsto/how-to-programmatically-open-workbooks.md)。

- [如何：以编程方式保存工作簿](../vsto/how-to-programmatically-save-workbooks.md)。

- [如何：以编程方式关闭工作簿](../vsto/how-to-programmatically-close-workbooks.md)。

- [如何：以编程方式向工作簿添加新工作表](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)。

- [如何：以编程方式隐藏工作表](../vsto/how-to-programmatically-hide-worksheets.md)。

- [如何：以编程方式在工作簿中移动工作表](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)。

- [如何：以编程方式保护工作簿](../vsto/how-to-programmatically-protect-workbooks.md)。

- [如何：以编程方式在代码中引用工作表范围](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)。

- [如何：以编程方式将样式应用于工作簿中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)。

- [如何：以编程方式在包含选定单元格的工作表行中更改格式设置](../vsto/how-to-programmatically-change-formatting-in-worksheet-rows-containing-selected-cells.md)。

- [如何：以编程方式在工作表范围内搜索文本](../vsto/how-to-programmatically-search-for-text-in-worksheet-ranges.md)。

- [如何：以编程方式打印工作表](../vsto/how-to-programmatically-print-worksheets.md)。

- [如何：以编程方式运行 Excel 计算](../vsto/how-to-programmatically-run-excel-calculations-programmatically.md)。

- [如何：以编程方式对工作表中的数据进行排序](../vsto/how-to-programmatically-sort-data-in-worksheets.md)。

## <a name="word-automation-tasks"></a><a name="word"></a> Word automation 任务

- [如何：以编程方式创建新文档](../vsto/how-to-programmatically-create-new-documents.md)。

- [如何：以编程方式打开现有文档](../vsto/how-to-programmatically-open-existing-documents.md)。

- [如何：以编程方式保存文档](../vsto/how-to-programmatically-save-documents.md)。

- [如何：以编程方式关闭文档](../vsto/how-to-programmatically-close-documents.md)。

- [如何：以编程方式在 Word 文档中插入文本](../vsto/how-to-programmatically-insert-text-into-word-documents.md)。

- [如何：以编程方式在文档中定义和选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)。

- [如何：以编程方式重置 Word 文档中的范围](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)。

- [如何：以编程方式设置文档中文本的格式](../vsto/how-to-programmatically-format-text-in-documents.md)。

- [如何：将 XMLNode 控件添加到 Word 文档](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)。

- [如何：以编程方式更新书签文本](../vsto/how-to-programmatically-update-bookmark-text.md)。

- [如何：以编程方式在文档中搜索和替换文本](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)。

- [如何：以编程方式打印文档](../vsto/how-to-programmatically-print-documents.md)。

- [如何：以编程方式创建 Word 表](../vsto/how-to-programmatically-create-word-tables.md)。

- [如何：以编程方式向 Word 表中添加行和列](../vsto/how-to-programmatically-add-rows-and-columns-to-word-tables.md)。

- [如何：以编程方式统计文档中的字符数](../vsto/how-to-programmatically-count-characters-in-documents.md)。

## <a name="data-tasks"></a><a name="data"></a> 数据任务

### <a name="data-bound-controls"></a>数据绑定控件

- [如何：用数据库中的数据填充工作表](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)。

- [如何：用数据库中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-a-database.md)。

- [如何：用服务中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-services.md)。

- [如何：用对象中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-objects.md)。

- [如何：用数据库中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-a-database.md)。

- [如何：用服务中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-services.md)。

- [如何：使用宿主控件中的数据更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)。

### <a name="cached-data-in-document-level-solutions"></a>文档级解决方案中的缓存数据

- [如何：缓存数据以便脱机使用或在服务器上使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)。

- [如何：以编程方式在 Office 文档中缓存数据源](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)。

- [如何：在受密码保护的文档中缓存数据](../vsto/how-to-cache-data-in-a-password-protected-document.md)。

### <a name="custom-xml-data"></a>自定义 XML 数据

- [如何：向文档级自定义项添加自定义 XML 部件](../vsto/how-to-add-custom-xml-parts-to-document-level-customizations.md)。

- [如何：使用 VSTO 外接程序将自定义 XML 部件添加到文档](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md)中。

## <a name="server-side-document-management-tasks"></a><a name="server"></a> 服务器端文档管理任务

- [如何：从文档中删除托管代码扩展](../vsto/how-to-remove-managed-code-extensions-from-documents.md)。

- [如何：将托管代码扩展附加到文档](../vsto/how-to-attach-managed-code-extensions-to-documents.md)。

## <a name="security-tasks"></a><a name="security"></a> 安全任务

- [如何：对 Office 解决方案进行签名](../vsto/how-to-sign-office-solutions.md)。

## <a name="deployment-tasks"></a><a name="deployment"></a> 部署任务

- [如何：使用 Office 发布 ClickOnce。](/previous-versions/bb386095(v=vs.110))

- [如何：使用 Office](/previous-versions/bb608595(v=vs.110))将文档Office解决方案发布到 SharePoint ClickOnce 服务器。

- [如何：安装ClickOnce Office解决方案](/previous-versions/bb608592(v=vs.110))。

- [如何：在最终用户计算机上安装必备组件以运行Office解决方案](/previous-versions/bb608608(v=vs.110))。

- [如何：准备 IIS 以部署Office解决方案](/previous-versions/bb608629(v=vs.110))。

- [如何：更新已部署Office解决方案](/previous-versions/bb157871(v=vs.110))。

- [如何：更改解决方案 的Office路径](/previous-versions/bb608626(v=vs.110))。

## <a name="see-also"></a>请参阅
- [开始&#40;Office开发Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [应用程序类型和Office可用的功能](../vsto/features-available-by-office-application-and-project-type.md)
- [Office开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)