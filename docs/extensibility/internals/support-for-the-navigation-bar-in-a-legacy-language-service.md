---
title: 支持旧版语言服务中的导航栏
description: 了解如何在旧版语言服务中支持导航栏。 编辑器视图中的导航栏显示文件中的类型和成员。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Navigation bar, supporting in language services [managed package framework]
- language services [managed package framework], Navigation bar
ms.assetid: 2d301ee6-4523-4b82-aedb-be43f352978e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 497fd019b0da6beac7776af6926aa24d677813f3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600709"
---
# <a name="support-for-the-navigation-bar-in-a-legacy-language-service"></a>旧版语言服务中的导航栏支持
编辑器视图顶部的导航栏显示文件中类型和成员。 类型显示在左侧下拉列表中，成员显示在右侧下拉列表中。 当用户选择类型时，该类型的第一行上会放置一个 caret。 当用户选择一个成员时，将 caret 置于该成员的定义中。 下拉框会更新，以反映看管的当前位置。

## <a name="displaying-and-updating-the-navigation-bar"></a>显示和更新导航栏
 若要支持导航栏，必须从 类派生类 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> 并实现 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 方法。 为语言服务提供代码窗口时，基类实例化 <xref:Microsoft.VisualStudio.Package.LanguageService> <xref:Microsoft.VisualStudio.Package.CodeWindowManager> ，其中包含 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> 表示代码窗口的 对象。 然后 <xref:Microsoft.VisualStudio.Package.CodeWindowManager> ，为 对象提供一个新的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 对象。 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>方法获取 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> 对象。 如果返回类的实例，则 调用 方法以填充内部列表，将对象传递给下 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> <xref:Microsoft.VisualStudio.Package.CodeWindowManager> <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 拉栏管理器。 而下拉栏管理器又对 对象调用 方法，以建立保存两个下拉条 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.SetDropdownBar%2A> <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBar> 的对象。

 当光标移动时， <xref:Microsoft.VisualStudio.Package.LanguageService.OnIdle%2A> 方法将调用 <xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A> 方法。 基 <xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A> 方法调用 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 类中的 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> 方法以更新导航栏的状态。 将一组 <xref:Microsoft.VisualStudio.Package.DropDownMember> 对象传递给此方法。 每个 对象都表示下拉列表中的一个条目。

## <a name="the-contents-of-the-navigation-bar"></a>导航栏的内容
 导航栏通常包含类型列表和成员列表。 类型列表包括当前源文件中可用的所有类型。 类型名称包括完整的命名空间信息。 下面是具有两种类型的 C# 代码的示例：

```csharp
namespace TestLanguagePackage
{
    public class TestLanguageService
    {
        internal struct Token
        {
            int tokenID;
        }
        private Tokens[] tokens;
        private string serviceName;
    }
}
```

 类型列表将显示 `TestLanguagePackage.TestLanguageService` 和 `TestLanguagePackage.TestLanguageService.Tokens` 。

 成员列表显示类型列表中所选类型的可用成员。 使用上面的代码示例，如果 `TestLanguagePackage.TestLanguageService` 是所选类型，则成员列表将包含私有成员 `tokens` 和 `serviceName` 。 不显示内部 `Token` 结构。

 您可以实现成员列表，使成员名称在将 caret 置于其中时以粗体显示。 成员还可以以灰显文本显示，表示它们不在当前定位了 caret 的范围内。

## <a name="enabling-support-for-the-navigation-bar"></a>启用对导航栏的支持
 若要启用对导航栏的支持，必须将 属性的 `ShowDropdownBarOption` <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 参数设置为 `true` 。 此参数设置 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A> 属性。 若要支持导航栏，必须在 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> 类的 方法 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A> 中实现 <xref:Microsoft.VisualStudio.Package.LanguageService> 对象。

 在 方法的 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A> 实现中，如果 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A> 属性设置为 `true` ，可以返回 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> 对象。 如果不返回对象，则不显示导航栏。

 用户可以设置用于显示导航栏的选项，因此可以在编辑器视图打开时重置此控件。 用户必须在更改发生之前关闭并重新打开编辑器窗口。

## <a name="implementing-support-for-the-navigation-bar"></a>实现对导航栏的支持
 方法采用两个 (一个列表，每个下拉列表) 两个值表示每个列表中的 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 当前选择。 可以更新列表和选择值，在这种情况下，方法必须返回 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> `true` 以指示列表已更改。

 随着类型下拉列表中的选择更改，必须更新成员列表以反映新类型。 成员列表中显示的成员可以是：

- 当前类型的成员列表。

- 源文件中可用的所有成员，但当前类型中不存在的所有成员均以灰显文本显示。 用户仍可以选择灰显成员，以便它们可用于快速导航，但颜色指示它们不是当前所选类型的一部分。

  方法的 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 实现通常执行以下步骤：

1. 获取源文件的当前声明的列表。

     填充列表的方法有很多种。 一种方法是在类版本上创建自定义方法，该方法使用返回所有声明列表的自定义分析原因调用 <xref:Microsoft.VisualStudio.Package.LanguageService> <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法。 另一种方法可能是使用 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 自定义分析原因 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 直接从 方法调用 方法。 第三种方法可能是在 类中最后一个完整分析操作返回的 类中缓存声明，然后 <xref:Microsoft.VisualStudio.Package.AuthoringScope> <xref:Microsoft.VisualStudio.Package.LanguageService> 从 方法中 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 检索该声明。

2. 填充或更新类型列表。

     如果源已更改，或者你已选择根据当前符号位置更改类型的文本样式，则类型列表的内容可能会更新。 请注意，此位置将传递给 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> 方法。

3. 根据当前的点头位置，确定在类型列表中选择的类型。

     可以搜索步骤 1 中获取的声明以查找包含当前插入点位置的类型，然后在类型列表中搜索该类型以确定其索引到类型列表中。

4. 根据所选类型填充或更新成员列表。

     成员列表反映了"成员"下拉列表中 **当前** 显示的内容。 如果源已更改，或者仅显示所选类型的成员并且所选类型已更改，可能需要更新成员列表的内容。 如果选择在源文件中显示所有成员，则如果当前所选类型已更改，则列表中每个成员的文本样式需要更新。

5. 确定要基于当前 caret 位置在成员列表中选择的成员。

     在步骤 1 中获取的声明中搜索包含当前插入点位置的成员，然后搜索该成员的成员列表以确定其索引到成员列表中。

6. 如果 `true` 对列表或任一列表中的选择进行了任何更改，则返回 。
