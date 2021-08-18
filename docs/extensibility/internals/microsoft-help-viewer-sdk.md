---
title: Microsoft Help Viewer SDK |Microsoft Docs
description: 了解Visual Studio查看器任务，例如创建文章、创建 Help Viewer 内容品牌包和部署一组文章。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 620d7dcd-d462-475e-a449-fbfa06ff12c5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 5ea294f29359e60764b2d6b3f2237bdc1f72cfdc
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122102594"
---
# <a name="microsoft-help-viewer-sdk"></a>Microsoft Help Viewer SDK

本文包含帮助查看器集成Visual Studio以下任务：

- 创建 F1 (主题) 

- 创建 Help Viewer 内容品牌包

- 部署一组文章

- 将帮助添加到集成Visual Studio或 (shell) 

- 其他资源

## <a name="create-a-topic-f1-support"></a>创建 F1 (主题) 

本部分概述了所呈现主题的组件、主题要求、如何创建主题的简短说明 (包括 F1 支持要求) 最后提供了一个示例主题及其呈现的结果。

**Help Viewer 主题概述**

当调用主题进行呈现时，帮助查看器将获取在安装或上次更新时与该主题关联的品牌包元素以及主题 XHTML，并合并这两个元素，以产生显示的内容视图 (品牌数据 + 主题数据) 。  品牌包包含徽标、内容行为支持、品牌文本 (版权等) 。  有关品牌包元素的详细信息，请参阅下面的"创建品牌包"。  如果没有与主题关联的品牌包，帮助查看器将使用 Help Viewer 应用程序根目录 (Branding_en-US.mshc) 中的回退品牌包。

**Help Viewer 主题要求**

若要在帮助查看器中正确呈现，原始主题内容必须是 W3C Basic 1.1 XHTML。

主题通常包含两个部分：

- 元数据 (元数据参考) ：有关主题的数据，例如主题唯一 ID、关键字值、主题 TOC ID、父节点 ID 等。

- 正文内容：符合 W3C Basic 1.1 XHTML，其中包括可折叠区域 (代码片段等支持的内容行为。完整列表如下所示) 。

Visual Studio品牌包支持的控件：

- 链接

- CodeSnippet

- 可折叠区域

- 继承的成员

- LanguageSpecificText

支持的语言字符串 (不区分大小写) ：

- javascript

- csharp 或 c#

- cplusplus、visualc++ 或 c++

- jscript

- visualbasic 或 vb

- f# 、fsharp 或 fs

- 其他 - 表示语言名称的字符串

**创建帮助查看器主题**

创建名为 ContosoTopic4.htm 的新 XHTML 文档，并在下面 (标题) 。

```html
<html>
<head>
<title>Contoso Topic 4</title>
</head>

<body>

</body>
</html>

```

接下来，添加数据以定义主题的呈现方式 (自品牌或不为) ，如何为 F1 引用本主题，其中本主题存在于 TOC 中，其 ID (供其他主题) 等链接参考。有关支持的元数据的完整列表，请参阅下面的"内容元数据"表。

- 在这种情况下，我们将使用自己的品牌包，这是帮助查看器品牌包Visual Studio的变体。

- 将 F1 元名称和值 ("Microsoft.Help.F1"content=" ContosoTopic4") ，与 IDE 属性包中提供的 F1 值匹配。  (有关详细信息，请参阅 F1 支持部分。) 在 IDE 中选择了 F1 时，此值与 IDE 中的 F1 调用匹配以显示本主题。

- 添加主题 ID。 这是其他主题用来链接到本主题的字符串。 它是本主题的帮助查看器 ID。

- 对于 TOC，请添加本主题的父节点，以定义本主题 TOC 节点的显示位置。

- 对于 TOC，添加本主题的节点顺序。 当父节点具有 `n` 子节点数时，按子节点的顺序定义本主题的位置。 例如，本主题是 4 个子主题中的数字 4。

示例元数据部分：

```html
<html>
<head>
<title>Contoso Topic 4</title>

<meta name="SelfBranded" content="false" />
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <meta name="Microsoft.Help.Id" content="ContosoTopic4" />
<meta name="Microsoft.Help.F1" content=" ContosoTopic4" />
    <meta name="Language" content="en-us" />
<meta name="Microsoft.Help.TocParent" content="ContosoTopic0" />
<meta name="Microsoft.Help.TocOrder" content="4" />

</head>

<body>

</body>
</html>
```

**主题正文**

不包含 (页眉和页脚) 正文将包含页面链接、备注部分、可折叠区域、代码片段和特定于语言的文本部分。  有关所介绍主题的这些方面的信息，请参阅品牌部分。

1. 添加主题标题标记：  `<div class="title">Contoso Topic 4</div>`

2. 添加备注部分： `<div class="alert"> add your table tag and text </div>`

3. 添加可折叠区域：  `<CollapsibleArea Expanded="1" Title="Collapsible Area Test Heading"> add text  </CollapsibleArea>`

4. 添加代码片段：  `<CodeSnippet EnableCopyCode="true" Language="CSharp" ContainsMarkup="false" DisplayLanguage="C#" > a block of code </CodeSnippet>`

5. 添加特定于代码语言的文本  `<LanguageSpecificText devLangcs="CS" devLangvb="VB" devLangcpp="C++" devLangnu="F#" />` ：请注意，允许 `devLangnu=` 输入其他语言。 例如，当 `devLangnu="Fortran"` 代码片段 DisplayLanguage = Fortran 时显示 Fortran

6. 添加页面链接： `<a href="ms-xhelp:///?Id=ContosoTopic1">Main Topic</a>`

