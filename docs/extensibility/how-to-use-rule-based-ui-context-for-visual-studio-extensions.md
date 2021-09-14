---
title: 将基于规则的 UI 上下文用于 Visual Studio 扩展
titleSuffix: ''
description: 了解如何使用基于规则的 UI 上下文，使扩展创作者可以在激活 UI 上下文和加载 Vspackage 时定义条件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 8dd2cd1d-d8ba-49b9-870a-45acf3a3259d
author: leslierichardson95
ms.author: lerich
ms.workload:
- vssdk
ms.openlocfilehash: 0ce09edd20c0c46a6b93ace77808fdfc7d5d1c5d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600770"
---
# <a name="how-to-use-rule-based-ui-context-for-visual-studio-extensions"></a>如何：将基于规则的 UI 上下文用于 Visual Studio 扩展

Visual Studio 允许在激活特定的已知时加载 vspackage <xref:Microsoft.VisualStudio.Shell.UIContext> 。 但是，这些 UI 上下文并不精细，这会使扩展创作者不会选择，而是选择在真正想要 VSPackage 加载的位置之前激活的可用 UI 上下文。 有关众所周知的 UI 上下文的列表，请参阅 <xref:Microsoft.VisualStudio.Shell.KnownUIContexts> 。

加载包可能会影响性能，并且比所需的更早加载它们并不是最佳做法。 Visual Studio 2015 介绍了基于规则的 UI 上下文的概念，这是一种机制，允许扩展创作者定义激活 UI 上下文并加载 vspackage 时所用的精确条件。

## <a name="rule-based-ui-context"></a>基于规则的 UI 上下文

"规则" 包含新的 UI 上下文 (GUID) 和引用一个或多个 "字词" 以及逻辑 "and"、"or"、"not" 运算的布尔表达式。 "字词" 会在运行时动态计算，只要其任何字词发生更改，就会重新计算表达式。 当表达式的计算结果为 true 时，将激活关联的 UI 上下文。 否则，将取消激活 UI 上下文。

可以通过多种方式使用基于规则的 UI 上下文：

1. 指定命令和工具窗口的可见性约束。 您可以隐藏 "命令/工具" 窗口，直到满足 UI 上下文规则。

2. 自动加载约束：仅在满足规则时自动加载包。

3. 延迟任务：延迟加载，直到超过指定的间隔，并且仍满足规则。

   任何 Visual Studio 扩展都可以使用该机制。

## <a name="create-a-rule-based-ui-context"></a>创建基于规则的 UI 上下文
 假设你有一个名为 TestPackage 的扩展，该扩展提供仅适用于具有 *.config* 扩展名的文件的菜单命令。 在 VS2015 之前，最佳选择是在 <xref:Microsoft.VisualStudio.Shell.KnownUIContexts.SolutionExistsAndFullyLoadedContext%2A> 激活 UI 上下文时加载 TestPackage。 以这种方式加载 TestPackage 的效率不高，因为加载的解决方案甚至不能包含 *.config* 文件。 以下步骤演示了如何使用基于规则的 UI 上下文来仅在选择了具有 *.config* 扩展名的文件时激活 ui 上下文，并在激活该 ui 上下文时加载 TestPackage。

1. 定义新的 UIContext GUID 并添加到 VSPackage 类 <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> 和 <xref:Microsoft.VisualStudio.Shell.ProvideUIContextRuleAttribute> 。

    例如，假设要添加一个新的 UIContext "UIContextGuid"。 创建 guid (可以通过单击 "**工具**  >  " "**创建 guid** ") 为 "8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B" 创建 guid。 然后，将以下声明添加到包类中：

   ```csharp
   public const string UIContextGuid = "8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B";
   ```

    对于属性，请添加以下值：稍后将介绍这些属性的 (详细信息) 

   ```csharp
   [ProvideAutoLoad(TestPackage.UIContextGuid)]
   [ProvideUIContextRule(TestPackage.UIContextGuid,
       name: "Test auto load",
       expression: "DotConfig",
       termNames: new[] { "DotConfig" },
       termValues: new[] { "HierSingleSelectionName:.config$" })]
   ```

    这些元数据定义了新的 UIContext GUID (8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B) 和引用单个术语 "DotConfig" 的表达式。 当活动层次结构中的当前选定内容具有与正则表达式模式 ".config$" 匹配的名称时，"DotConfig" 项的计算结果为 true \\ (以 *.config*) 结尾。  (默认) 值定义用于调试的规则的可选名称。

    此属性的值将添加到生成时生成时生成的 .pkgdef 中。

