---
title: VSCT 编译器Command-Line标志|Microsoft Docs
description: 命令Visual Studio编译器提供命令行选项，以确保成功编译 .vsct 文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT files, compiling
- command-table file compilation (VSCT files)
ms.assetid: 9dc6c33f-e6cf-4cf2-9b05-e8f7bfac1cfb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: de48995abe6547b9f73c27a3c749609e8f99cfd8c8f17aa74f5200106238d205
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121375427"
---
# <a name="vsct-compiler-command-line-flags"></a>VSCT 编译器命令行标志
VSCT Visual Studio 命令 (编译器) 命令行开关，以确保成功编译 .vsct 文件。

## <a name="command-line-parameters"></a>命令行参数
 若要查看命令窗口中的基本 VSCT 帮助，请导航到 Visual Studio [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]  *SDK 安装路径*\VisualStudioIntegration\Tools\Bin\ 文件夹并键入：

```
vsct /?
```

 这将返回以下内容：

```
Microsoft (R) Visual Studio (R) Command Table Compiler Version 3.00.2000

Syntax: vsct <infile> [<outfile>] [-S[symbols file]] [-D<preprocessor-define>]*
[-I<include-path>]* [-L<language>] [-E[C|H|N]:<name>]

  -D    Specify any additional preprocessor defines
  -I    Indicate what additional include paths to send to the preprocessor
  -L    Specify the language to use when selecting strings
  -E    Emit C# objects in the specified namespace for command items,
        followed by [L|F|H|N]:<value>
        F = Name of the file to emit (used if -EL is provided)
        L = Name of a language providing a CodeDOM provider
        N = namespace (required if -EL is provided)
        H = C++ header
  -c    Clean build skipping dependency checks
  -v    Verbose output
```

> [!NOTE]
> 字符 - (短划线) 和/ (正斜杠) 表示法，用于指示命令行参数。

 可接受的标志及其含义如下所示。

|开关|说明|
|------------|-----------------|
|-d|指定任何其他定义的符号。|
|-I|指示解析文件引用时应当使用的其他包含路径。|
|-l|指定 <xref:System.Globalization.CultureInfo> 区域性名称，例如"en-US"。|
|-E|为命令项发出指定命名空间中的 C# 对象，后跟 [C&#124;H&#124;N]：*filename* where C = C#， H = C++ header， N = namespace。 C# 需要 命名空间。|
|-v|详细输出。|

 -L 开关指示编译器选择一组字符串，以生成与给定区域性名称相对应的二进制 .cto <xref:System.Globalization.CultureInfo> 文件。 指定的区域性名称应匹配 .vsct 文件中一个或多个 [Strings 元素](../../extensibility/strings-element.md) 的 Language 属性。 如果 Strings 元素没有 Language 属性，则它继承自包含 [CommandTable 元素](../../extensibility/commandtable-element.md)。

 .vsct 文件可能有多个 Strings 元素，并且每个元素可能具有不同的 Language 属性。 全球化是通过多次运行 VSCT 编译器并更改每个区域性名称的 -L 开关实现的。

 如果 -L 开关给定的区域性名称与任何 Strings 元素的 Language 属性不匹配，编译器将尝试匹配语言，而不是区域。 例如，如果找不到"en-US"，编译器将改为尝试"en"。 如果失败，它将尝试操作系统的当前区域性。 如果失败，它将编译找到的第一个 Strings 元素。

 -E 开关可用于发出包含命令表使用的符号的 C 样式头文件，或发出包含命令符号对象的 C# 文件。

 -D 和 -I 开关具有同名Cl.exe C 预处理器标志的语法。 格式为 X=Y 的 -D 定义用于扩展属性中基于 XML \<Defined> `Condition` 的测试。 -I include 路径用于解析 \<Include> 、 \<Extern> 和 \<Bitmap> 文件引用。 有关详细信息，请参阅 [VSCT XML 架构引用](../../extensibility/vsct-xml-schema-reference.md)。

 VSCT 编译器还可以取消编译以前构建的二进制文件。 为此，请为 提供二进制文件 \<infile> 。   如果二进制文件由 VSCT 编译器生成，它将已嵌入其符号，并且将在输出的一节中生成具有符号名称 \<Symbols> 的输出。 如果二进制文件是由 COMPILER 编译器生成的，则输出将包含实际 GUID 和 ID。 如果当前版本的 Ctc.exe 生成的 *.ctsym 文件与二进制输入文件位于同一文件夹中，则符号将从该文件加载并用于输出。

## <a name="see-also"></a>另请参阅
- [Visual Studio 命令表格 (.Vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)
- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
