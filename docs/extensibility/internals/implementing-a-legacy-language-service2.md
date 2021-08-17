---
title: 实现旧版语言服务 2 |Microsoft Docs
description: 了解如何通过使用 MPF 中的托管包框架实现支持扩展语言服务功能 (语言) 。 第 2 部分（第 2 部分，第 2 部分）。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- language services [managed package framework], implementing
ms.assetid: 5bcafdc5-f922-48f6-a12e-6c8507a79a05
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 7a20d4e39d9a70e85a09a534fa224a279027bcde
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122042343"
---
# <a name="implementing-a-legacy-language-service-2"></a>实现旧版语言服务 2
若要使用 MPF (包框架实现语言) ，必须从 类派生类，并 <xref:Microsoft.VisualStudio.Package.LanguageService> 实现以下抽象方法和属性：

- <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> 方法

- <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> 方法

- <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法

- <xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A> 属性

  有关实现这些方法和属性的详细信息，请参阅下面的相应部分。

  若要支持其他功能，语言服务可能需要从其中一个 MPF 语言服务类派生类;例如，若要支持其他菜单命令，必须从 类派生类，并重写多个命令 (方法，了解 <xref:Microsoft.VisualStudio.Package.ViewFilter> <xref:Microsoft.VisualStudio.Package.ViewFilter>) 。 类提供了许多方法，这些方法被调用以创建各种类的新实例，你可以重写相应的创建 <xref:Microsoft.VisualStudio.Package.LanguageService> 方法以提供类的实例。 例如，需要重写 类中的 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A> 方法 <xref:Microsoft.VisualStudio.Package.LanguageService> 以返回自己的类 <xref:Microsoft.VisualStudio.Package.ViewFilter> 的实例。 有关更多详细信息，请参阅"实例化自定义类"部分。

  语言服务还可以提供自己的图标，可在许多位置使用。 例如，当显示 IntelliSense 完成列表时，列表中的每个项都可以具有与之关联的图标，将该项标记为方法、类、命名空间、属性或语言所需的任何内容。 这些图标用于所有 IntelliSense 列表、导航 **栏** 和" **错误列表"任务** 窗口。 有关详细信息，请参阅下面的"语言服务图像"部分。

## <a name="getlanguagepreferences-method"></a>GetLanguagePreferences 方法
 <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>方法始终返回类的相同 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 实例。 如果不需要为语言服务提供任何其他首选项， <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 可以使用基类。 MPF 语言服务类假定至少存在基 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 类。

### <a name="example"></a>示例
 此示例演示 方法的典型 <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> 实现。 此示例使用基 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 类。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private LanguagePreferences m_preferences;

        public override LanguagePreferences GetLanguagePreferences()
        {
            if (m_preferences == null)
            {
                m_preferences = new LanguagePreferences(this.Site,
                                                        typeof(TestLanguageService).GUID,
                                                        this.Name );
                m_preferences.Init();
            }
            return m_preferences;
        }
    }
}
```

## <a name="getscanner-method"></a>GetScanner 方法
 此方法返回 对象的实例，该对象实现用于获取令牌及其类型和触发器的面向行分析器或 <xref:Microsoft.VisualStudio.Package.IScanner> 扫描程序。 此扫描程序在 类中用于着色，尽管扫描程序还可用于获取令牌类型和触发器，作为更复杂的分析操作 <xref:Microsoft.VisualStudio.Package.Colorizer> 的前导。 必须提供实现 接口的 类 <xref:Microsoft.VisualStudio.Package.IScanner> ，并且必须在接口上实现所有 <xref:Microsoft.VisualStudio.Package.IScanner> 方法。

### <a name="example"></a>示例
 此示例演示 方法的典型 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> 实现。 `TestScanner`类实现接口 <xref:Microsoft.VisualStudio.Package.IScanner> (接口) 。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private TestScanner m_scanner;

        public override IScanner GetScanner(IVsTextLines buffer)
        {
            if (m_scanner == null)
            {
                m_scanner = new TestScanner(buffer);
            }
            return m_scanner;
        }
    }
}
    internal class TestScanner : IScanner
    {
        private IVsTextBuffer m_buffer;
        string m_source;

        public TestScanner(IVsTextBuffer buffer)
        {
            m_buffer = buffer;
        }

        bool IScanner.ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo, ref int state)
        {
            tokenInfo.Type = TokenType.Unknown;
            tokenInfo.Color = TokenColor.Text;
            return true;
        }

        void IScanner.SetSource(string source, int offset)
        {
            m_source = source.Substring(offset);
        }
    }

```

