---
title: 通过编辑器扩展访问 DTE 对象
description: 了解如何使用本演练中的代码示例从编辑器扩展访问 DTE 对象。
ms.custom: SEO-VS-2020
ms.date: 04/24/2019
ms.topic: tutorial
helpviewer_keywords:
- editors [Visual Studio SDK], new - getting the DTE object
ms.assetid: c1f40bab-c6ec-45b0-8333-ea5ceb02a39d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 094a37960fa5b32d018eebe3becee4fde43cc392
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905119"
---
# <a name="walkthrough-access-the-dte-object-from-an-editor-extension"></a>演练：通过编辑器扩展访问 DTE 对象

在 VSPackages 中，可以通过使用 DTE 对象类型调用 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 方法来获取 DTE 对象。 在 Managed Extensibility Framework (MEF) 扩展中，可以导入 <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>，然后使用 <xref:EnvDTE.DTE> 类型调用 <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> 方法。

## <a name="prerequisites"></a>先决条件

要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

## <a name="get-the-dte-object"></a>获取 DTE 对象

1. 创建 C# VSIX 项目，将其命名为“DTETest”。 添加“编辑器分类器”项模板，将其命名为“DTETest” 。

   有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

::: moniker range=">=vs-2019"

2. 将下列程序集引用添加到该项目中：

    - Microsoft.VisualStudio.Shell.Framework
    - Microsoft.VisualStudio.Shell.Immutable.10.0

3. 在 DTETestProvider.cs 文件中，添加以下 `using` 指令：

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. 在 `DTETestProvider` 类中，导入 <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. 在 `GetClassifier()` 方法中，在 `return` 语句前添加以下代码：

    ```csharp
   ThreadHelper.ThrowIfNotOnUIThread();
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

::: moniker range="vs-2017"

2. 将下列程序集引用添加到该项目中：

   - EnvDTE
   - Microsoft.VisualStudio.Shell.Framework

3. 在 DTETestProvider.cs 文件中，添加以下 `using` 指令：

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. 在 `DTETestProvider` 类中，导入 <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. 在 `GetClassifier()` 方法中，在 `return` 语句前添加以下代码：

    ```csharp
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

## <a name="see-also"></a>另请参阅

- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
- [使用 DTE 启动 Visual Studio](launch-visual-studio-dte.md)
