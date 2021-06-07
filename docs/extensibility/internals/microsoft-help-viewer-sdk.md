---
title: Microsoft Help Viewer SDK |Microsoft Docs
description: 了解 Visual Studio 帮助查看器任务，例如创建项目、创建帮助查看器内容品牌包以及部署一组文章。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 620d7dcd-d462-475e-a449-fbfa06ff12c5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8bc2ed473e25dc75d0155bc864aa02c157e3482f
ms.sourcegitcommit: f430d014f912aa7874e1db65026dc72688b973e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2021
ms.locfileid: "111448319"
---
# <a name="microsoft-help-viewer-sdk"></a>Microsoft Help Viewer SDK

本文包含 Visual Studio 帮助查看器集成器的以下任务：

-  (F1 支持创建主题) 

- 创建帮助查看器内容品牌包

- 部署一组文章

- 将帮助添加到 Visual Studio shell (集成或隔离) 

- 其他资源

## <a name="create-a-topic-f1-support"></a> (F1 支持创建主题) 

本部分概述了介绍的主题的组件、主题要求、有关如何创建主题的简短说明 (包括 F1 支持要求) 最后是一个示例主题及其呈现的结果。

**Help Viewer 主题概述**

当调用主题进行呈现时，帮助查看器将获取安装或上次更新时与主题相关联的品牌包元素以及主题 XHTML，并组合两者以生成显示的内容视图 (品牌数据 + 主题数据) 。  品牌包包含徽标、对内容行为的支持和品牌文本 (版权等 ) 。  有关署名包元素的详细信息，请参阅下面的 "创建署名包"。  如果没有与主题相关联的品牌包，帮助查看器将使用位于帮助查看器应用程序根中的 "回退署名包" (Branding_en-.mshc) 。

**Help Viewer 主题要求**

若要在帮助查看器中正确呈现，原始主题内容必须是 W3C Basic 1.1 XHTML。

主题通常包含两个部分：

- 元数据 (参阅 Content Metadata Reference) ：有关该主题的数据，例如，主题唯一 ID、关键字值、主题 TOC ID、父节点 ID 等。

- 正文内容：符合 W3C Basic 1.1 XHTML，其中包括受支持的内容行为 (可折叠区域、代码片段等。下面) 显示完整列表。

Visual Studio 署名包支持的控件：

- 链接

- CodeSnippet

- CollapsibleArea

- 继承成员

- LanguageSpecificText

支持的语言字符串 (不区分大小写) ：

- javascript

- csharp 或 c#

- cplusplus 或 visualc + + 或 c + +

- jscript

- "

- f # 或 fsharp.core 或 fs

- 其他-表示语言名称的字符串

**创建帮助查看器主题**