## <a name="parsesource-method"></a>ParseSource 方法
 根据许多不同的原因分析源文件。 为此方法提供 <xref:Microsoft.VisualStudio.Package.ParseRequest> 一个 对象，该对象描述特定分析操作的预期结果。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法调用更复杂的分析器，用于确定令牌功能和范围。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法用于支持 IntelliSense 操作以及大括号匹配。 即使不支持此类高级操作，也仍必须返回有效的 对象，这要求创建实现 接口的类，并实现该接口 <xref:Microsoft.VisualStudio.Package.AuthoringScope> <xref:Microsoft.VisualStudio.Package.AuthoringScope> 上的所有方法。 可以从所有方法返回 null 值，但 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 对象本身不能为 null 值。

### <a name="example"></a>示例
 此示例演示 方法和 类的最少实现，足以允许语言服务编译和运行，而无需实际支持任何更 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> <xref:Microsoft.VisualStudio.Package.AuthoringScope> 高级的功能。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        public override AuthoringScope ParseSource(ParseRequest req)
        {
            return new TestAuthoringScope();
        }
    }

    internal class TestAuthoringScope : AuthoringScope
    {
        public override string GetDataTipText(int line, int col, out TextSpan span)
        {
            span = new TextSpan();
            return null;
        }

        public override Declarations GetDeclarations(IVsTextView view,
                                                     int line,
                                                     int col,
                                                     TokenInfo info,
                                                     ParseReason reason)
        {
            return null;
        }

        public override string Goto(VSConstants.VSStd97CmdID cmd, IVsTextView textView, int line, int col, out TextSpan span)
        {
            span = new TextSpan();
            return null;
        }

        public override Methods GetMethods(int line, int col, string name)
        {
            return null;
        }
}
```

## <a name="name-property"></a>Name 属性
 此属性返回语言服务的名称。 此名称必须与注册语言服务时提供的名称相同。 此名称用于许多位置，其中最突出的位置是用于访问 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 注册表的名称的类。 此属性返回的名称不得本地化，因为它在注册表中用于注册表项和密钥名称。

### <a name="example"></a>示例
 此示例演示 属性的一个可能 <xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A> 实现。 请注意，此处的名称是硬编码的：实际名称应从资源文件中获取，以便可用于注册语言服务 [ (请参阅注册](../../extensibility/internals/registering-a-legacy-language-service1.md) 旧版语言服务) 。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        public override string Name
        {
            get { return "Test Language"; }
        }
    }
}
```

## <a name="instantiating-custom-classes"></a>实例化自定义类
 可以重写指定类中的以下方法，以提供每个类自己的版本的实例。

### <a name="in-the-languageservice-class"></a>在 LanguageService 类中

|方法|返回的类|说明|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateCodeWindowManager%2A>|<xref:Microsoft.VisualStudio.Package.CodeWindowManager>|支持向文本视图添加自定义内容。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDocumentProperties%2A>|<xref:Microsoft.VisualStudio.Package.DocumentProperties>|支持自定义文档属性。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>|<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>|支持导航 **栏**。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionFunction>|支持代码片段模板中的函数。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionProvider>|为了支持代码片段 (此方法通常不会重写) 。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateParseRequest%2A>|<xref:Microsoft.VisualStudio.Package.ParseRequest>|为了支持自定义 <xref:Microsoft.VisualStudio.Package.ParseRequest> 结构 (此方法通常不会重写) 。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateSource%2A>|<xref:Microsoft.VisualStudio.Package.Source>|支持格式化源代码、指定注释字符和自定义方法签名。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A>|<xref:Microsoft.VisualStudio.Package.ViewFilter>|支持其他菜单命令。|
|<xref:Microsoft.VisualStudio.Package.Source.GetColorizer%2A>|<xref:Microsoft.VisualStudio.Package.Colorizer>|为了支持语法突出显示 (此方法通常不会重写) 。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>|<xref:Microsoft.VisualStudio.Package.LanguagePreferences>|支持访问语言首选项。 此方法必须实现，但可以返回基类的实例。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>|<xref:Microsoft.VisualStudio.Package.IScanner>|提供用于标识行上的标记类型的分析器。 此方法必须实现， <xref:Microsoft.VisualStudio.Package.IScanner> 并且必须派生自 。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringScope>|提供用于标识整个源文件的功能和范围的分析器。 必须实现此方法，并且必须返回类版本的 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 实例。 如果只想支持语法突出显示 (这需要从) 方法返回的分析器，则除了返回其方法均返回 null 值的类的版本外，在此方法中不能执行任何操作。 <xref:Microsoft.VisualStudio.Package.IScanner> <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> <xref:Microsoft.VisualStudio.Package.AuthoringScope>|

