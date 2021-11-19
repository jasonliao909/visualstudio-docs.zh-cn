---
title: “选项”对话框 ->“环境”->“Web 浏览器”
description: 了解如何使用“环境”部分的“Web 浏览器”页，为内部 Web 浏览器和 Internet Explorer 设置选项。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.Environment.Web Browser
- VS.ToolsOptionsPages.Environment.WebBrowser
- VS.ToolsOptionsPages.Environment.Web_Browser
helpviewer_keywords:
- browsers, customizing
- searching, search page for Web browser
- Web browsers, customizing
- searches, default Web browser search page
- URLs, specifying VS home page
- home page
- Options dialog box, Web settings
- Internet Explorer, setting options
ms.assetid: 586db4eb-032d-4cb5-93a6-a7c14de1ae49
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 527163959146545fcf1e8d371bd13804e33d6610
ms.sourcegitcommit: 76541583274c4af4218ac2a8ab4308077a7e340e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2021
ms.locfileid: "132733161"
---
# <a name="options-dialog-box-environment--web-browser"></a>“选项”对话框：环境 \> Web 浏览器

为内部 Web 浏览器和 Internet Explorer 设置选项。 若要访问此对话框，请在“工具”菜单上单击“选项”，展开“环境”文件夹，然后选择“Web 浏览器”。

> [!Important]
> 此功能在 Visual Studio 2022 中已弃用，今后将不受支持。
>
> 有关 Visual Studio 2022 的详细信息，请查看[发行说明]( /visualstudio/releases/2022/release-notes)和 Visual Studio [路线图](/visualstudio/productinfo/vs-roadmap/)。

> [!IMPORTANT]
> 从 Web 打开某些文件或组件可在计算机上执行代码。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[重置设置](../environment-settings.md#reset-settings)。

## <a name="home-page"></a>主页

设置打开 IDE Web 浏览器时显示的页面。

## <a name="search-page"></a>“搜索”页

支持为内部 Web 浏览器指定搜索页。 此位置可能不同于在集成开发环境 (IDE) 外部启动的 Internet Explorer 实例所使用的搜索页。

## <a name="view-source-in"></a>查看源文件的工具

设置从内部 Web 浏览器页上选择“查看源”时用于打开网页的编辑器。

- **源编辑器**：选择此选项可在 [编辑器](../../ide/writing-code-in-the-code-and-text-editor.md)中查看源。

- **HTML 编辑器**：选择此选项可在 [HTML 设计器](/previous-versions/ex0hkwbx(v=vs.140))中查看源。 使用此选项可在两个视图之一中编辑网页：设计视图或基于标准文本的源视图。

- **外部编辑器** 选择此选项可在其他编辑器中查看源。 指定所选任何编辑器（例如 Notepad.exe）的路径。

## <a name="internet-explorer-options"></a>Internet Explorer 选项

单击此选项可更改“Internet 属性”对话框中的 Internet Explorer 选项。 在此对话框中所做的更改会同时影响内部 Web 浏览器和在 Visual Studio 的 IDE 外部（例如，从“开始”菜单）启动的 Internet Explorer 实例。

> [!NOTE]
> 使用“浏览方式”对话框可将 Visual Studio 内部 Web 浏览器替换为所选浏览器。 可从项目中的 HTML 文件或其他文件的右击菜单或上下文菜单访问“浏览方式”对话框。

## <a name="see-also"></a>请参阅

- [“选项”对话框 ->“环境”->“常规”](../../ide/reference/general-environment-options-dialog-box.md)
- [HTML Designer](/previous-versions/ex0hkwbx(v=vs.140))（HTML 设计器）
