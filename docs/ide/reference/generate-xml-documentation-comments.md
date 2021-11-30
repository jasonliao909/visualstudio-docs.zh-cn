---
title: 插入 XML 文档注释
description: 了解如何在代码中插入 XML 文档注释，从而能创建编译器生成的 XML 文件，以便与 .NET 程序集一起分发。
ms.custom: SEO-VS-2020
ms.date: 11/23/2021
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- dotnet
ms.openlocfilehash: 7f037dc69b39f051cebca3d0d00306da07745a99
ms.sourcegitcommit: 28168514c0c9472e852de35cceb4f95837669da6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "133256589"
---
# <a name="how-to-insert-xml-comments-for-documentation-generation"></a>如何：为文档生成项插入 XML 注释

Visual Studio 可自动生成标准的 XML 文档注释结构，进而帮助记录类和方法等代码元素。 在编译时，可生成一个包含文档注释的 XML 文件。 若要启用该选项，请在项目属性的 "**生成** 输出" 选项卡上选择 "**生成包含 API 文档的文件**"  >   。

> [!TIP]
> 如果要为文档文件配置非默认名称和位置，请将 [DocumentationFile](/dotnet/core/project-sdk/msbuild-props#documentationfile) 属性添加到 *.csproj*、 *. .vbproj* 或 *.fsproj* 文件。

可随附 .NET 程序集一并分发编译器生成的 XML 文件，让 Visual Studio 和其他 IDE 能够快速显示类型和成员信息。 此外，可以通过 [DocFX](https://dotnet.github.io/docfx/) 和 [Sandcastle](https://www.microsoft.com/download/details.aspx?id=10526) 等工具运行 XML 文件，由此生成 API 引用网站。

> [!NOTE]
> 可在 [C#](/dotnet/csharp/programming-guide/xmldoc/) 和 [Visual Basic](/dotnet/visual-basic/programming-guide/program-structure/how-to-create-xml-documentation) 中使用自动插入 XML 文档注释的“插入注释”命令。 但可在 C++ 文件中手动插入 [XML 文档注释](/cpp/build/reference/xml-documentation-visual-cpp)，这样仍可在编译时生成 XML 文档文件。

## <a name="to-insert-xml-comments-for-a-code-element"></a>若要为代码元素插入 XML 注释

1. 将文本光标放在要记录的元素上（例如，一种方法）。

2. 执行下列操作之一：

   - 在 C# 中键入 `///` 或在 Visual Basic 中键入 `'''`

   - 在“编辑”菜单上，选择“IntelliSense” > “插入注释”

   - 在代码元素上或其正上方的右键单击或上下文菜单中，选择“代码段” > “插入代码段”

   随即基于代码元素生成 XML 模板。 例如，对方法进行注释时，它会生成 \<summary\> 元素，针对每个参数生成一个 \<param\> 元素，并生成一个记录返回值的 \<returns\> 元素  。

   ![XML 注释模板 - C#](media/doc-preview-cs.png)

   ![XML 注释模板 - Visual Basic](media/doc-preview-vb.png)

3. 为每个 XML 元素输入说明以完整记录代码元素。

   ![此屏幕截图显示了完成的注释。](media/doc-result-cs.png)

你可以在 XML 注释中使用样式，将鼠标悬停在元素上时这些样式将在“快速信息”中呈现。 这些样式包括：斜体、粗体、项目符号和可单击的链接。

   ![此屏幕截图显示了完成的注释，包含斜体、粗体、项目符号和可单击链接的样式标记。](media/doc-style-cs.png)

> [!NOTE]
> 在 C# 中键入`///`（或在 Visual Basic 中键入 `'''`）后，可[选择](../../ide/reference/options-text-editor-csharp-advanced.md)切换 XML 文档注释。 在菜单栏中，选择“工具” > “选项”以打开“选项”对话框。 然后，导航到“文本编辑器” > “C#”或导航到“基本” > “高级”。 在“编辑器帮助”部分，查找“生成 XML 文档注释”选项   。

## <a name="see-also"></a>请参阅

- [使用 XML 注释来记录代码（C# 指南）](/dotnet/csharp/language-reference/xmldoc/)
- [如何：创建 XML 文档 (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/how-to-create-xml-documentation)
- [C++ 注释](/cpp/cpp/comments-cpp)
- [XML 文档 (C++)](/cpp/build/reference/xml-documentation-visual-cpp)
- [代码生成](../code-generation-in-visual-studio.md)