### <a name="in-the-source-class"></a>在源类中

|方法|返回的类|说明|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A>|<xref:Microsoft.VisualStudio.Package.CompletionSet>|对于自定义 IntelliSense 完成列表的显示 (此方法通常不会重写) 。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A>|<xref:Microsoft.VisualStudio.Package.DocumentTask>|对于"错误列表"任务列表中的支持标记;具体而言，支持除打开文件并跳转到导致错误的行之外的功能。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateMethodData%2A>|<xref:Microsoft.VisualStudio.Package.MethodData>|用于自定义 IntelliSense 参数信息工具提示的显示。|
|<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A>|<xref:Microsoft.VisualStudio.Package.CommentInfo>|用于支持注释代码。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateAuthoringSink%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringSink>|在分析操作期间收集信息。|

### <a name="in-the-authoringscope-class"></a>在 AuthoringScope 类中

|方法|返回的类|说明|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A>|<xref:Microsoft.VisualStudio.Package.Declarations>|提供声明的列表，如成员或类型。 此方法必须实现，但可以返回 null 值。 如果此方法返回有效的 对象，则该对象必须是类版本的 <xref:Microsoft.VisualStudio.Package.Declarations> 实例。|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetMethods%2A>|<xref:Microsoft.VisualStudio.Package.Methods>|提供给定上下文的方法签名列表。 此方法必须实现，但可以返回 null 值。 如果此方法返回有效的 对象，则该对象必须是类版本的 <xref:Microsoft.VisualStudio.Package.Methods> 实例。|

## <a name="language-service-images"></a>语言服务映像
 若要提供在整个语言服务中使用的图标列表，请重写 类中的 方法并 <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> 返回包含 <xref:System.Windows.Forms.ImageList> 图标的 。 基 <xref:Microsoft.VisualStudio.Package.LanguageService> 类加载一组默认图标。 由于在需要图标的位置中指定了确切的图像索引，因此如何排列自己的图像列表完全由你决定。