> [!NOTE]
> 注意：对于不支持的新"显示语言" (，代码片段中的 F#、Cobol、Fortran) 代码着色将是单色的。

**帮助查看器主题示例** 该代码演示如何定义元数据、代码片段、可折叠区域以及特定于语言的文本。

```html
<?xml version="1.0" encoding="utf-8"?>
<html>
<head>
<title>Contoso Topic 4</title>

    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <meta name="Microsoft.Help.Id" content="ContosoTopic4" />
<meta name="Microsoft.Help.F1" content=" ContosoTopic4" />
    <meta name="Language" content="en-us" />
<meta name="Microsoft.Help.TocParent" content="ContosoTopic0" />
<meta name="Microsoft.Help.TocOrder" content="4" />
<meta name="SelfBranded" content="false" />
</head>

<body>
<div class="title">Contoso Topic 4</div>

  <div id="header">
<table id="bottomTable" cellpadding="0" cellspacing="0"  width="100%">
        <tr id="headerTableRow2"><td align="left">
            <span id="nsrTitle">Contoso Topic 1</span>
          </td>
<td align="right">
</td></tr>
<tr id="headerTableRow1"><td align="left">
            <span id="runningHeaderText">Contoso Widgets & Sprockets</span>
          </td></tr>
      </table>
</div>

<h2>Table of Contents</h2>

<ul class="toc">
<li class="tocline1"><a href="#introduction" target="_self">1.0 Introduction</a></li>
<li class="tocline1"><a href="#seealso" target="_self">See Also</a></li>
</ul>

<div class="topic">

<div id="mainSection">
<div id="mainBody">

<a name="introduction"></a>
<h2>1.0 Introduction</h2>
<p>[This documentation is for sample purposes only.]</p>

<p>Contoso Topic 1 contains examples of:
<ul>
<li>Collapsible Area</li>
<li>Bookmark ("See also")</li>
<li>Code Snippets from Branding Package</li>
</ul>
 </p>
<div class="alert"><table><tr><th>
<strong>Note </strong></th></tr>
<tr><td>
<p>This is an example of a <span class="label">Note </span>section.
Call out important items for your reader in this <span class="label">Note </span>box.
</p></td></tr>
</table>
</div>
</div>

<CollapsibleArea Expanded="1" Title="Collapsible Area Test Heading">

            <a id="sectionToggle0"><!----></a>

<div>
Example of Collapsible Area
<br/>
Lorem ipsum dolor sit amet...
</div>
</CollapsibleArea>

<div id="snippetGroup" >
<CodeSnippet EnableCopyCode="true" Language="VisualBasic" ContainsMarkup="false" DisplayLanguage="Visual Basic" >
Private Sub ToolStripRenderer1_RenderGrip(sender as Object, e as ToolStripGripRenderEventArgs) _ Handles ToolStripRenderer1.RenderGrip
Dim messageBoxVB as New System.Text.StringBuilder()
    messageBoxVB.AppendFormat("{0} = {1}", "GripBounds", e.GripBounds)
    messageBoxVB.AppendLine()
 ...
    MessageBox.Show(messageBoxVB.ToString(),"RenderGrip Event")
End Sub
</CodeSnippet>

<CodeSnippet EnableCopyCode="true" Language="CSharp" ContainsMarkup="false" DisplayLanguage="C#" >
private void ToolStripRenderer1_RenderGrip(Object sender, ToolStripGripRenderEventArgs e)
{
System.Text.StringBuilder messageBoxCS = new System.Text.StringBuilder();
messageBoxCS.AppendFormat("{0} = {1}", "GripBounds", e.GripBounds );
messageBoxCS.AppendLine();
...
MessageBox.Show(messageBoxCS.ToString(), "RenderGrip Event" );
}
</CodeSnippet>

<CodeSnippet EnableCopyCode="true" Language="fsharp" ContainsMarkup="false" DisplayLanguage="F#" >
some F# code
</CodeSnippet>
</div>

<h4 class="subHeading">Example of code specific text</h4>Language = <LanguageSpecificText devLangcs="CS" devLangvb="VB" devLangcpp="C++" devLangnu="F#" />

<a name="seealso"></a>
<h1 class="heading">See Also</h1>

    <div id="seeAlsoSection" class="section">
    <div class="seeAlsoStyle">
        <a href="ms-xhelp:///?Id=ContosoTopic1">Main Topic</a>
    </div>
 </div>
</div>
</div>
</body>
</html>
```

**F1 支持**

在 Visual Studio中，选择 F1 会生成从光标在 IDE 中的位置提供的值，并使用基于游标位置提供 (填充"属性包"。 当光标位于功能 x 上时，功能 x 处于活动状态/焦点为焦点，并使用值填充属性包。  选择 F1 时，将填充属性包，Visual Studio F1 代码将查看客户的默认帮助源是本地还是联机 (联机是默认) ， 然后根据用户设置创建适当的字符串 (online 是默认的) - shell 执行 (请参阅 exe launch 参数的帮助管理员指南) 以及本地帮助查看器的参数 + 属性包中的关键字 (s) （如果本地帮助是默认值）或参数列表中具有 关键字的 MSDN URL。

如果为 F1 返回了三个字符串（称为多值字符串），则采用第一个术语，查找命中，如果找到，则完成操作;如果没有，则移动到下一个字符串。  顺序很重要。 多值关键字的表示形式应为最长字符串到最短字符串。  若要在多值关键字的情况下验证这一点，请检查联机 F1 URL 字符串，该字符串将包含所选的关键字。

在 Visual Studio 2012 中，我们有意在联机和脱机之间进行了更强的划分，因此，如果用户的设置是"联机"，则只需将 F1 请求直接传递到 MSDN 上的联机查询服务，而不是通过 Visual Studio 2010 中提供的帮助库代理进行路由。 然后，我们依靠"供应商内容已安装 = true"状态来确定是否执行该上下文中的不同操作。 如果为 true，则根据你希望为客户提供的支持来执行此分析和路由逻辑。 如果为 false，则只需转到 MSDN。 如果用户设置为"本地"，则所有调用都转到本地帮助引擎。

F1 Flow关系图：

![F1 流](../../extensibility/internals/media/f1flow.png "F1flow")

当帮助查看器的默认帮助内容源设置为联机 (浏览器中启动) ：

- Visual Studio合作伙伴 (VSP) 功能向 F1 属性包 (属性包 prefix.keyword 和联机 URL 发出一个值，该值用于注册表) ：F1 将 VSP URL+ 参数发送到浏览器。

- Visual Studio语言 (、Visual Studio菜单项等功能) ：F1 将Visual Studio URL 发送到浏览器。

当帮助查看器的默认帮助内容源设置为本地帮助 (在帮助查看器中启动) ：

- VSP 功能，其中关键字在 F1 属性包和本地存储索引之间匹配 (也就是说，属性包 prefix.keyword = 在本地存储索引) ：F1 在帮助查看器中呈现主题。

- Visual Studio功能 (VSP 无法替代从 Visual Studio 功能发出的属性包) ：F1 在帮助查看器中呈现 Visual Studio 主题。

设置以下注册表值，为供应商帮助内容启用 F1 回退。 F1 回退意味着帮助查看器设置为联机查找 F1 帮助内容，供应商内容在本地安装到用户的硬盘驱动器上。 帮助查看器应查看内容的本地帮助，即使默认设置用于联机帮助。

1. 设置 Help 2.3 注册表项下的 **VendorContent** 值：

   - 对于 32 位操作系统：

        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.3\Catalogs\VisualStudio15

        "VendorContent"=dword：00000001

   - 对于 64 位操作系统：

        HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

        "VendorContent"=dword：00000001

2. 在 Help 2.3 注册表项下注册合作伙伴命名空间：

   - 对于 32 位操作系统：

      <em> \\ HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.3\Partner<命名空间 \> </em>

      "location"="offline"

   - 对于 64 位操作系统：

      <em> \\ HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Partner<命名空间 \> </em>

      "location"="offline"

**基本本机命名空间分析**

若要启用基本本机命名空间分析，请在注册表中按以下名称添加一个新的 DWORD： BaseNativeNamespaces，并将其值设置为 1 (要支持的目录项) 。  例如，如果想要使用 Visual Studio 目录，则可以将该密钥添加到路径中：

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

如果遇到格式标头/方法中的 F1 关键字，将会分析 "/" 字符，从而导致以下构造：

- 标头：将是可用于在注册表中注册的命名空间

- 方法：这将成为通过传递的关键字。

例如，假设有一个名为 CustomLibrary 的自定义库和一个名为 MyTestMethod 的方法，当 F1 请求进入时，它的格式将设置为 `CustomLibrary/MyTestMethod` 。

然后，用户可以将 CustomLibrary 注册为合作伙伴 hive 下的命名空间，并提供所需的任何位置键，并且传递给查询的关键字将为 MyTestMethod。

**在 IDE 中启用帮助调试工具**

添加以下注册表项和值：

::: moniker range="vs-2017"

**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\15.0\Dynamic Help**

::: moniker-end

::: moniker range=">=vs-2019"

**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\16.0\Dynamic Help**

::: moniker-end

值：在零售数据中显示调试输出：是

在 IDE 的 "帮助" 菜单项下，选择 " **调试帮助上下文**"。

**内容元数据**

在下表中，括在括号中的任何字符串都是一个必须被识别的值替换的占位符。 例如，在中 \<meta name="Microsoft.Help.Locale" content="[language code]" /> ，必须将 "[language code]" 替换为 "en-us" 之类的值。

|  (HTML 表示形式的属性)  | 说明 |
| - | - |
| \< meta name="Microsoft.Help.Locale" content="[language-code]" /> | 为此主题设置区域设置。 如果在主题中使用此标记，则必须只使用一次，并且必须将其插入到任何其他 Microsoft 帮助标记之上。 如果未使用此标记，则将使用与产品区域设置相关联的断字符（如果已指定）对主题的正文文本进行索引。否则，将使用 en-us 断字符。 此标记符合 ISOC RFC 4646。 若要确保 Microsoft 帮助正常工作，请使用此属性而不是 "常规语言" 属性。 |
| \< meta name="Microsoft.Help.TopicLocale" content="[language-code]" /> | 如果还使用了其他区域设置，则设置本主题的区域设置。 如果在主题中使用此标记，则必须只使用一次。 当目录包含多种语言的内容时，请使用此标记。 目录中的多个主题可以具有相同的 ID，但每个主题都必须指定唯一的 TopicLocale。 指定与目录的区域设置匹配的 TopicLocale 的主题是在目录中显示的主题。 但是，该主题的所有语言版本都将显示在搜索结果中。 |
| \< title>词首\</title> | 指定本主题的标题。 此标记是必需的，必须在主题中仅使用一次。 如果主题正文不包含标题 \<div> 部分，则此标题将显示在主题和目录中。 |
| \< meta name=" Microsoft.Help.Keywords" content="[aKeywordPhrase]"/> | 指定在帮助查看器的 "索引" 窗格中显示的链接文本。 单击此链接时，将显示该主题。 您可以为一个主题指定多个索引关键字，如果您不希望该主题的链接显示在索引中，也可以省略此标记。 可以将早期版本的帮助中的 "K" 关键字转换为此属性。 |
| \< meta name="Microsoft.Help.Id" content="[TopicID]"/> | 设置该主题的标识符。 此标记是必需的，必须在主题中仅使用一次。 此 ID 必须在目录中具有相同区域设置的主题中是唯一的。 在另一个主题中，你可以使用此 ID 创建指向此主题的链接。 |
| \< meta name="Microsoft.Help.F1" content="[System.Windows.Controls.Primitives.IRecyclingItemContainerGenerator]"/> | 指定本主题的 F1 关键字。 您可以为一个主题指定多个 F1 关键字，如果您不希望在应用程序用户按 F1 时显示此主题，则可以省略此标记。 通常，为主题指定一个 F1 关键字。 可以将早期版本的帮助中的 "F" 关键字转换为此属性。 |
| \< meta name="Description" content="[topic description]" /> | 提供本主题内容的简短摘要。 如果在主题中使用此标记，则必须只使用一次。 此属性可由查询库直接访问;它不存储在索引文件中。 |
| meta name = "TocParent" content = "[parent_Id]"/> | 在目录中指定本主题的父主题。 此标记是必需的，必须在主题中仅使用一次。 该值是父级的 Microsoft.Help.Id。 一个主题在目录中只能有一个位置。 "-1" 被视为 TOC 根的主题 ID。 在中 [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] ，该页是 Help Viewer 主页。 这是因为我们将 TocParent =-1 专门添加到一些主题，以确保它们显示在顶级。 Help Viewer 主页是系统页面，因此不可替换。 如果 VSP 尝试添加 ID 为-1 的页，则它可能会添加到内容集，但是 Help Viewer 将始终使用系统页-Help Viewer Home |
| \< meta name="Microsoft.Help.TocOrder" content="[positive integer]"/> | 指定本主题在目录中相对于其对等主题显示的位置。 此标记是必需的，必须在主题中仅使用一次。 该值是一个整数。 指定一个较低值的整数的主题将显示在指定值较大的主题的上方。 |
| \< meta name="Microsoft.Help.Product" content="[product code]"/> | 指定本主题描述的产品。 如果在主题中使用此标记，则必须只使用一次。 此信息还可以作为传递到帮助索引器的参数提供。 |
| \< meta name="Microsoft.Help.ProductVersion" content="[version number]"/> | 指定本主题描述的产品版本。 如果在主题中使用此标记，则必须只使用一次。 此信息还可以作为传递到帮助索引器的参数提供。 |
| \< meta name="Microsoft.Help.Category" content="[string]"/> | 由产品用于标识内容的子部分。 您可以为某个主题标识多个子部分，如果您不希望链接识别任何子节，则可以省略此标记。 此标记用于存储在从帮助的早期版本转换主题时 TargetOS 和 TargetFrameworkMoniker 的属性。 内容的格式为 AttributeName： AttributeValue。 |
| \< meta name="Microsoft.Help.TopicVersion content="[topic version number]"/> | 如果目录中存在多个版本，则指定主题的此版本。 由于 Microsoft.Help.Id 不一定是唯一的，因此，如果目录中存在多个版本的主题，则需要此标记，例如，当目录包含有关 .NET Framework 3.5 的主题和 .NET Framework 4 的主题并且两者都具有相同的 Microsoft.Help.Id 时。 |
| \< meta name="SelfBranded" content="[TRUE or FALSE]"/> | 指定本主题是使用帮助库管理器启动品牌包还是特定于该主题的品牌包。 此标记必须为 TRUE 或 FALSE。 如果为 TRUE，则相关主题的品牌包将重写在帮助库管理器启动时设置的品牌包，以便即使该主题与其他内容的呈现不同，也会呈现该主题。 如果为 FALSE，则根据帮助库管理器启动时设置的品牌包呈现当前主题。 默认情况下，帮助库管理器假定自品牌为 false，除非 SelfBranded 变量声明为 TRUE;因此，您无需声明 \<meta name="SelfBranded" content="FALSE"/> 。 |

## <a name="create-a-branding-package"></a>创建品牌包

Visual Studio 版本包含许多不同的 Visual Studio 产品，其中包括用于 Visual Studio 合作伙伴的独立和集成 shell。  其中每个产品都需要某种程度上基于主题的帮助内容品牌支持，这对于产品是唯一的。  例如，Visual Studio 主题需要具有一致的品牌表示形式，而用于包装 ISO Shell 的 SQL Studio 需要每个主题的唯一帮助内容品牌。  集成外壳合作伙伴可能希望其帮助主题位于父 Visual Studio 产品帮助内容中，同时保持其自己的主题品牌。

品牌包由包含帮助查看器的产品安装。  对于 Visual Studio 产品：

- 在 \<locale> Help viewer 2.3 应用程序根中安装了 (Branding_ .mshc) 的后备署名包 (示例： C:\Program Files (x86) \Microsoft help Viewer\v2.3 通过 Help viewer 语言包) 。  这适用于未安装产品品牌包 (未安装任何内容) 或安装的品牌包损坏的情况。  使用应用根后备署名包时，将忽略 Visual Studio 元素 (徽标和反馈) 。

- 从内容包服务安装 Visual Studio 内容时，还会在第一次) 内容安装方案时 (安装品牌包。  如果有对署名包的更新，则在发生 "下一内容更新" 或 "其他包安装" 操作时，会安装更新。

Microsoft Help Viewer 支持基于主题元数据的主题标记。

- 如果主题元数据定义自行品牌为 true，则按原样呈现主题， (品牌) 的任何内容。

- 如果主题元数据定义自品牌 = false，请使用与 TopicVendor metadata 值相关联的品牌包。

- Where 主题 metadata 定义 name = "TopicVendor" content = \< branding package name in vendor MSHA> ，请使用内容值中定义的品牌包。

- 在 Visual Studio 目录中，有一个优先级应用程序的品牌包。  首先 Visual Studio 应用默认署名，然后，如果在主题元数据中定义，并在与安装 .msha) 中定义的关联品牌包 (支持，则会将供应商定义的品牌作为替代应用。

品牌元素通常分为三个主要类别：

- 标头元素 (示例包括反馈链接、条件免责声明文本、徽标) 

- 内容行为 (例如，展开/折叠控件文本元素和代码片段元素) 

- 页脚元素 (示例版权) 

被视为署名元素的项包括此规范中 (详细说明) ：

- 目录/产品徽标 (示例，Visual Studio) 

- 反馈链接和电子邮件元素

- 免责声明文本

- 版权文本

Visual Studio 帮助查看器署名包中的支持文件包括：

- 图形 (徽标、图标等 ) 

- Branding.js-支持内容行为的脚本文件

- Branding.xml-始终跨目录内容使用的字符串。  注意：若要在 branding.xml 中 Visual Studio 本地化文本元素，请包括 _locID = " \<unique value> "

- 品牌。 css 样式定义以实现演示一致性

- 打印 css 样式的样式定义

如上所述，品牌包与主题相关联：

- 如果在元数据中定义了 SelfBranded = false，该主题将继承目录署名包

- 或者，当 SelfBranded = false 并且在 .MSHA 中定义了唯一的品牌包，并且在安装内容时可用

对于用于实现自定义品牌包 (VSP 内容、SelfBranded = True) 的 .Vsps，一种继续操作的方法是从 (与帮助查看器) 一起安装的后备署名包开始，并根据需要更改文件的名称。  Branding_ \<locale> .mshc 文件是文件扩展名更改为 .mshc 的 zip 文件，因此只需将扩展名从 .mshc 更改为 .zip 并提取内容。  请参阅下面的品牌包元素，并根据需要进行修改 (例如，将徽标更改为 VSP 徽标，并将对 Branding.xml 文件中的徽标的引用、更新 Branding.xml 每个 VSP 的详细信息 ) 等。

完成所有修改后，创建一个包含所需品牌元素的 zip 文件，并将扩展名更改为 .mshc。

若要关联自定义品牌包，请创建 .MSHA，其中包含对品牌 .mshc 文件的引用，以及包含) 主题的 content .mshc (。  有关如何创建基本 .MSHA 的说明，请参阅下面的 ".MSHA"。

Branding.xml 文件包含一个元素列表，其中的元素用于在主题包含时一致地呈现主题中的特定项 \<meta name="Microsoft.Help.SelfBranded" content="false"/> 。  下面列出了 Branding.xml 文件中元素的 Visual Studio 列表。  此列表旨在用作 ISO Shell 用户的模板，在该模板中，他们修改这些元素 (例如徽标、反馈和版权) ，以满足其自己的产品品牌需求。

注意： "{n}" 标记的变量具有代码依赖项，删除或更改这些值会导致错误，并可能导致应用程序崩溃。 Visual Studio 品牌包中包含本地化标识符 (示例 _locID = "codesnippet" ) 。

**Branding.xml**

| 元素 | 说明 |
| - | - |
| 功能： | **CollapsibleArea** |
| 使用： | 展开折叠内容控件文本 |
| **元素** | 值 |
| ExpandText | 展开 |
| CollapseText | 折叠 |
| 功能： | **CodeSnippet** |
| 使用： | 代码片段控件文本。  注意： "不间断" 空间的代码片段内容将更改为空间。 |
| **元素** | 值 |
| CopyToClipboard | 复制到剪贴板 |
| ViewColorizedText | 查看着色 |
| CombinedVBTabDisplayLanguage | Visual Basic (示例)  |
| VBDeclaration | 声明 |
| VBUsage | 使用情况 |
| 功能： | **反馈、页脚和徽标** |
| 使用： | 为客户提供反馈控制，以通过电子邮件提供当前主题的反馈。  内容的版权文本。  徽标定义。 |
| **元素** | **值 (可以修改这些字符串以满足所采纳的内容。 )** |
| 版权声明 | © 2013 微软公司。 All rights reserved. |
| SendFeedback | \<a href="{0}" {1}>向 \</a> Microsoft 发送有关本主题的反馈。 |
| No-results-found-feedbacklink | |
| LogoTitle | [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] |
| LogoFileName | vs_logo_bk.gif |
| LogoFileNameHC | vs_logo_wh.gif |
| 功能： | **免责声明** |
| 使用： | 计算机翻译内容的一组案例特定免责声明。 |
| **元素** | 值 |
| MT_Editable | 本文进行了机器翻译。 如果你有 Internet 连接，请选择 "联机查看本主题" 以在可编辑模式下查看此页面，同时提供原始英语内容。 |
| MT_NonEditable | 本文进行了机器翻译。 如果你有 Internet 连接，请选择 "联机查看本主题" 以在可编辑模式下查看此页面，同时提供原始英语内容。 |
| MT_QualityEditable | 本文已手动翻译。 如果你有 Internet 连接，请选择 "联机查看本主题" 以在可编辑模式下查看此页面，同时提供原始英语内容。 |
| MT_QualityNonEditable | 本文已手动翻译。 如果你有 Internet 连接，请选择 "联机查看本主题" 以在可编辑模式下查看此页面，同时提供原始英语内容。 |
| MT_BetaContents | 本文是针对预发布版本的机器翻译。 如果你有 Internet 连接，请选择 "联机查看本主题" 以在可编辑模式下查看此页面，同时提供原始英语内容。 |
| MT_BetaRecycledContents | 本文是针对初步版本手动翻译的。 如果已建立 Internet 连接，请选择"联机查看本主题"，以可编辑模式同时查看包含原始英语内容的此页面。 |
| 功能： | **LinkTable** |
| 使用： | 支持联机主题链接 |
| **元素** | 值 |
| LinkTableTitle | 链接表 |
| TopicEnuLinkText | 查看计算机上提供的本主题 \</a> 的英语版本。 |
| TopicOnlineLinkText | 联机查看 \<a href="{0}" {1}> 本主题\</a> |
| OnlineText | 联机 |
| 功能： | **视频音频控件** |
| 使用： | 显示视频内容的元素和文本 |
| **元素** | 值 |
| MultiMediaNotSupported | Internet Explorer安装 9 或更大版本以支持 {0} 内容。 |
| VideoText | 显示视频 |
| AudioText | 流式处理音频 |
| OnlineVideoLinkText | \<p>若要查看与本主题关联的视频，请单击此处 {0} \<a href="{1}"> {2} \</a> 。\</p> |
| OnlineAudioLinkText | \<p>若要侦听与本主题关联的音频，请单击此处 {0} \<a href="{1}"> {2} \</a> 。\</p> |
| 功能： | **内容未安装控件** |
| 使用： | 文本元素 (字符串) 用于呈现contentnotinstalled.htm |
| **元素** | 值 |
| ContentNotInstalledTitle | 计算机上未找到任何内容。 |
| ContentNotInstalledDownloadContentText | \<p>若要将内容下载到计算机，请单击 \<a href="{0}" {1}> "管理"选项卡 \</a> 。\</p> |
| ContentNotInstalledText | \<p>计算机上未安装任何内容。 有关本地帮助内容安装，请参阅管理员。\</p> |
| 功能： | **"找不到主题"控件** |
| 使用： | 文本元素 (字符串) 用于呈现topicnotfound.htm |
| **元素** | 值 |
| TopicNotFoundTitle | 在计算机上找不到请求的主题。 |
| TopicNotFoundViewOnlineText | \<p>计算机上找不到你请求的主题，但你可以 \<a href="{0}" {1}> 联机查看该主题 \</a> 。\</p> |
| TopicNotFoundDownloadContentText | \<p>有关类似主题的链接，请参阅导航窗格，或单击"管理 \<a href="{0}" {1}> "选项卡 \</a> 将内容下载到计算机。\</p> |
| TopicNotFoundText | \<p>计算机上找不到你请求的主题。\</p> |
| 功能： | **主题损坏控件** |
| 使用： | 文本元素 (字符串) 用于呈现topiccorrupted.htm |
| **元素** | 值 |
| TopicCorruptedTitle | 无法显示请求的主题。 |
| TopicCorruptedViewOnlineText | \<p>帮助查看器无法显示请求的主题。 主题的内容或基础系统依赖项中可能有错误。\</p> |
| 功能： | **主页控件** |
| 使用： | 支持显示帮助查看器顶级节点内容的文本。 |
| **元素** | 值 |
| HomePageTitle | 帮助查看器主页 |
| HomePageIntroduction | \<p>欢迎使用 Microsoft Help Viewer，这是使用 Microsoft 工具、产品、技术和服务的每个人的基本信息源。 使用帮助查看器可以访问帮助和参考信息、示例代码、技术文章等。 若要查找所需的内容，请浏览目录、使用全文搜索或使用关键字索引浏览内容。\</p> |
| HomePageContentInstallText | \<p>\<br />使用 \<a href="{0}" {1}> "管理 \</a> 内容"选项卡执行以下操作： \<ul> \<li> 将内容添加到计算机。 \</li> \<li>检查本地内容更新。 \</li> \<li>从计算机中删除内容。\</li>\</ul>\</p> |
| HomePageInstalledBooks | 已安装的书籍 |
| HomePageNoBooksInstalled | 计算机上未找到任何内容。 |
| HomePageHelpSettings | 帮助内容设置 |
| HomePageHelpSettingsText | \<p>当前设置是本地帮助。 帮助查看器显示计算机上安装的内容。 \<br />若要更改帮助内容的源，请选择菜单栏上的Visual Studio"帮助 \<span style="{0}"> "，然后选择"设置帮助首选项 \</span> "。\<br />\</p> |
| 兆 字节 | MB |

**branding.js**

此branding.js包含帮助查看器品牌元素Visual Studio使用的 JavaScript。  下面是品牌元素和支持的 JavaScript 函数的列表。  此文件顶部的"可本地化字符串"部分中定义了要对此文件本地化的所有字符串。  ICL 文件已针对文件内的 loc branding.js创建。

|**品牌功能**|**JavaScript 函数**|**说明**|
|-|-|-|
|无 功。。。||定义变量|
|获取用户代码语言|setUserPreferenceLang|将索引 # 映射到代码语言|
|设置和获取 Cookie 值|getCookie、setCookie||
|继承的成员|changeMembersLabel|展开/折叠继承的成员|
|当 SelfBranded=False 时|onLoad|读取查询字符串，检查其是否为打印请求。  设置所有代码nippets 以重点关注用户首选选项卡。 如果是打印请求，则将 isPrinterFriendly 设置为 true。 检查高对比度模式。|
|代码片段|addSpecificTextLanguageTagSet||
||getIndexFromDevLang||
||ChangeTab||
||setCodesnippetLang||
||setCurrentLang||
||CopyToClipboard||
|可折叠区域|addToCollapsibleControlSet|将所有可折叠控件对象写入列表。|
||CA_Click|根据可折叠区域的状态，定义要呈现的图像和文本|
|徽标的对比度支持|isBlackBackground () |调用以确定背景是否为黑色。  仅在高对比度模式下才准确。|
||isHighContrast () |使用彩色范围检测高对比度模式|
||onHighContrast (黑色) |检测到高对比度时调用|
|LST 功能|||
||addToLanSpecTextIdSet (id) ||
||updateLST (currentLang) ||
||getDevLangFromCodeSnippet (lang) ||
|多媒体功能|标题 (开始、结束、文本、样式) ||
||findAllMediaControls (normalizedId) ||
||getActivePlayer (normalizedId) ||
||captionsOnOff (id) ||
||toSeconds (t) ||
||getAllComments (节点) ||
||styleRectify (styleName， styleValue) ||
||showCC (id) ||
||副标题 (id) ||

**HTM 文件**

品牌包包含一组 HTM 文件，这些文件支持将关键信息传达到帮助内容用户的方案，例如，包含一个部分的主页，其中描述了安装了哪些内容集，以及在本地主题集找不到主题时告知用户的页面。 可以按产品修改这些 HTM 文件。  ISO Shell 供应商能够接受默认品牌包，并更改这些页面的行为和内容，以满足其需求。  这些文件引用各自的品牌包，以便品牌标记从branding.xml内容。

|**File**|**使用**|**显示的内容源**|
|-|-|-|
|homepage.htm|这是一个页面，显示当前安装的内容，以及适合向用户显示其内容的其他任何消息。  此文件具有附加的元数据属性"Microsoft.Help.Id"content="-1"，该属性将此内容放在本地内容 TOC 的顶部。||
||<META_HOME_PAGE_TITLE_ADD />|Branding.xml、标记 \<HomePageTitle>|
||<HOME_PAGE_INTRODUCTION_SECTION_ADD />|Branding.xml、标记 \<HomePageIntroduction>|
||<HOME_PAGE_CONTENT_INSTALL_SECTION_ADD />|Branding.xml、标记 \<HomePageContentInstallText>|
||<HOME_PAGE_BOOKS_INSTALLED_SECTION_ADD />|标题部分Branding.xml标记 ，即未安装任何书籍 \<HomePageInstalledBooks>  \<HomePageNoBooksInstalled> 时从应用程序生成的数据。|
||<HOME_PAGE_SETTINGS_SECTION_ADD />|标题部分Branding.xml \<HomePageHelpSettings> 标记 ，节文本 \<HomePageHelpSettingsText> 。|
|topiccorrupted.htm|当主题存在于本地集，但由于某种原因无法显示 (损坏的内容) 。||
||<META_TOPIC_CORRUPTED_TITLE_ADD />|Branding.xml、标记 \<TopicCorruptedTitle>|
||<TOPIC_CORRUPTED_SECTION_ADD />|Branding.xml、标记 \<TopicCorruptedViewOnlineText>|
|topicnotfound.htm|在本地内容集找不到主题或联机可用时||
||<META_TOPIC_NOT_FOUND_TITLE_ADD />|Branding.xml、标记 \<TopicNotFoundTitle>|
||<META_TOPIC_NOT_FOUND_ID_ADD />|Branding.xml，标记 \<TopicNotFoundViewOnlineText> + \<TopicNotFoundDownloadContentText>|
||<TOPIC_NOT_FOUND_SECTION_ADD />|Branding.xml、标记 \<TopicNotFoundText>|
|contentnotinstalled.htm|未为产品安装本地内容时。||
||<META_CONTENT_NOT_INSTALLED_TITLE_ADD />|Branding.xml、标记 \<ContentNotInstalledTitle>|
||<META_CONTENT_NOT_INSTALLED_ID_ADD />|Branding.xml、标记 \<ContentNotInstalledDownloadContentText>|
||<CONTENT_NOT_INSTALLED_SECTION_ADD />|Branding.xml、标记 \<ContentNotInstalledText>|

**CSS 文件**

"Visual Studio帮助查看器品牌包"包含两个 css 文件，用于支持一致的Visual Studio帮助内容呈现：

- Branding.css - 包含用于呈现的 css 元素，其中 SelfBranded=false

- Printer.css - 包含用于呈现的 css 元素，其中 SelfBranded=false

Branding.css 文件包括 Visual Studio 主题演示的定义 (请注意，包服务的 Branding_ .mshc 中包含的 branding.css 可能会更改 \<locale>) 。

**图形文件**

Visual Studio 内容显示 Visual Studio 徽标以及其他图形。  下面显示了 Visual Studio 帮助查看器署名包中图形文件的完整列表。

|**File**|**使用**|**示例**|
|-|-|-|
|clear.gif|用于呈现可折叠区域||
|footer_slice.gif|页脚显示||
|info_icon.gif|显示信息时使用|免责声明|
|online_icon.gif|此图标将与联机链接关联||
|tabLeftBD.gif|用于呈现代码片段容器||
|tabRightBD.gif|用于呈现代码片段容器||
|vs_logo_bk.gif|用于 Branding.xml 标记中定义的正常对比度徽标 \<LogoFileName> 。  对于 Visual Studio 产品，徽标名称为 vs_logo_bk.gif。||
|vs_logo_wh.gif|用于 Branding.xml 标记中定义的高对比度徽标 \<LogoFileNameHC> 。  对于 Visual Studio 产品，徽标名称为 vs_logo_wh.gif。||
|ccOff.png|图形标题||
|ccOn.png|图形标题||
|ImageSprite.png|用于呈现可折叠区域|展开或折叠图形|

## <a name="deploy-a-set-of-topics"></a>部署一组主题

这是创建帮助查看器内容部署集的简单快捷教程，其中包含 .MSHA 文件以及包含主题的 cab 或 MSHCs 集。 .MSHA 是一个 XML 文件，用于描述一组 cab 文件或 .MSHC 文件。 Help Viewer 可以读取 .MSHA，以获取 .CAB 或 (的内容列表。.MSHC 文件) 可用于本地安装。

这只是描述帮助查看器 .MSHA 的基本 XML 架构的入门教程。  在此 brief 概述和示例 Helpcontentsetup.msha. .msha 中有一个示例实现。

本入门教程中，.MSHA 的名称是 Helpcontentsetup.msha。 .msha (文件的名称可以是任何扩展名为的文件。.MSHA) 。 下面) 的 Helpcontentsetup.msha (示例应包含 cab 或 MSHCs 列表。  文件类型必须在 .MSHA 中保持一致， (不支持) 的 .MSHA 和 CAB 文件类型组合。 对于每个 CAB 或 .mshc，应 \<div class="package"> \</div> (参阅下面) 的示例。

注意：下面的实现示例中包含了署名包。 若要获得所需的 Visual Studio 内容呈现元素和内容行为，这一点非常重要。

示例 Helpcontentsetup.msha. .msha 文件： (将 "内容集名称 1" 和 "内容集名称 2" 等替换为文件名。 ) 

```html
<html>
<head />
<body class="vendor-book">
<div class="details">
<span class="vendor">Your Company</span>
<span class="locale">en-us</span>
<span class="product">Your Company Help Content</span>
<span class="name">Your Company Help Content</span>
</div>
<div class="package-list">
<div class="package">
<span class="name">Your_Company _Content_Set_1</span>
<span class="deployed">True</span>
<a class="current-link" href="Your_Company _Content_Set_1.mshc">Your_Company _Content_Set_1.mshc </a>
</div>
<div class="package">
<span class="name">Your_Company _Content_Set_2</span>
<span class="deployed">True</span>
<a class="current-link"href=" Your_Company _Content_Set_2.mshc "> Your_Company _Content_Set_2.mshc </a>
</div>.
```

1. 创建本地文件夹，如 "C:\SampleContent"

2. 在此示例中，我们将使用 .MSHC 文件来包含主题。  .MSHC 是文件扩展名从 .zip 更改为的 zip。.MSHC.

3. 将下面的 Helpcontentsetup.msha 创建为文本文件 (记事本用于创建文件) 并将其保存到前面所述的文件夹 (参见步骤 1) 。

类 "署名" 存在并且是唯一的。 此入门教程包含品牌 .mshc，因此已安装的内容将具有品牌，MSHCs 中包含的内容行为将具有品牌包中包含的相应支持元素。 如果没有此选项，系统查找不属于已翻录 () 内容的支持项时，将产生错误。

若要获取 Visual Studio 品牌包，请 Branding_en 将 C:\Program 文件中的 .mshc 文件复制到 (x86) \microsoft Help Viewer\v2.3\ 复制到工作文件夹。

```html
<html>
<head />
<body class="vendor-book">
<div class="details">
<span class="vendor">Your Company</span>
<span class="locale">en-us</span>
<span class="product">Your Company Help Content</span>
<span class="name">Your Company Help Content</span>
</div>
<div class="package-list">
<div class="package">
<span class="name">Your_Company _Content_Set_1</span>
<span class="deployed">True</span>
<a class="current-link" href="Your_Company _Content_Set_1.mshc">Your_Company _Content_Set_1.mshc </a>
</div>
<div class="package">
<span class="name">Your_Company _Content_Set_2</span>
<span class="deployed">True</span>
<a class="current-link"href=" Your_Company _Content_Set_2.mshc "> Your_Company _Content_Set_2.mshc </a>
</div>
<div class="package">
<span class="packageType">branding</span>
<span class="name">Branding_en-US</span>
<span class="deployed">True</span>
<a class="current-link" href="Branding_en-US.mshc">Branding_en-US.mshc</a>
</div>
</div>
</body>
</html>
```

**摘要**

使用和扩展以上步骤将使 vsp 为 Visual Studio 帮助查看器部署其内容集。

### <a name="add-help-to-the-visual-studio-shell-integrated-and-isolated"></a>将帮助添加到 Visual Studio Shell (集成和隔离) 

**介绍**

本演练演示如何将帮助内容合并到 Visual Studio Shell 应用程序中，然后将其部署。

**惠?**

1. [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]

2. [Visual Studio 2013独立 Shell 再发行](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

概述

[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]Shell 是一个 [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 可以基于其应用程序的 IDE 版本。 此类应用程序包含独立 Shell 以及您创建的扩展。 使用 SDK 中包含的独立 Shell 项目模板 [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 来构建扩展。

创建基于 Shell 的独立应用程序及其帮助的基本步骤：

1. [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] (Microsoft 下载) 获取 ISO Shell 可再发行组件。

2. 在 Visual Studio 中，创建一个基于独立 Shell 的帮助扩展，例如本演练稍后部分中所述的 Contoso 帮助扩展。

3. 将扩展和 ISO Shell 可再发行组件包装到部署 MSI (应用程序安装) 。 本演练不包含安装步骤。

创建 Visual Studio 内容存储。 对于集成 Shell 方案，请将视觉对象 Studio12 更改为产品目录名称，如下所示：

- 创建文件夹 C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15。

- 创建一个名为 CatalogType.xml 的文件，并将其添加到该文件夹中。 该文件应包含以下代码行：

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <catalogType>UserManaged</catalogType>
    ```

在注册表中定义内容存储。 对于集成 Shell，请将 VisualStudio15 更改为产品目录名称：

- HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

   Key： LocationPath 字符串值： C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15\

- HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15\en-US

   Key： CatalogName 字符串值： [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 文档

**创建 Project**

若要创建独立的 Shell 扩展：

1. 在 Visual Studio 中的 "**文件**" 下，选择 "**新建" Project** 在 "**其他 Project 类型**" 下，选择 "**扩展性**"，然后选择 " **Visual Studio Shell 隔离**"。 将项目命名 `ContosoHelpShell` 为基于 Visual Studio 独立 Shell 模板创建扩展性项目) 。

2. 在解决方案资源管理器的 ContosoHelpShellUI 项目的 "资源文件" 文件夹中，打开 System.windows.input.applicationcommands.paste. .vsct。 请确保已将此行注释掉 (搜索 "No_Help" ) ： `<!-- <define name="No_HelpMenuCommands"/> -->`

3. 选择 F5 键编译并运行 **调试**。 在独立 Shell IDE 的实验实例中，选择 " **帮助** " 菜单。 请确保显示 " **查看帮助**"、" **添加和删除帮助内容**" 和 " **设置帮助首选项** "。

4. 在解决方案资源管理器的 ContosHelpShell 项目的 "Shell 自定义项" 文件夹中，打开 ContosoHelpShell. .pkgdef。 若要定义 Contoso 帮助目录，请添加以下行：

    ```
     [$RootKey$\Help]
    "Product"="Contoso"
    "Catalog"="Contoso"
    "Version"="100"
    "BrandingPackage"="ContosoBrandingPackage.mshc"
    ```

5. 在解决方案资源管理器的 ContosHelpShell 项目的 "Shell 自定义项" 文件夹中，打开 ContosoHelpShell. .pkgdef。 若要启用 F1 帮助，请添加以下行：

    ```
    // F1 Help Provider

    [$RootKey$\HelpProviders\{C99BDC23-FF29-46bf-9658-ADD634CCAED8}]
    "Name"="13407"
    "Package"="{DA9FB551-C724-11d0-AE1F-00A0C90FFFC3}"
    @="Help3 Provider"
    [$RootKey$\HelpProviders]
    @="{C99BDC23-FF29-46bf-9658-ADD634CCAED8}"
    [$RootKey$\Services\{C99BDC23-FF29-46bf-9658-ADD634CCAED8}]
    "Name"="Help3 Provider"
    @="{4A791146-19E4-11D3-B86B-00C04F79F802}"
    ```

6. 在解决方案资源管理器的 ContosoHelpShell 解决方案的上下文菜单上，选择 " **属性** " 菜单项。 在 " **配置属性**" 下，选择 **Configuration Manager**。 在 " **配置** " 列中，将每个 "调试" 值更改为 "Release"。

7. 生成解决方案。 这会在发布文件夹中创建一组文件，将在下一部分中使用。

若要对此进行测试，如下所示：

1. 在要将 Contoso 部署到的计算机上，安装) ISO Shell 以上下载的 (。

2. 在 \\ \Program 文件 (x86) 中创建文件夹 \\ ，并将其命名为 `Contoso` 。

3. 将 ContosoHelpShell 发布文件夹中的内容复制到 \Program Files (\\ x86) \Contoso\ 文件夹中。

4. 通过选择"开始"菜单中的  **"运行** "并输入 **来** 启动注册表编辑器 `Regedit` 。 在注册表编辑器中，选择"**文件"，** 然后选择"**导入"。** 浏览到 ContosoHelpShell 项目文件夹。 在 ContosoHelpShell 子文件夹内，选择"ContosoHelpShell.reg"。

5. 创建内容存储：

    对于 ISO Shell - 创建 Contoso 内容存储 C：\ProgramData\Microsoft\HelpLibrary2\Catalogs\ContosoDev12

    对于 [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 集成 Shell，创建文件夹 C：\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15

6. 创建CatalogType.xml并添加到内容存储 (步骤) 包含：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <catalogType>UserManaged</catalogType>
   ```

7. 添加以下注册表项：

    HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15Key： LocationPath String 值：

    对于 ISO Shell：

    C：ProgramDataMicrosoftHelpLibrary2CatalogsVisualStudio15

    [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 集成 Shell：

    C：ProgramDataMicrosoftHelpLibrary2CatalogsVisualStudio15en-US

    键：CatalogName 字符串值： [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 文档。 对于 ISO Shell，这是目录的名称。

8. 将内容 (CAB 或 MSHC 和 MSHA) 复制到本地文件夹。

9. 用于测试内容存储的集成 Shell 命令行示例。 对于 ISO Shell，请根据情况更改目录并启动"应用"值，以匹配产品。

     "C：\Program Files (x86) \Microsoft Help Viewer\v2.3\HlpViewer.exe" /catalogName VisualStudio15 /helpQuery method="page&id=ContosoTopic0" /launchingApp Microsoft，VisualStudio，12.0

10. 从 Contoso 应用根 (启动 Contoso 应用程序) 。 在 ISO Shell 中，选择" **帮助** "菜单项，然后更改"设置帮助 **首选项** " **以使用本地帮助**。

11. 在 shell 中，选择"**帮助"** 菜单项，然后选择"**查看帮助"。** 应启动本地帮助查看器。 选择" **管理内容"** 选项卡。在 **"安装源"** 下，选择 **"磁盘** "选项按钮。 选择 **"..."** 按钮并浏览到包含 Contoso 内容的本地 (复制到上述步骤中的本地) 。 选择 HelpContentSetup.msha。 Contoso 现在应作为书籍显示在书籍选择中。 选择 **"添加**"，然后选择右下角 ("更新") 。

12. 在 Contoso IDE 中，选择 F1 键以测试 F1 功能。

## <a name="additional-resources"></a>其他资源

有关运行时 API，请参阅 Windows [API](/previous-versions/windows/desktop/helpapi/helpapi-portal)。

若要详细了解如何利用帮助 API，请参阅 [Help Viewer 代码示例](https://marketplace.visualstudio.com/items?itemName=RobChandlerHelpMVP.HelpViewer20CodeExamples)。

可以在开发人员服务中提交功能[Community。](https://aka.ms/feedback/suggest?space=8)
