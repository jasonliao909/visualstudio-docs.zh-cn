---
title: 编程中的Office任务
description: 了解如何针对文档级自定义项中的数据进行编程，而无需使用 Word 或 Microsoft Office 对象Office Excel。
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
ms.openlocfilehash: 152af5d3be5385e6f5c91fb510d62ea7bc336218
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664763"
---
# <a name="common-tasks-in-office-programming"></a>编程中的Office任务
  本主题旨在帮助针对使用 Visual Studio 对 Office 解决方案编程的下列常见问题找到解决方法。

- [设置和常规任务](#projects)。

- [用户界面自定义任务](#ui)。

- [Excel自动化任务](#excel)。

- [Word 自动化任务](#word)。

- [数据任务](#data)。

- [服务器端文档管理任务](#server)。

- [安全任务](#security)。

- [部署任务](#deployment)。

## <a name="setup-and-general-tasks"></a><a name="projects"></a> 设置和常规任务

- [如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

- [如何：升级Office解决方案](/previous-versions/4bez6837(v=vs.140))。

- [如何：安装Office互操作程序集](../vsto/how-to-install-office-primary-interop-assemblies.md)。

- [如何：通过Office程序集 将应用程序作为目标](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)。

- [如何：在项目 Office处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

- [如何：打开Office解决方案，而无需运行代码](../vsto/how-to-open-office-solutions-without-running-code.md)。

- [如何：为解决方案 设置Office信息](../vsto/how-to-set-up-configuration-information-for-an-office-solution.md)。

- [如何：在功能区 上显示开发人员选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

- [如何：显示外接程序用户界面错误](../vsto/how-to-show-add-in-user-interface-errors.md)。

## <a name="user-interface-customization-tasks"></a><a name="ui"></a> 用户界面自定义任务

### <a name="controls-on-documents-and-worksheets"></a>文档和工作表上的控件

- [如何：添加Windows窗体控件以Office文档](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)。

- [如何：将 NamedRange 控件添加到工作表](../vsto/how-to-add-namedrange-controls-to-worksheets.md)。

- [如何：将 ListObject 控件添加到工作表](../vsto/how-to-add-listobject-controls-to-worksheets.md)。

- [如何：添加Windows窗体控件以Office文档](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)。

- [如何：将内容控件添加到 Word 文档](../vsto/how-to-add-content-controls-to-word-documents.md)。

- [如何：将书签控件添加到 Word 文档](../vsto/how-to-add-bookmark-controls-to-word-documents.md)。

### <a name="task-panes-in-document-level-customizations"></a>文档级自定义项中的任务窗格

- [如何：将操作窗格添加到 Word 文档或Excel工作簿。](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)

### <a name="task-panes-in-vsto-add-ins"></a>外接程序中VSTO窗格

- [如何：将自定义任务窗格添加到应用程序](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)。

### <a name="ribbon-customizations"></a>功能区自定义项

- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)。

- [如何：更改功能区 上选项卡的位置](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)。

- [如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)。

- [如何：将控件添加到 Backstage 视图](../vsto/how-to-add-controls-to-the-backstage-view.md)。

- [如何：将功能区从功能区设计器导出到功能区 XML](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)。

### <a name="outlook-form-regions"></a>Outlook 窗体区域

- [如何：将窗体区域添加到Outlook外接程序项目 。](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)

- [如何：防止Outlook显示窗体区域](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)。

### <a name="custom-menus"></a>自定义菜单

- [如何：将命令添加到快捷菜单](../vsto/how-to-add-commands-to-shortcut-menus.md)。

## <a name="excel-automation-tasks"></a><a name="excel"></a>Excel自动化任务

- [如何：以编程方式在工作表单元格 中显示字符串](../vsto/how-to-programmatically-display-a-string-in-a-worksheet-cell.md)。

- [如何：以编程方式创建新工作簿](../vsto/how-to-programmatically-create-new-workbooks.md)。

- [如何：以编程方式打开工作簿](../vsto/how-to-programmatically-open-workbooks.md)。

- [如何：以编程方式保存工作簿](../vsto/how-to-programmatically-save-workbooks.md)。

- [如何：以编程方式关闭工作簿](../vsto/how-to-programmatically-close-workbooks.md)。

- [如何：以编程方式将新工作表添加到工作簿](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)。

- [如何：以编程方式隐藏工作表](../vsto/how-to-programmatically-hide-worksheets.md)。

- [如何：以编程方式在工作簿 中移动工作表](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)。

- [如何：以编程方式保护工作簿](../vsto/how-to-programmatically-protect-workbooks.md)。

- [如何：以编程方式引用代码 中的工作表范围](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)。

- [如何：以编程方式将样式应用于工作簿 中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)。

- [如何：以编程方式更改包含所选单元格 的工作表行中的格式](../vsto/how-to-programmatically-change-formatting-in-worksheet-rows-containing-selected-cells.md)设置。

- [如何：以编程方式搜索工作表范围 中的文本](../vsto/how-to-programmatically-search-for-text-in-worksheet-ranges.md)。

- [如何：以编程方式打印工作表](../vsto/how-to-programmatically-print-worksheets.md)。

- [如何：以编程方式运行Excel计算](../vsto/how-to-programmatically-run-excel-calculations-programmatically.md)。

- [如何：以编程方式对工作表 中的数据进行排序](../vsto/how-to-programmatically-sort-data-in-worksheets.md)。

## <a name="word-automation-tasks"></a><a name="word"></a> Word 自动化任务

- [如何：以编程方式创建新文档](../vsto/how-to-programmatically-create-new-documents.md)。

- [如何：以编程方式打开现有文档](../vsto/how-to-programmatically-open-existing-documents.md)。

- [如何：以编程方式保存文档](../vsto/how-to-programmatically-save-documents.md)。

- [如何：以编程方式关闭文档](../vsto/how-to-programmatically-close-documents.md)。

- [如何：以编程方式将文本插入 Word 文档](../vsto/how-to-programmatically-insert-text-into-word-documents.md)。

- [如何：以编程方式定义并选择文档 中的范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)。

- [如何：以编程方式重置 Word 文档中的范围](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)。

- [如何：以编程方式设置文档 中的文本格式](../vsto/how-to-programmatically-format-text-in-documents.md)。

- [如何：将 XMLNode 控件添加到 Word 文档](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)。

- [如何：以编程方式更新书签文本](../vsto/how-to-programmatically-update-bookmark-text.md)。

- [如何：以编程方式搜索和替换文档中的文本](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)。

- [如何：以编程方式打印文档](../vsto/how-to-programmatically-print-documents.md)。

- [如何：以编程方式创建 Word 表](../vsto/how-to-programmatically-create-word-tables.md)。

- [如何：以编程方式将行和列添加到 Word 表](../vsto/how-to-programmatically-add-rows-and-columns-to-word-tables.md)。

- [如何：以编程方式计算文档中的字符数](../vsto/how-to-programmatically-count-characters-in-documents.md)。

## <a name="data-tasks"></a><a name="data"></a> 数据任务

### <a name="data-bound-controls"></a>数据绑定控件

- [如何：使用数据库 中的数据填充工作表](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)。

- [如何：使用数据库 的数据填充文档](../vsto/how-to-populate-documents-with-data-from-a-database.md)。

- [如何：使用服务 的数据填充文档](../vsto/how-to-populate-documents-with-data-from-services.md)。

- [如何：使用 对象 的数据填充文档](../vsto/how-to-populate-documents-with-data-from-objects.md)。

- [如何：使用数据库 的数据填充文档](../vsto/how-to-populate-documents-with-data-from-a-database.md)。

- [如何：使用服务 的数据填充文档](../vsto/how-to-populate-documents-with-data-from-services.md)。

- [如何：使用来自主机控件 的数据更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)。

### <a name="cached-data-in-document-level-solutions"></a>文档级解决方案中的缓存数据

- [如何：缓存数据以脱机或在服务器上使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)。

- [如何：以编程方式将数据源缓存在Office文档中](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)。

- [如何：在受密码保护的文档 中缓存数据](../vsto/how-to-cache-data-in-a-password-protected-document.md)。

### <a name="custom-xml-data"></a>自定义 XML 数据

- [如何：向文档级自定义项 添加自定义 XML 部件](../vsto/how-to-add-custom-xml-parts-to-document-level-customizations.md)。

- [如何：使用外接程序 将自定义 XML 部件VSTO文档](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md)。

## <a name="server-side-document-management-tasks"></a><a name="server"></a> 服务器端文档管理任务

- [如何：从文档 中删除托管代码扩展](../vsto/how-to-remove-managed-code-extensions-from-documents.md)。

- [如何：将托管代码扩展附加到文档](../vsto/how-to-attach-managed-code-extensions-to-documents.md)。

## <a name="security-tasks"></a><a name="security"></a> 安全任务

- [如何：对解决方案 Office签名](../vsto/how-to-sign-office-solutions.md)。

## <a name="deployment-tasks"></a><a name="deployment"></a> 部署任务

- [如何：使用 ClickOnce 发布 Office 解决方案](/previous-versions/bb386095(v=vs.110))。

- [如何：使用 ClickOnce 将文档级 Office 解决方案发布到 SharePoint 服务器](/previous-versions/bb608595(v=vs.110))。

- [如何：安装 ClickOnce Office 解决方案](/previous-versions/bb608592(v=vs.110))。

- [如何：在最终用户计算机上安装必备组件以运行 Office 解决方案](/previous-versions/bb608608(v=vs.110))。

- [如何：为部署 Office 解决方案准备 IIS](/previous-versions/bb608629(v=vs.110))。

- [如何：更新部署的 Office 解决方案](/previous-versions/bb157871(v=vs.110))。

- [如何：更改 Office 解决方案的安装路径](/previous-versions/bb608626(v=vs.110))。

## <a name="see-also"></a>另请参阅
- [&#40;Visual Studio 中的 Office 开发入门&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office 应用程序和项目类型提供的功能](../vsto/features-available-by-office-application-and-project-type.md)
- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)