2. 在 TestPackage 的命令的 .VSCT 文件中，将 "DynamicVisibility" 标志添加到相应的命令：

   ```xml
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

3. 在 .VSCT 的可见性节中，将相应的命令绑定到 #1 中定义的新 UIContext GUID：

   ```xml
   <VisibilityConstraints>
       <VisibilityItem guid="guidTestPackageCmdSet" id="TestId"  context="UIContextGuid"/>
   </VisibilityConstraints>
   ```

4. 在 "符号" 部分中，添加 UIContext 的定义：

   ```xml
   <GuidSymbol name="UIContextGuid" value="{8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B}" />
   ```

    现在，仅当 "解决方案资源管理器" 中的选定项是 *.config* 文件时，才会显示 *\*.config* 文件的上下文菜单命令，并且在选择其中一个命令之前不会加载包。

   接下来，使用调试器确认包仅在预期时加载。 调试 TestPackage：

5. 在方法中设置断点 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 。

6. 生成 TestPackage 并启动调试。

7. 创建一个项目或打开一个项目。

8. 选择扩展名不是 *.config* 的任何文件。不应命中断点。

9. 选择 *App.Config* 文件。

   TestPackage 加载并停止在断点处。

## <a name="add-more-rules-for-ui-context"></a>为 UI 上下文添加更多规则
 由于 UI 上下文规则是布尔表达式，因此你可以为 UI 上下文添加更多限制的规则。 例如，在上面的 UI 上下文中，你可以指定仅当加载包含项目的解决方案时才应用规则。 这样一来，如果将 *.config* 文件打开为独立的文件，而不是项目的一部分，则命令将不会显示。

```csharp
[ProvideAutoLoad(TestPackage.UIContextGuid)]
[ProvideUIContextRule(TestPackage.UIContextGuid,
    name: "Test auto load",
    expression: "(SingleProject | MultipleProjects) & DotConfig",
    termNames: new[] { "SingleProject", "MultipleProjects","DotConfig" },
    termValues: new[] { VSConstants.UICONTEXT.SolutionHasSingleProject_string , VSConstants.UICONTEXT.SolutionHasMultipleProjects_string , "HierSingleSelectionName:.config$" })]
```

 现在，表达式引用了三个字词。 前两个术语 "SingleProject" 和 "MultipleProjects" 引用其他已知的 UI 上下文 (其 Guid) 。 第三个术语 "DotConfig" 是本文前面部分定义的基于规则的 UI 上下文。

## <a name="delayed-activation"></a>延迟激活
 规则可以具有可选的 "延迟"。 延迟以毫秒为单位指定。 如果存在，延迟将导致规则的 UI 上下文激活或停用延迟为该时间间隔。 如果规则更改回延迟间隔之前，则不会发生任何事情。 此机制可用于 "错开" 初始化步骤（特别是一次性初始化），而无需依赖计时器或注册空闲通知。

 例如，可以指定测试负载规则延迟为100毫秒：

```csharp
[ProvideAutoLoad(TestPackage.UIContextGuid)]
[ProvideUIContextRule(TestPackage.UIContextGuid,
    name: "Test auto load",
    expression: "DotConfig",
    termNames: new[] { "DotConfig" },
    termValues: new[] { "HierSingleSelectionName:.config$" },
    delay: 100)]