### <a name="images-used-in-intellisense-completion-lists"></a>IntelliSense 完成列表中使用的图像
 对于 IntelliSense 完成列表，为 类的 方法中的每个项指定图像索引，如果要提供图像索引，则必须 <xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A> <xref:Microsoft.VisualStudio.Package.Declarations> 重写该索引。 从 方法返回的值是提供给类构造函数的图像列表的索引，与从类 (中的 方法返回的映像列表相同 (如果重写 类中的 方法以提供不同的图像列表 <xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A> <xref:Microsoft.VisualStudio.Package.CompletionSet>) ，可以更改要用于 <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> <xref:Microsoft.VisualStudio.Package.CompletionSet> <xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A> <xref:Microsoft.VisualStudio.Package.Source> 的映像列表。

### <a name="images-used-in-the-navigation-bar"></a>导航栏中使用的图像
 导航 **栏** 显示类型和成员的列表，用于快速导航可以显示图标。 这些图标从 类中的 <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> 方法获取 <xref:Microsoft.VisualStudio.Package.LanguageService> ，不能专门为导航栏 **重写**。 当表示组合框的列表在 类的 方法中填充时，将指定组合框中用于每个项的索引 (请参阅支持旧版语言服务中的导航栏 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>) 。 [](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md) 这些映像索引以某种方式从分析器获取，通常是通过 类 <xref:Microsoft.VisualStudio.Package.Declarations> 的版本获取的。 获取索引完全由你决定。

### <a name="images-used-in-the-error-list-task-window"></a>"错误列表"任务窗口中使用的图像
 每当方法分析器 (旧版语言服务分析器与扫描程序) 遇到错误，并且将此错误传递给 类中的 方法时，错误列表任务窗口中 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> [](../../extensibility/internals/legacy-language-service-parser-and-scanner.md) <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A> <xref:Microsoft.VisualStudio.Package.AuthoringSink> **都会报告此错误**。 图标可以与任务窗口中显示的每个项相关联，该图标来自从 类中的 方法返回的同一 <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> 图像 <xref:Microsoft.VisualStudio.Package.LanguageService> 列表。 MPF 类的默认行为是不要显示包含错误消息的图像。 但是，可以通过从 类派生类并重写 方法来 <xref:Microsoft.VisualStudio.Package.Source> 重写此 <xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A> 行为。 在该方法中，创建一个新的 <xref:Microsoft.VisualStudio.Package.DocumentTask> 对象。 在返回该对象之前，可以使用 对象 <xref:Microsoft.VisualStudio.Shell.Task.ImageIndex%2A> 上的 属性 <xref:Microsoft.VisualStudio.Package.DocumentTask> 设置图像索引。 这如以下示例所示。 请注意 `TestIconImageIndex` ， 是一个枚举，它列出所有图标并特定于此示例。 你可能有不同的方法在语言服务中标识图标。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    class TestSource : Source
    {
        public override DocumentTask CreateErrorTaskItem(
            TextSpan          span,
            string            filename,
            string            message,
            TaskPriority      priority,
            TaskCategory      category,
            MARKERTYPE        markerType,
            TaskErrorCategory errorCategory)
        {
            DocumentTask taskItem = base.CreateErrorTaskItem(
                                           span,
                                           filename,
                                           message,
                                           priority,
                                           category,
                                           markerType,
                                           errorCategory);
            if (errorCategory == TaskErrorCategory.Error)
            {
                taskItem.ImageIndex = TestIconImageIndex.Error;
            }
            return taskItem;
        }
    }
}
```

## <a name="the-default-image-list-for-a-language-service"></a>语言服务的默认图像列表
 与基本 MPF 语言服务类一起提供的默认图像列表包含许多与更常见的语言元素关联的图标。 这些图标的大部分按六种变体排列，对应于公共、内部、友元、受保护、私有和快捷方式的访问概念。 例如，方法可以具有不同的图标，具体取决于它是公共的、受保护的还是私有的。

 以下枚举指定每个图标集的典型名称，并指定关联的索引。 例如，根据 枚举，可以将受保护方法的图像索引指定为 `(int)IconImageIndex.Method + (int)IconImageIndex.AccessProtected` 。 可更改此枚举中的名称（如需要）。

```csharp
public enum IconImageIndex
        {
            // access types
            AccessPublic = 0,
            AccessInternal = 1,
            AccessFriend = 2,
            AccessProtected = 3,
            AccessPrivate = 4,
            AccessShortcut = 5,

            Base = 6,
            // Each of the following icon type has 6 versions,
            //corresponding to the access types
            Class = Base + 0,
            Constant = Base + 1,
            Delegate = Base + 2,
            Enumeration = Base + 3,
            EnumMember = Base + 4,
            Event = Base + 5,
            Exception = Base + 6,
            Field = Base + 7,
            Interface = Base + 8,
            Macro = Base + 9,
            Map = Base + 10,
            MapItem = Base + 11,
            Method = Base + 12,
            OverloadedMethod = Base + 13,
            Module = Base + 14,
            Namespace = Base + 15,
            Operator = Base + 16,
            Property = Base + 17,
            Struct = Base + 18,
            Template = Base + 19,
            Typedef = Base + 20,
            Type = Base + 21,
            Union = Base + 22,
            Variable = Base + 23,
            ValueType = Base + 24,
            Intrinsic = Base + 25,
            JavaMethod = Base + 26,
            JavaField = Base + 27,
            JavaClass = Base + 28,
            JavaNamespace = Base + 29,
            JavaInterface = Base + 30,
            // Miscellaneous icons with one icon for each type.
            Error = 187,
            GreyedClass = 188,
            GreyedPrivateMethod = 189,
            GreyedProtectedMethod = 190,
            GreyedPublicMethod = 191,
            BrowseResourceFile = 192,
            Reference = 193,
            Library = 194,
            VBProject = 195,
            VBWebProject = 196,
            CSProject = 197,
            CSWebProject = 198,
            VB6Project = 199,
            CPlusProject = 200,
            Form = 201,
            OpenFolder = 202,
            ClosedFolder = 203,
            Arrow = 204,
            CSClass = 205,
            Snippet = 206,
            Keyword = 207,
            Info = 208,
            CallBrowserCall = 209,
            CallBrowserCallRecursive = 210,
            XMLEditor = 211,
            VJProject = 212,
            VJClass = 213,
            ForwardedType = 214,
            CallsTo = 215,
            CallsFrom = 216,
            Warning = 217,
        }
```

## <a name="see-also"></a>请参阅
- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [旧版语言服务概述](../../extensibility/internals/legacy-language-service-overview.md)
- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)
- [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
