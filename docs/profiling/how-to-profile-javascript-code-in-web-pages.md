---
title: 分析网页中的 JavaScript 代码 | Microsoft Docs
description: 了解 Visual Studio 分析工具如何使用检测分析方法收集 JavaScript 代码的性能数据。
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- JavaScript performance profiling
- Profiling Tools,JavaScript
- web site performance profiling
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: f6ff70d45f47a8f7c34be58cfa33491f28e34bdb
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122060968"
---
# <a name="how-to-profile-javascript-code-in-web-pages"></a>如何：分析网页中的 JavaScript 代码

Visual Studio 分析工具可以通过使用检测分析方法收集在 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序、任意网页或 JavaScript 应用程序中执行的 JavaScript 代码的性能数据。 需要 Internet Explorer 8 或更高版本。

> [!WARNING]
> 若要分析 UWP 应用中的 JavaScript，请参阅 [JavaScript 内存](../profiling/javascript-memory.md)

可以使用“分析向导”创建性能会话。 指定检测方法，然后在该性能会话的属性对话框的“检测”页上指定 JavaScript 分析选项。

如果指定 JavaScript 分析，则将同时分析在浏览器中执行的 JavaScript 代码以及在服务器中执行的 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 代码。

- 对于 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序，将同时分析在浏览器中执行的 JavaScript 代码以及在服务器中执行的 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 代码。

- 对于任意网页，将分析在浏览器中执行的 JavaScript 代码。

## <a name="to-profile-javascript-in-an-aspnet-web-application-project"></a>分析 ASP.NET Web 应用程序项目中的 JavaScript

1. 在 Visual Studio 中打开 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 项目。

2. 在“分析”  菜单上，单击“启动性能向导” 。

3. 在“性能向导”的第一页上，指定“检测”  分析方法，然后单击“下一步” 。

4. 在向导的第二页上，确保在目标列表中选择了当前项目，然后单击“下一步” 

5. 在向导的第三页上，选中“分析 JavaScript”  复选框，然后单击“下一步” 。

6. 在向导的第四页上，单击“完成”以在浏览器中启动 Web 应用程序。

7. 练习要分析的功能。

8. 若要结束分析会话，请关闭浏览器。

### <a name="to-profile-javascript-in-individual-web-pages-or-a-javascript-applications"></a>分析各网页或 JavaScript 应用程序中的 JavaScript

1. 打开 Visual Studio。

2. 在“分析”  菜单上，单击“启动性能向导” 。

3. 在“性能向导”的第一页上，指定“检测”  分析方法，然后单击“下一步” 。

4. 在向导的第二页上，单击 ASP.NET 或 JavaScript 应用程序，然后单击“下一步” 

5. 在向导的第三页上：

    1. 在“将运行应用程序的 URL 或路径”  框中键入网页的 URL。

    2. 选中“分析 JavaScript”  复选框，然后单击“下一步” 。

6. 在向导的第四页上，单击“完成”以在浏览器中启动网页。

7. 练习要分析的功能。

8. 若要结束分析会话，请关闭浏览器。
