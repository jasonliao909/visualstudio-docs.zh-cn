---
title: 将内容类型链接到文件扩展名
description: 本演练中了解如何使用编辑器和扩展名将Managed Extensibility Framework类型链接到文件扩展名。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - link content type to file name extension
ms.assetid: 21ee64ce-9afe-4b08-94a0-8389cc4dc67c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: d49c7241d952270a7ca394e445ef777189a39b9a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122078526"
---
# <a name="walkthrough-link-a-content-type-to-a-file-name-extension"></a>演练：将内容类型链接到文件扩展名
可以使用 MEF 扩展名的编辑器定义自己的内容类型，Managed Extensibility Framework (文件) 扩展名。 在某些情况下，文件扩展名已由语言服务定义。 但是，若要与 MEF 一起使用它，仍必须链接到内容类型。

## <a name="prerequisites"></a>必备条件
 从 Visual Studio 2015 开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-a-mef-project"></a>创建 MEF 项目

1. 创建 C# VSIX 项目。  ("**新建** Project对话框中，选择 **"Visual C#/** 扩展性"，然后选择 **"VSIX Project**.) 将解决方案命名 `ContentTypeTest` "。

2. 在 **source.extension.vsixmanifest** 文件中，转到"资产"选项卡，将"类型"字段设置为 **Microsoft.VisualStudio.MefComponent，** 将"源"字段设置为当前解决方案中的 **A** 项目，将 **Project** 字段设置为项目名称。 

## <a name="define-the-content-type"></a>定义内容类型

1. 添加一个类文件并将其命名为 `FileAndContentTypes`。

2. 添加对下列程序集的引用：

    1. System.ComponentModel.Composition

    2. Microsoft.VisualStudio.Text.Logic

    3. Microsoft.VisualStudio.CoreUtility

3. 添加以下 `using` 指令。

    ```csharp
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text.Classification;
    using Microsoft.VisualStudio.Utilities;

    ```

4. 声明包含定义的静态类。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {. . .}
    ```

5. 在此类中，导出 <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> 名为"hid"的 ，并声明其基定义为"text"。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {
        [Export]
        [Name("hid")]
        [BaseDefinition("text")]
        internal static ContentTypeDefinition hidingContentTypeDefinition;
    }
    ```

## <a name="link-a-file-name-extension-to-a-content-type"></a>将文件扩展名链接到内容类型

- 若要将此内容类型映射到文件扩展名，请导出扩展名 <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> *为 .hid* 且内容类型为"hid"的 。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {
         [Export]
         [Name("hid")]
         [BaseDefinition("text")]
        internal static ContentTypeDefinition hidingContentTypeDefinition;

         [Export]
         [FileExtension(".hid")]
         [ContentType("hid")]
        internal static FileExtensionToContentTypeDefinition hiddenFileExtensionDefinition;
    }
    ```

## <a name="add-the-content-type-to-an-editor-export"></a>将内容类型添加到编辑器导出

1. 创建编辑器扩展。 例如，可以使用演练：创建边距字形 中所述的 [边距字形扩展](../extensibility/walkthrough-creating-a-margin-glyph.md)。

2. 添加在此过程中定义的类。

3. 导出扩展类时，向该类添加 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> 类型为"hid"的 。

    ```csharp
    [Export]
    [ContentType("hid")]
    ```

## <a name="see-also"></a>另请参阅
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