创建一个名为 ContosoTopic4.htm 的新 XHTML 文档，并在) 以下 (包含标题标记。

```html
<html>
<head>
<title>Contoso Topic 4</title>
</head>

<body>

</body>
</html>

```

接下来，添加数据以定义主题如何表现 (自品牌或不) 、如何为 F1 引用本主题、在目录中存在此主题，该主题的 ID (其他) 主题的链接引用等。有关支持的元数据的完整列表，请参阅下面的 "内容元数据" 表。

- 在这种情况下，我们将使用自己的品牌包，这是 Visual Studio 帮助查看器署名包的一个变体。

- 将 F1 meta name 和 value ( "ContosoTopic4" content = "" ) ，它将与 IDE 属性包中提供的 F1 值匹配。  (参见 F1 支持部分了解详细信息。 ) 此值与 IDE 内的 F1 调用匹配，以在 IDE 中选择 F1 时显示此主题。

- 添加主题 ID。 这是其他主题用来链接到本主题的字符串。 它是本主题的帮助查看器 ID。

- 对于 TOC，请添加该主题的父节点以定义将显示此主题 TOC 节点的位置。

- 对于 TOC，请添加该主题的节点顺序。 当父节点具有子节点 `n` 数时，按子节点的位置定义。 例如，本主题是4个子主题的第4步。

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

主体 (不包含主题的页眉和页脚) 将包含页面链接、附注部分、可折叠区域、代码片段和特定于语言的文本部分。  请参阅品牌部分，了解有关提供的主题的这些区域的信息。

1. 添加主题标题标记：  `<div class="title">Contoso Topic 4</div>`

2. 添加便笺部分： `<div class="alert"> add your table tag and text </div>`

3. 添加可折叠区域：  `<CollapsibleArea Expanded="1" Title="Collapsible Area Test Heading"> add text  </CollapsibleArea>`

4. 添加代码片段：  `<CodeSnippet EnableCopyCode="true" Language="CSharp" ContainsMarkup="false" DisplayLanguage="C#" > a block of code </CodeSnippet>`

5. 添加特定于代码语言的文本：  `<LanguageSpecificText devLangcs="CS" devLangvb="VB" devLangcpp="C++" devLangnu="F#" />` 请注意， `devLangnu=` 允许您输入其他语言。 例如， `devLangnu="Fortran"` 当代码片段 DisplayLanguage = fortran 时显示 fortran

6. 添加页面链接： `<a href="ms-xhelp:///?Id=ContosoTopic1">Main Topic</a>`

> [!NOTE]
> 注意：对于不支持的新 "显示语言" (示例、F #、Cobol、Fortran) 代码段中的代码着色将为单色。

**示例帮助查看器主题** 此代码演示如何定义元数据、代码段、可折叠区域和特定于语言的文本。

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

在 Visual Studio 中，选择 F1 将生成从 IDE 中的光标位置提供的值，并使用提供的值 (基于游标位置来填充 "属性包"。 当游标超出功能 x 时，功能 x 是活动/焦点，并用值填充属性包。  选择 F1 后，将填充属性包，并且 Visual Studio F1 代码会查看客户默认帮助源是本地的还是联机的 (默认) 为 "联机"。然后，基于 "用户" 设置 (默认的) shell 执行创建适当的字符串 (请参阅 exe 启动参数的帮助管理员指南。如果本地帮助是默认值，则为属性包中的 "本地帮助查看器 + 关键字 (s 的参数"; 如果 ") 参数" 列表中包含关键字的 MSDN URL，则为。

如果为 F1 返回了三个字符串，称为多值字符串，请使用第一项，查找命中，如果找到，则完成;否则，转到下一个字符串。  订单问题。 多值关键字的表示形式应最长为字符串。  若要在多值关键字的情况下验证这一点，请查看联机 F1 URL 字符串，其中包含所选关键字。

在 Visual Studio 2012 中，我们特意在联机和脱机之间建立了更强的分隔，因此，如果用户的设置为联机，则只需将 F1 请求直接传递到 MSDN 上的联机查询服务，而不是通过 Visual Studio 2010 中的帮助库代理进行路由。 然后，我们依赖于 "安装的供应商内容 = true" 的状态来确定是否在该上下文中执行其他操作。 如果为 true，则根据你希望为客户提供的支持来执行此分析和路由逻辑。 如果为 false，则只需跳到 MSDN。 如果用户的设置为 "本地"，则所有调用都将转向本地帮助引擎。

F1 流程图：

![F1 流](../../extensibility/internals/media/f1flow.png "F1flow")

如果帮助查看器默认帮助内容源设置为 online (在浏览器中启动) ：

- Visual Studio 合作伙伴 (VSP) 功能向 F1 属性包发送值 (属性包前缀。在注册表) 中找到的前缀的关键字和联机 URL： F1 将 VSP URL + 参数发送到浏览器。

- Visual Studio 功能 (语言编辑器、Visual Studio 特定菜单项等 ) ： F1 将 Visual Studio URL 发送到浏览器。

如果帮助查看器默认帮助内容源设置为本地帮助 (在帮助查看器中启动) ：

- 在 F1 属性包和本地存储索引之间具有关键字匹配的 VSP 功能 (即，属性包前缀。关键字 = 在本地存储索引中找到的值) ： F1 会在帮助查看器中呈现该主题。

- Visual Studio 功能 (不为 VSP 重写从 Visual Studio 功能发出的属性包) ： F1 会在帮助查看器中呈现 Visual Studio 主题。

设置以下注册表值以启用供应商帮助内容的 F1 回退。 F1 回退意味着帮助查看器设置为联机查找 F1 帮助内容，并将供应商内容本地安装到用户的硬盘驱动器上。 即使默认设置为 "联机帮助"，帮助查看器也应查看内容的本地帮助。

1. 在 Help 2.3 注册表项下设置 **VendorContent** 值：

   - 对于32位操作系统：

        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.3\Catalogs\VisualStudio15

        "VendorContent" = dword：00000001

   - 对于64位操作系统：

        HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

        "VendorContent" = dword：00000001

2. 在 Help 2.3 注册表项下注册合作伙伴命名空间：

   - 对于32位操作系统：

      HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.3\Partner<em> \\<命名 \> 空间</em>

      "位置" = "脱机"

   - 对于64位操作系统：

      HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Partner<em> \\<命名 \> 空间</em>

      "位置" = "脱机"

**基本本机命名空间分析**

若要启用基本本机命名空间分析，在注册表中，添加一个新的 DWORD，其名称为：BaseNativeNamespaces，并在其要支持的目录 (下将其值设置为 1) 。  例如，如果要使用Visual Studio目录，可以将密钥添加到路径：

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

当遇到格式为 HEADER/METHOD 的 F1 关键字时，将分析"/"字符，从而生成以下构造：

- HEADER：是可用于在注册表中注册的命名空间

- 方法：这将成为传递的关键字。

例如，给定名为 CustomLibrary 的自定义库和名为 MyTestMethod 的方法，当 F1 请求进入时，它将格式化为 `CustomLibrary/MyTestMethod` 。

然后，用户可以将 CustomLibrary 注册为 Partners 配置单元下的命名空间，并提供所需的任何位置键，传递给查询的关键字将是 MyTestMethod。

**在 IDE 中启用帮助调试工具**

添加以下注册表项和值：

::: moniker range="vs-2017"

**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\15.0\Dynamic Help**

::: moniker-end

::: moniker range=">=vs-2019"

**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\16.0\Dynamic Help**

::: moniker-end

值：在零售数据中显示调试输出：是

在 IDE 中的"帮助"菜单项下，选择"**调试帮助上下文"。**

**内容元数据**

在下表中，括号之间出现的任何字符串都是占位符，必须替换为识别的值。 例如，在 \<meta name="Microsoft.Help.Locale" content="[language code]" /> 中，"[语言代码]"必须替换为"en-us"等值。

| 属性 (HTML 表示)  | 说明 |
| - | - |
| \< meta name="Microsoft.Help.Locale" content="[language-code]" /> | 设置本主题区域设置。 如果在主题中使用了此标记，则它必须只使用一次，并且必须插入到任何其他 Microsoft 帮助标记的上方。 如果未使用此标记，则通过使用与产品区域设置关联的断字符（如果已指定）为主题的正文文本编制索引;否则，使用 en-us 断字符。 此标记符合 ISOC RFC 4646。 若要确保 Microsoft 帮助正常工作，请使用此属性而不是常规语言属性。 |
| \< meta name="Microsoft.Help.TopicLocale" content="[language-code]" /> | 当还使用其他区域设置时，设置本主题区域设置。 如果在主题中使用了此标记，则必须只使用一次。 当目录包含多个语言的内容时，请使用此标记。 目录中的多个主题可以具有相同的 ID，但每个主题必须指定唯一的 TopicLocale。 指定与目录区域设置匹配的 TopicLocale 的主题是目录中显示的主题。 但是，主题的所有语言版本都显示在搜索结果中。 |
| \< title>[标题]\</title> | 指定本主题的标题。 此标记是必需的，并且必须在主题中仅使用一次。 如果主题的正文不包含标题部分，则此标题将显示在主题和 \<div> 目录中。 |
| \< meta name=" Microsoft.Help.Keywords" content="[aKeywordPhrase]"/> | 指定在帮助查看器的索引窗格中显示的链接的文本。 单击链接时，将显示主题。 您可以为主题指定多个索引关键字，或者，如果不希望在索引中显示指向本主题的链接，可以省略此标记。 可以将早期版本的帮助中的"K"关键字转换为此属性。 |
| \< meta name="Microsoft.Help.Id" content="[TopicID]"/> | 设置本主题的标识符。 此标记是必需的，并且必须在主题中仅使用一次。 ID 在目录中具有相同区域设置的主题之间必须唯一。 在另一个主题中，可以使用此 ID 创建指向本主题的链接。 |
| \< meta name="Microsoft.Help.F1" content="[System.Windows.Controls.Primitives.IRecyclingItemContainerGenerator]"/> | 指定本主题的 F1 关键字。 你可以为主题指定多个 F1 关键字，或者，如果不希望在应用程序用户按 F1 时显示本主题，可以省略此标记。 通常，只为主题指定一个 F1 关键字。 可以将早期版本的帮助中的"F"关键字转换为此属性。 |
| \< meta name="Description" content="[topic description]" /> | 提供本主题中内容的简短摘要。 如果在主题中使用了此标记，则必须只使用一次。 此属性由查询库直接访问;不存储在索引文件中。 |
| meta name="Microsoft.Help.TocParent" content="[parent_Id]"/> | 在目录中指定本主题的父主题。 此标记是必需的，并且必须在主题中仅使用一次。 值是 Microsoft.Help.Id 的默认值。 主题在目录只能有一个位置。 "-1"被视为 TOC 根的主题 ID。 在 [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 中，该页是帮助查看器主页。 正因如此，我们专门将 TocParent=-1 添加到某些主题，以确保它们在顶级显示。 帮助查看器主页是一个系统页面，因此不可替换。 如果 VSP 尝试添加 ID 为 -1 的页面，可能会将其添加到内容集，但帮助查看器将始终使用系统页 - 帮助查看器主页 |
| \< meta name="Microsoft.Help.TocOrder" content="[positive integer]"/> | 指定本主题相对于其对等主题在目录中的显示位置。 此标记是必需的，并且必须在主题中仅使用一次。 该值是一个整数。 指定较低值整数的主题显示在指定高值整数的主题上方。 |
| \< meta name="Microsoft.Help.Product" content="[product code]"/> | 指定本主题描述的产品。 如果在主题中使用了此标记，则必须只使用一次。 此信息还可以作为传递给帮助索引器的参数提供。 |
| \< meta name="Microsoft.Help.ProductVersion" content="[version number]"/> | 指定本主题描述的产品版本。 如果在主题中使用了此标记，则必须只使用一次。 此信息还可以作为传递给帮助索引器的参数提供。 |
| \< meta name="Microsoft.Help.Category" content="[string]"/> | 由产品用于标识内容的子部分。 可以标识主题的多个子节，或者如果不希望链接标识任何子节，可以省略此标记。 当主题从早期版本的帮助转换时，此标记用于存储 TargetOS 和 TargetFrameworkMoniker 的属性。 内容的格式为 AttributeName：AttributeValue。 |
| \< meta name="Microsoft.Help.TopicVersion content="[topic version number]"/> | 当目录中存在多个版本时，指定本主题的此版本。 由于 Microsoft.Help.Id 不一定是唯一的，因此当目录中存在多个主题版本时（例如，当目录包含 .NET Framework 3.5 的主题和 .NET Framework 4 的主题并且两者具有相同的 Microsoft.Help.Id 时，需要此标记。 |
| \< meta name="SelfBranded" content="[TRUE or FALSE]"/> | 指定本主题是使用 Help Library Manager 启动品牌包还是特定于该主题的品牌包。 此标记必须为 TRUE 或 FALSE。 如果为 TRUE，则关联主题的品牌包将替代在帮助库管理器启动时设置的品牌包，以便即使主题不同于其他内容的呈现，该主题也呈现为预期。 如果为 FALSE，则根据帮助库管理器启动时设置的品牌包呈现当前主题。 默认情况下，帮助库管理器假定自品牌为 false，除非 SelfBranded 变量声明为 TRUE;因此，不需要声明 \<meta name="SelfBranded" content="FALSE"/> 。 |

## <a name="create-a-branding-package"></a>创建品牌包

Visual Studio版本包含许多不同的 Visual Studio 产品，包括适用于合作伙伴的隔离和Visual Studio shell。  每种产品都需要一定程度的基于主题的帮助内容品牌支持，这是产品独有的。  例如，Visual Studio主题需要具有一致的品牌表示形式，而包装 ISO Shell 的 SQL Studio 需要每个主题具有自己独特的帮助内容品牌。  集成 Shell 合作伙伴可能希望其帮助主题位于产品帮助Visual Studio父主题中，同时保持自己的主题品牌。

品牌包由包含帮助查看器的产品安装。  对于Visual Studio产品：

- Help Viewer 2. (3 应用根根中安装了回退品牌包 (Branding_ \<locale> .mshc) ，例如：Help Viewer 语言包的 C：\Program Files (x86) \Microsoft Help Viewer\v2.3) 。  这用于以下情况：未安装产品品牌包 (未安装任何内容) 或已安装的品牌包已损坏。  使用Visual Studio根 (包时，) 忽略徽标和反馈元素。

- 从Visual Studio服务安装内容时，还会在 (安装方案中安装品牌) 。  如果品牌包有更新，则当发生下一个内容更新或其他包安装操作时，将安装更新。

该Microsoft Help Viewer支持基于主题元数据的主题品牌。

- 其中，主题元数据定义自品牌 = true，并像现在一样呈现主题， (品牌打造方面) 。

- 其中，主题元数据定义自品牌 = false，请使用与 TopicVendor 元数据值关联的品牌包。

- 其中，主题元数据定义 name="Microsoft.Help.TopicVendor" content= ，使用内容值中定义的品牌 \< branding package name in vendor MSHA> 包。

- 在Visual Studio目录中，有一个"品牌包"的优先级应用程序。  首先Visual Studio应用默认品牌，然后，如果在主题元数据中定义，并且与安装 msha) 中定义的关联品牌包 (一起受支持，则供应商定义的品牌将应用为替代。

品牌元素通常分为三个主要类别：

- 标头元素 (示例包括反馈链接、条件免责声明文本、徽标) 

- 示例内容 (包括展开/折叠控件文本元素和代码片段元素) 

- 页脚元素 (示例版权所有) 

被视为品牌元素的项目包括 (规范中详述) ：

- 目录/产品徽标 (示例，Visual Studio) 

- 反馈链接和电子邮件元素

- 免责声明文本

- 版权文本

帮助查看器品牌包Visual Studio支持文件包括：

- 图形 (徽标、图标等) 

- Branding.js - 支持内容行为的脚本文件

- Branding.xml - 跨目录内容一致使用的字符串。  注意：对于Visual Studio中的本地化文本branding.xml，请包含 _locID=" \<unique value> "

- Branding.css - 表示一致性样式定义

- Printing.css - 用于一致打印演示文稿的样式定义

如上所述，品牌包与主题相关联：

- 在元数据中定义 SelfBranded = false 时，主题将继承目录品牌包

- 或者，如果 SelfBranded = false，并且 MSHA 中定义了唯一的品牌包，并且安装内容时可用

对于实现自定义品牌包 (VSP 内容 SelfBranded=True) 的 VSP，一种继续操作的方法就是从随 Help Viewer) 一起安装的回退品牌包 (开始，并视情况更改文件的名称。  .mshc Branding_文件是 zip 文件，文件扩展名已更改为 .mshc，因此只需将扩展名从 .mshc 更改为 .zip 并提取 \<locale> 内容。  请参阅下文了解品牌包元素，并根据需要进行修改 (例如，将徽标更改为 VSP 徽标，以及引用 Branding.xml 文件中徽标、根据 VSP 特定内容更新 Branding.xml，等等) 。

完成所有修改后，创建包含所需品牌元素的 zip 文件，将扩展名更改为 .mshc。

若要关联自定义品牌包，请创建 MSHA，其中包含对品牌 mshc 文件的引用以及包含 (主题的 mshc) 。  请参阅下面的"MSHA"，了解如何创建基本 MSHA。

该Branding.xml文件包含一系列元素，这些元素用于在主题包含 时一致地呈现主题中的特定项 \<meta name="Microsoft.Help.SelfBranded" content="false"/> 。  下面Visual Studio列表中Branding.xml元素的列表。  此列表旨在用作 ISO Shell 采用者模板，他们在此模板中修改这些元素 (例如徽标、反馈和版权) 以满足自己的产品品牌需求。

注意："{n}"记下的变量具有代码依赖项 - 删除或更改这些值将导致错误，并可能导致应用程序崩溃。 本地化标识符 (示例 _locID="codesnippet.n") 包含在 Visual Studio 品牌包中。

**Branding.xml**

| 元素 | 说明 |
| - | - |
| 功能： | **可折叠区域** |
| 使用： | 展开折叠内容控件文本 |
| **元素** | **值** |
| ExpandText | 展开 |
| CollapseText | 折叠 |
| 功能： | **CodeSnippet** |
| 使用： | 代码片段控件文本。  注意：具有"非中断"空间的代码片段内容将更改为空格。 |
| **元素** | **值** |
| CopyToClipboard | 复制到剪贴板 |
| ViewColorizedText | 视图着色 |
| CombinedVBTabDisplayLanguage | Visual Basic (示例)  |
| VBDeclaration | 声明 |
| VBUsage | 使用情况 |
| 功能： | **反馈、页脚和徽标** |
| 使用： | 提供反馈控件，以便客户通过电子邮件提供有关当前主题的反馈。  内容的版权文本。  徽标定义。 |
| **元素** | **值 (可以修改这些字符串以满足内容采用者需求。)** |
| 版权 | © 2013 微软公司。 保留所有权利。 |
| SendFeedback | \<a href="{0}" {1}>向 \</a> Microsoft 发送有关本主题的反馈。 |
| FeedbackLink | |
| LogoTitle | [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] |
| LogoFileName | vs_logo_bk.gif |
| LogoFileNameHC | vs_logo_wh.gif |
| 功能： | **免责声明** |
| 使用： | 计算机翻译内容的一组特定于大小写的免责声明。 |
| **元素** | **值** |
| MT_Editable | 本文是机器翻译的。 如果已建立 Internet 连接，请选择"联机查看本主题"，以可编辑模式同时查看包含原始英语内容的此页面。 |
| MT_NonEditable | 本文是机器翻译的。 如果已建立 Internet 连接，请选择"联机查看本主题"，以可编辑模式同时查看包含原始英语内容的此页面。 |
| MT_QualityEditable | 本文已手动翻译。 如果已建立 Internet 连接，请选择"联机查看本主题"，以可编辑模式同时查看包含原始英语内容的此页面。 |
| MT_QualityNonEditable | 本文已手动翻译。 如果已建立 Internet 连接，请选择"联机查看本主题"，以可编辑模式同时查看包含原始英语内容的此页面。 |
| MT_BetaContents | 本文是计算机翻译的，供初步发布使用。 如果已建立 Internet 连接，请选择"联机查看本主题"，以可编辑模式同时查看包含原始英语内容的此页面。 |
| MT_BetaRecycledContents | 本文已手动翻译，供初步发布使用。 如果你有 Internet 连接，请选择 "联机查看本主题" 以在可编辑模式下查看此页面，同时提供原始英语内容。 |
| 功能： | **LinkTable** |
| 使用： | 支持联机主题链接 |
| **元素** | **值** |
| LinkTableTitle | 链接表 |
| TopicEnuLinkText | 查看 \</a> 计算机上提供的本主题的英文版。 |
| TopicOnlineLinkText | 联机查看本主题 \<a href="{0}" {1}>\</a> |
| OnlineText | 联机 |
| 功能： | **视频音频控件** |
| 使用： | 显示视频内容的元素和文本 |
| **元素** | **值** |
| MultiMediaNotSupported | 必须安装 Internet Explorer 9 或更高版本才能支持 {0} 内容。 |
| VideoText | 显示视频 |
| AudioText | 流式传输音频 |
| OnlineVideoLinkText | \<p>若要查看与本主题相关的视频，请单击 {0} \<a href="{1}"> {2} 此处 \</a> 。\</p> |
| OnlineAudioLinkText | \<p>若要收听与本主题相关的音频，请单击 {0} \<a href="{1}"> {2} 此处 \</a> 。\</p> |
| 功能： | **内容未安装控件** |
| 使用： | 文本元素 (字符串) 用于呈现 contentnotinstalled.htm |
| **元素** | **值** |
| ContentNotInstalledTitle | 在您的计算机上找不到任何内容。 |
| ContentNotInstalledDownloadContentText | \<p>若要将内容下载到您的计算机，请 \<a href="{0}" {1}> 单击 "管理" 选项卡 \</a> 。\</p> |
| ContentNotInstalledText | \<p>计算机上未安装任何内容。 请参阅管理员以获取本地帮助内容安装。\</p> |
| 功能： | **找不到主题控件** |
| 使用： | 文本元素 (字符串) 用于呈现 topicnotfound.htm |
| **元素** | **值** |
| TopicNotFoundTitle | 在您的计算机上找不到请求的主题。 |
| TopicNotFoundViewOnlineText | \<p>您在计算机上找不到您请求的主题，但您可以 \<a href="{0}" {1}> 联机查看该主题 \</a> 。\</p> |
| TopicNotFoundDownloadContentText | \<p>请参阅导航窗格以获取指向类似主题的链接，或 \<a href="{0}" {1}> 单击 "管理" 选项卡 \</a> 将内容下载到您的计算机。\</p> |
| TopicNotFoundText | \<p>在您的计算机上找不到您请求的主题。\</p> |
| 功能： | **主题损坏控件** |
| 使用： | 文本元素 (字符串) 用于呈现 topiccorrupted.htm |
| **元素** | **值** |
| TopicCorruptedTitle | 无法显示请求的主题。 |
| TopicCorruptedViewOnlineText | \<p>Help Viewer 无法显示请求的主题。 主题的内容或基础系统依赖项中可能存在错误。\</p> |
| 功能： | **主页控件** |
| 使用： | 支持显示帮助查看器顶层节点内容的文本。 |
| **元素** | **值** |
| HomePageTitle | Help Viewer 主页 |
| HomePageIntroduction | \<p>欢迎使用 Microsoft Help Viewer，这是使用 Microsoft 工具、产品、技术和服务的所有用户的重要信息来源。 帮助查看器可让你访问操作方法和参考信息、示例代码、技术文章等。 若要查找所需的内容，请浏览目录、使用全文搜索或使用关键字索引在内容中导航。\</p> |
| HomePageContentInstallText | \<p>\<br />使用 " \<a href="{0}" {1}> 管理内容" \</a> 选项卡执行以下操作： \<ul> \<li> 向计算机添加内容。 \</li> \<li>检查本地内容的更新。 \</li> \<li>从计算机中删除内容。\</li>\</ul>\</p> |
| HomePageInstalledBooks | 已安装书籍 |
| HomePageNoBooksInstalled | 在您的计算机上找不到任何内容。 |
| HomePageHelpSettings | 帮助内容设置 |
| HomePageHelpSettingsText | \<p>你的当前设置是本地帮助。 "帮助查看器" 显示您在计算机上安装的内容。 \<br />若要更改帮助内容的源，请在 Visual Studio 菜单栏上选择 " \<span style="{0}"> 帮助"，然后选择 "帮助首选项" \</span> 。\<br />\</p> |
| 几 | MB |

**branding.js**

branding.js 文件包含 Visual Studio 帮助查看器品牌元素使用的 JavaScript。  下面是品牌元素和支持 JavaScript 函数的列表。  要为此文件本地化的所有字符串都在此文件顶部的 "可本地化字符串" 部分中定义。  已为 branding.js 文件中的位置字符串创建了 ICL 文件。

|**品牌功能**|**JavaScript 函数**|**说明**|
|-|-|-|
|Var .。。||定义变量|
|获取用户代码语言|setUserPreferenceLang|将索引号映射到代码语言|
|设置并获取 cookie 值|System.windows.application.getcookie、System.windows.application.setcookie||
|继承成员|changeMembersLabel|展开/折叠继承的成员|
|当 SelfBranded = False 时|onLoad|阅读查询字符串，检查其是否是打印请求。  将所有 codesnippets 设置为 "关注用户首选" 选项卡。 如果是打印请求，则将 isPrinterFriendly 设置为 true。 检查高对比度模式。|
|代码片段|addSpecificTextLanguageTagSet||
||getIndexFromDevLang||
||ChangeTab||
||setCodesnippetLang||
||setCurrentLang||
||CopyToClipboard||
|CollapsibleArea|addToCollapsibleControlSet|将所有可折叠控件对象写入列表中。|
||CA_Click|根据可折叠区域的状态，定义要显示的图像和文本|
|徽标的对比度支持|isBlackBackground () |调用以确定背景是否为黑色。  仅在高对比度模式下才准确。|
||isHighContrast () |使用彩色范围检测高对比度模式|
||onHighContrast (黑色) |检测到高对比度时调用|
|.LST 功能|||
||addToLanSpecTextIdSet (id) ||
||updateLST (currentLang) ||
||getDevLangFromCodeSnippet (lang) ||
|多媒体功能|标题 (开始、结束、文本和样式) ||
||findAllMediaControls (normalizedId) ||
||getActivePlayer (normalizedId) ||
||captionsOnOff (id) ||
||toSeconds (t) ||
||getAllComments (节点) ||
||styleRectify (styleName，styleValue) ||
||showCC (id) ||
||副标题 (id) ||

**HTM 文件**

品牌包包含一组 HTM 文件，这些文件支持用于传达关键信息以帮助内容用户的方案，例如，主页包含描述安装了哪些内容集的部分，以及在本地主题集中找不到主题的页面。 每个产品都可以修改这些 HTM 文件。  ISO Shell 供应商能够采用默认的品牌包，并更改这些页面的行为和内容以满足他们的需要。  这些文件引用各自的品牌包，以便品牌标记获取 branding.xml 文件中的相应内容。

|**File**|**使用**|**显示的内容源**|
|-|-|-|
|homepage.htm|此页面显示当前已安装的内容，以及任何其他适用于用户内容的消息。  此文件具有附加的元数据属性 "Microsoft.Help.Id" content = "-1"，该属性将此内容置于本地内容目录的顶部。||
||<META_HOME_PAGE_TITLE_ADD/>|Branding.xml、标记 \<HomePageTitle>|
||<HOME_PAGE_INTRODUCTION_SECTION_ADD/>|Branding.xml、标记 \<HomePageIntroduction>|
||<HOME_PAGE_CONTENT_INSTALL_SECTION_ADD/>|Branding.xml、标记 \<HomePageContentInstallText>|
||<HOME_PAGE_BOOKS_INSTALLED_SECTION_ADD/>|\<HomePageInstalledBooks> \<HomePageNoBooksInstalled> 在未安装任何书籍时，标题部分 Branding.xml 标记，即从应用程序生成的数据。|
||<HOME_PAGE_SETTINGS_SECTION_ADD/>|标题节 Branding.xml 标记 \<HomePageHelpSettings> ，部分文本 \<HomePageHelpSettingsText> 。|
|topiccorrupted.htm|如果主题位于本地集中，但出于某种原因无法显示 (损坏的内容) 。||
||<META_TOPIC_CORRUPTED_TITLE_ADD/>|Branding.xml、标记 \<TopicCorruptedTitle>|
||<TOPIC_CORRUPTED_SECTION_ADD/>|Branding.xml、标记 \<TopicCorruptedViewOnlineText>|
|topicnotfound.htm|在本地内容集中找不到主题，也不能联机使用时||
||<META_TOPIC_NOT_FOUND_TITLE_ADD/>|Branding.xml、标记 \<TopicNotFoundTitle>|
||<META_TOPIC_NOT_FOUND_ID_ADD/>|Branding.xml、标记 \<TopicNotFoundViewOnlineText> + \<TopicNotFoundDownloadContentText>|
||<TOPIC_NOT_FOUND_SECTION_ADD/>|Branding.xml、标记 \<TopicNotFoundText>|
|contentnotinstalled.htm|如果没有为产品安装本地内容。||
||<META_CONTENT_NOT_INSTALLED_TITLE_ADD/>|Branding.xml、标记 \<ContentNotInstalledTitle>|
||<META_CONTENT_NOT_INSTALLED_ID_ADD/>|Branding.xml、标记 \<ContentNotInstalledDownloadContentText>|
||<CONTENT_NOT_INSTALLED_SECTION_ADD/>|Branding.xml、标记 \<ContentNotInstalledText>|

**CSS 文件**

Visual Studio 帮助查看器署名包包含两个 css 文件，以支持一致的 Visual Studio 帮助内容演示：

- 品牌 .css-包含用于呈现的 css 元素，其中 SelfBranded = false

- Printer css-包含用于呈现的 css 元素，其中 SelfBranded = false

署名 .css 文件包括 Visual Studio 的定义演示 (需要注意的是，包服务的 Branding_ 中包含的 \<locale> .mshc 可能会更改) 。

**图形文件**

Visual Studio内容将显示Visual Studio和其他图形。  下面显示了帮助查看器Visual Studio包中图形文件的完整列表。

|**File**|**使用**|**示例**|
|-|-|-|
|clear.gif|用于呈现可折叠区域||
|footer_slice.gif|页脚演示||
|info_icon.gif|显示信息时使用|免责声明|
|online_icon.gif|此图标与联机链接相关联||
|tabLeftBD.gif|用于呈现代码片段容器||
|tabRightBD.gif|用于呈现代码片段容器||
|vs_logo_bk.gif|用于标记 中定义的普通对比度徽标Branding.xml引用 \<LogoFileName> 。  对于Visual Studio，徽标名称vs_logo_bk.gif。||
|vs_logo_wh.gif|用于标记 中定义的高对比度徽标Branding.xml引用 \<LogoFileNameHC> 。  对于Visual Studio，徽标名称vs_logo_wh.gif。||
|ccOff.png|标题图形||
|ccOn.png|标题图形||
|ImageSprite.png|用于呈现可折叠区域|展开或折叠图形|

## <a name="deploy-a-set-of-topics"></a>部署一组主题

这是一个简单快捷的教程，介绍如何创建由 MSHA 文件和包含主题的 cab 或 MSHC 组成的帮助查看器内容部署集。 MSHA 是描述一组 cab 或 MSHC 文件的 XML 文件。 帮助查看器可以读取 MSHA，以获取或 (.CAB列表。MSHC 文件) 本地安装。

这仅仅是描述帮助查看器 MSHA 的非常基本 XML 架构的一个基础。  下面是此简要概述和 HelpContentSetup.msha 示例实现示例。

就本开始操作来说，MSHA 的名称是 HelpContentSetup.msha (文件的名称可以是任何扩展名 。MSHA) 。 下面的 HelpContentSetup.msha (示例) 应包含可用的 cab 或 MSHC 的列表。  文件类型在 MSHA 中必须一致 (不支持 MSHA 和 CAB 文件类型) 。 对于每个 CAB 或 MSHC，应存在 \<div class="package"> ... (\</div> 请参阅以下示例) 。

注意：在下面的实现示例中，我们包含了品牌包。 若要获取所需的内容呈现元素和内容Visual Studio，这一点至关重要。

示例 HelpContentSetup.msha 文件： (将"内容集名称 1"和"内容集名称 2"等替换为文件名。) 

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

1. 创建本地文件夹，例如"C：\SampleContent"

2. 对于此示例，我们将使用 MSHC 文件来包含主题。  MSHC 是一个 zip，其文件扩展名从 .zip 更改为 。MSHC。

3. 创建以下 HelpContentSetup.msha 作为文本文件 (记事本用于创建文件) 并将其保存到上面记下的文件夹 (请参阅步骤 1) 。

类"Branding"存在且是唯一的。 品牌 mshc 包含在此参考中，以便已安装的内容具有品牌，并且 MSHC 中包含的内容行为将具有品牌包中包含的相应支持元素。 如果不这样做，则当系统查找不是所安装内容中已 (的支持) 错误。

若要获取 Visual Studio 品牌包，将 C：\Program Files (x86) \Microsoft Help Viewer\v2.3\ 中的 Branding_en-US.mshc 文件复制到工作文件夹。

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

使用和扩展上述步骤将使 VSP 能够为帮助查看器部署Visual Studio集。

### <a name="add-help-to-the-visual-studio-shell-integrated-and-isolated"></a>将帮助添加到 Visual Studio Shell (集成和独立) 

**介绍**

本演练演示如何将帮助内容合并到 Visual Studio Shell 应用程序中，然后部署它。

**要求**

1. [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]

2. [Visual Studio 2013独立 Shell Redist](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

**概述**

[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]Shell 是可基于应用程序的 [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] IDE 版本。 此类应用程序包含独立 Shell 以及你创建的扩展。 使用 SDK 中包含的独立 Shell 项目模板 [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 生成扩展。

创建基于独立 Shell 的应用程序及其帮助的基本步骤：

1. 获取 [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] Microsoft 下载 (ISO Shell 可再发行) 。

2. 在 Visual Studio，创建基于独立 Shell 的帮助扩展，例如，本演练稍后所述的 Contoso 帮助扩展。

3. 将扩展和 ISO Shell 可再发行组件包装到部署 MSI (应用程序安装程序) 。 本演练不包含安装步骤。

创建Visual Studio存储。 对于集成 Shell 方案，将 Visual Studio12 更改为产品目录名称，如下所示：

- 创建文件夹 C：\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15。

- 创建名为 CatalogType.xml文件，并将其添加到 文件夹中。 该文件应包含以下代码行：

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <catalogType>UserManaged</catalogType>
    ```

定义注册表中的内容存储。 对于集成 Shell，将 VisualStudio15 更改为产品目录名称：

- HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

   键：LocationPath String 值：C：\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15\

- HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15\en-US

   键：CatalogName 字符串值： [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 文档

**创建项目**

若要创建独立 Shell 扩展，请：

1. 在Visual Studio"下，选择"新建项目"，在"其他项目类型"下选择"扩展性"，然后选择"Visual Studio **Shell 隔离"。**  将项目) ，以基于独立 Shell 模板Visual Studio `ContosoHelpShell` 扩展性项目。

2. 在解决方案资源管理器 ContosoHelpShellUI 项目的"资源文件"文件夹中，打开 ApplicationCommands.vsct。 请确保在搜索" ("No_Help注释掉) ： `<!-- <define name="No_HelpMenuCommands"/> -->`

3. 选择 F5 键以编译并 **运行调试**。 在独立 Shell IDE 的实验实例中，选择"帮助 **"** 菜单。 确保显示"**查看帮助"、"****添加和删除帮助内容**"和 **"设置帮助首选项"** 命令。

4. 在解决方案资源管理器"ContosHelpShell"项目中的"Shell 自定义"文件夹中，打开"ContosoHelpShell.pkgdef"。 若要定义 Contoso 帮助目录，请添加以下行：

    ```
     [$RootKey$\Help]
    "Product"="Contoso"
    "Catalog"="Contoso"
    "Version"="100"
    "BrandingPackage"="ContosoBrandingPackage.mshc"
    ```

5. 在解决方案资源管理器中，在 ContosHelpShell 项目中的"Shell 自定义"文件夹中，打开"ContosoHelpShell.Application.pkgdef"。 若要启用 F1 帮助，请添加以下行：

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

6. 在解决方案资源管理器，在 ContosoHelpShell 解决方案的上下文菜单上，选择"属性 **"** 菜单项。 在 **"配置属性"****下，配置服务器"**。 在" **配置"** 列中，将每个"调试"值更改为"Release"。

7. 生成解决方案。 这会在发布文件夹中创建一组文件，将在下一部分使用。

若要测试这一点，就像部署一样：

1. 在要部署 Contoso 的计算机上安装从上述 ISO Shell (下载) 版本。

2. 在 \\ \Program Files (x86) \\ 文件夹，并命名 `Contoso` 它。

3. 将 ContosoHelpShell release 文件夹中的内容复制到 \\ \Program 文件 (x86) \contoso\ 文件夹中。

4. 通过在 "**开始**" 菜单中选择 "**运行**" 并输入来启动注册表编辑器 `Regedit` 。 在注册表编辑器中，选择 " **文件**"，然后选择 " **导入**"。 浏览到 ContosoHelpShell 项目文件夹。 在 ContosoHelpShell 子文件夹中，选择 ContosoHelpShell。

5. 创建内容存储：

    对于 ISO Shell-创建 Contoso 内容存储 C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\ContosoDev12

    对于 [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 集成 Shell，请创建文件夹 C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15

6. 创建 CatalogType.xml 并添加到内容存储 (上一步骤) 包含：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <catalogType>UserManaged</catalogType>
   ```

7. 添加以下注册表项：

    HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15Key： LocationPath 字符串值：

    对于 ISO Shell：

    C:ProgramDataMicrosoftHelpLibrary2CatalogsVisualStudio15

    [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 集成外壳：

    C:ProgramDataMicrosoftHelpLibrary2CatalogsVisualStudio15en-US

    Key： CatalogName 字符串值： [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 文档。 对于 ISO Shell，这是你的目录的名称。

8. 将 (cab 或 .MSHC 和 .MSHA) 的内容复制到本地文件夹。

9. 用于测试内容存储的集成 Shell 命令行示例。 对于 ISO Shell，请根据需要更改目录和 launchingApp 值以匹配产品。

     "C:\Program Files (x86) \Microsoft 帮助 Viewer\v2.3\HlpViewer.exe"/catalogName VisualStudio15/helpQuery method = "page&id = ContosoTopic0"/launchingApp Microsoft，VisualStudio，12。0

10. 从 Contoso 应用根) 启动 Contoso 应用程序 (。 在 ISO Shell 中，选择 " **帮助** " 菜单项，然后将 " **设置帮助首选项** " 更改为 " **使用本地帮助**"。

11. 在 shell 中，选择 " **帮助** " 菜单项，然后单击 " **查看帮助**"。 本地帮助查看器应启动。 选择 " **管理内容** " 选项卡。在 " **安装源**" 下，选择 " **磁盘** " 选项按钮。 选择 " **...** " 按钮，并浏览到包含 Contoso 内容的本地文件夹， (复制到上述步骤) 中的本地文件夹。 选择 Helpcontentsetup.msha. .msha。 Contoso 现在应显示为书籍中的一本书。 选择 " **添加**"，然后选择)  (右下角的 " **更新** " 按钮。

12. 在 Contoso IDE 中，选择 F1 键来测试 F1 功能。

## <a name="additional-resources"></a>其他资源

有关运行时 API，请参阅 [Windows 帮助 API](/previous-versions/windows/desktop/helpapi/helpapi-portal)。

有关如何利用帮助 API 的详细信息，请参阅 [帮助查看器代码示例](https://marketplace.visualstudio.com/items?itemName=RobChandlerHelpMVP.HelpViewer20CodeExamples)。

你可以在 [开发人员社区](https://aka.ms/feedback/suggest?space=8)提交功能建议。