```

## <a name="term-types"></a>术语类型

下面是受支持的各种类型的术语：

|术语|说明|
|-|-|
|{nnnnnnnn-nnnnnnnnnnnn}|GUID 引用 UI 上下文。 每当 UI 上下文处于活动状态时，术语为 true，否则为 false。|
|HierSingleSelectionName:\<pattern>|当活动层次结构中的选定内容为单个项并且所选项的名称与 "pattern" 给定的 .Net 正则表达式匹配时，将为 true。|
|UserSettingsStoreQuery:\<query>|"查询" 表示用户设置存储中的完整路径，其计算结果必须为非零值。 查询拆分为最后一个斜杠的 "集合" 和 "属性名称"。|
|ConfigSettingsStoreQuery:\<query>|"查询" 表示配置设置存储中的完整路径，其计算结果必须为非零值。 查询拆分为最后一个斜杠的 "集合" 和 "属性名称"。|
|ActiveProjectFlavor:\<projectTypeGuid>|每当当前选定的项目 (聚合) 并且具有与给定项目类型 GUID 匹配的口味时，此术语就为 true。|
|ActiveEditorContentType:\<contentType>|当所选文档是具有给定内容类型的文本编辑器时，此术语为 true。 注意：在重命名所选文档后，在关闭并重新打开该文件之前，不会刷新此术语。|
|ActiveProjectCapability:\<Expression>|当活动项目功能与提供的表达式匹配时，术语为 true。 表达式可以是类似于 VB &#124; CSharp 的内容。|
|SolutionHasProjectCapability:\<Expression>|与上面类似，但当解决方案具有与表达式匹配的任何已加载项目时，term 为 true。|
|SolutionHasProjectFlavor:\<projectTypeGuid>|只要解决方案包含的项目为风格 (聚合) 并且具有与给定项目类型 GUID 匹配的风格，就会出现这种情况。|
|ProjectAddedItem:\<pattern>| 当与 "pattern" 匹配的文件添加到打开的 soluion 中的项目时，这一术语为 true。|
|ActiveProjectOutputType:\<outputType>|当活动项目的输出类型完全匹配时，术语为 true。  OutputType 可以是整数或 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROJOUTPUTTYPE> 类型。|
|ActiveProjectBuildProperty:\<buildProperty>=\<regex>|当活动项目具有与提供的 regex 筛选器匹配的指定生成属性和属性值时，术语为 true。 有关生成属性的更多详细信息，请参阅[MSBuild Project 文件中保存数据](internals/persisting-data-in-the-msbuild-project-file.md)。|
|SolutionHasProjectBuildProperty:\<buildProperty>=\<regex>|当解决方案具有已加载的项目，且该项目的指定生成属性和属性值与提供的 regex 筛选器匹配时，此术语为 true。|

## <a name="compatibility-with-cross-version-extension"></a>跨版本扩展的兼容性

基于规则的 UI 上下文是 Visual Studio 2015 的一项新功能，不会移植到早期版本。 如果不迁移到早期版本，则会出现针对 Visual Studio 的多个版本的扩展/包的问题。 这些版本必须在 Visual Studio 2013 及更早版本中自动加载，但可以从基于规则的 UI 上下文中获益，以防止在 Visual Studio 2015 中自动加载。

为了支持此类包，注册表中的 AutoLoadPackages 条目现在可以在其值字段中提供一个标志，以指示应在 Visual Studio 2015 及以上版本跳过该条目。 可以通过向 添加标志选项来完成此操作 <xref:Microsoft.VisualStudio.Shell.PackageAutoLoadFlags> 。 VSPackages 现在可以将 **SkipWhenUIContextRulesActive** 选项添加到其 属性，以指示在 <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> 2015 和 2015 及Visual Studio中应忽略该条目。
## <a name="extensible-ui-context-rules"></a>可扩展的 UI 上下文规则

有时，包不能使用静态 UI 上下文规则。 例如，假设有一个包支持扩展性，使命令状态基于导入的 MEF 提供程序支持的编辑器类型。 如果存在支持当前编辑类型的扩展，则启用 命令。 在这种情况下，包本身不能使用静态 UI 上下文规则，因为术语将根据可用的 MEF 扩展而更改。

为了支持此类包，基于规则的 UI 上下文支持硬编码表达式"*"，该表达式指示以下所有术语都将与 OR 联接。 这允许主包定义已知的基于规则的 UI 上下文，并在其命令状态与此上下文进行连接。 之后，针对主包的任何 MEF 扩展都可以为它支持的编辑器添加其术语，而不会影响其他术语或主表达式。

构造函数 <xref:Microsoft.VisualStudio.Shell.ProvideExtensibleUIContextRuleAttribute.%23ctor%2A> 文档演示可扩展 UI 上下文规则的语法。
