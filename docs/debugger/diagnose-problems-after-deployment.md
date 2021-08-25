---
title: 在部署后诊断问题 | Microsoft Docs
description: 在 Visual Studio 中使用 IntelliTrace 于部署后诊断问题。 在发布中包含生成信息。 发布并监视应用以发现问题。
ms.custom: SEO-VS-2020
ms.date: 04/10/2018
ms.topic: how-to
ms.assetid: a3463eab-a352-4d17-8551-adbaad526db0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 192389c32a8ff5193b545a1a4159441bab298a8b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122031008"
---
# <a name="diagnose-problems-after-deployment-using-intellitrace-c-visual-basic"></a>使用 IntelliTrace在部署后诊断问题（C#、Visual Basic）

要在使用 IntelliTrace 部署后诊断 ASP.NET Web 应用中的问题，请加入发行版本信息，以便 Visual Studio 自动查找调试 IntelliTrace 日志所需的正确源文件及符号文件。

 如果当前使用 Microsoft Monitoring Agent 控制 IntelliTrace，则还需在 Web 服务器上设置应用程序性能监视。 这样可在应用运行时记录诊断事件，并将这些事件保存到 IntelliTrace 日志文件。 然后可以在 Visual Studio Enterprise（并非 Professional 或 Community 版）中查看事件，转到发生事件的代码，查看在该时间点记录的值，然后在已运行的代码中向前或向后移动。 在找到并解决问题后，重复生成、发布和监控发布这一循环，以便可以更早更快地解决将来的潜在问题。

 ![代码、生成、发布、监视、诊断、修复](../debugger/media/ffr_cycle.png "FFR_Cycle")

 需要的软件：

- Visual Studio、Azure DevOps 或 Team Foundation Server 2017、2015、2013、2012 或 2010，用于设置生成

- 用于监视应用和记录诊断数据的 Microsoft Monitoring Agent

- Visual Studio Enterprise（并非 Professional 或 Community 版），用于查看诊断数据并使用 IntelliTrace 调试代码的

## <a name="step-1-include-build-information-with-your-release"></a><a name="SetUpBuild"></a> 步骤 1：在发布中包含生成信息
 设置生成过程，为 Web 项目创建生成清单（BuildInfo.config 文件）并在发布中包含此清单。 此清单包含有关项目、源代码管理和用于创建特定生成的生成系统的信息。 在你打开 IntelliTrace 日志以查看记录的事件时，此信息可帮助 Visual Studio 查找匹配的源和符号。

### <a name="create-the-build-manifest-for-an-automated-build-using-team-foundation-server"></a><a name="AutomatedBuild"></a> 使用 Team Foundation Server 为自动化生成创建生成清单

 无论你使用 Team Foundation 版本控制还是 Git，请按照这些步骤进行操作。

#### <a name="azure-devops-and-team-foundation-server-2017"></a><a name="TFS2017"></a> Azure DevOps 和 Team Foundation Server 2017

Visual Studio 2017 及更高版本不包括 BuildInfo.config 文件，该文件已被弃用且已被删除。 若要在部署后调试 ASP.NET Web 应用，请使用以下方法之一：

* 若要部署到 Azure，请使用 [Application Insights](/azure/application-insights/)。

* 如果需要使用 IntelliTrace，请在 Visual Studio 中打开项目，并从匹配的生成中加载符号文件。 可以从“模块”窗口加载符号文件，或通过在“工具” > “选项” > “调试” > “符号”中配置符号来进行加载    。

#### <a name="team-foundation-server-2013"></a><a name="TFS2013"></a> Team Foundation Server 2013
 设置生成管道以将源、生成和符号的位置添加到生成清单（BuildInfo.config 文件）。 Team Foundation Build 自动创建此文件并将其放置在项目的输出文件夹中。

1. [编辑生成管道或创建新的生成管道。](/azure/devops/pipelines/get-started-designer?view=vsts&preserve-view=true)

     ![在 TFS 2013 中查看生成管道](../debugger/media/ffr_tfs2013viewbuilddefinition.png "FFR_TFS2013ViewBuildDefinition")

2. 选择默认模板 (TfvcTemplate.12.xaml) 或自己的自定义模板。

     ![选择生成过程模板 - TFS 2013](../debugger/media/ffr_tfs2013buildprocesstemplate.png "FFR_TFS2013BuildProcessTemplate")

3. 指定保存符号 (PDB) 文件的位置，以便自动为你的源编制索引。

     如果使用自定义模板，请确保该模板具有用于为源编制索引的活动。 之后你将添加 MSBuild 参数以指定保存符号文件的位置。

     ![在生成管道 TFS 2013 中设置符号路径](../debugger/media/ffr_tfs2013builddefsymbolspath.png "FFR_TFS2013BuildDefSymbolsPath")

     有关符号的详细信息，请参阅 [发布符号数据](/azure/devops/pipelines/tasks/build/index-sources-publish-symbols?view=vsts&preserve-view=true)。

4. 添加此 MSBuild 参数以在生成清单文件中包含 TFS 和符号位置：

     **/p:IncludeServerNameInBuildInfo=True**

     任何可访问你的 Web 服务器的人都可以在生成清单中看见这些位置。 请确保你的源服务器是安全的。

5. 如果使用自定义模板，请添加此 MSBuild 参数，以指定保存符号文件的位置：

     /p:BuildSymbolStorePath=\<*path to symbols*>

     ![在生成定义 TFS 2013 中包括生成服务器信息](../debugger/media/ffr_tfs2013builddefincludeserverinfo.png "FFR_TFS2013BuildDefIncludeServerInfo")

     将这些行添加到你的 Web 项目文件（.csproj、.vbproj）中：

    ```xml
    <!-- Import the targets file. Change the folder location as necessary. -->
       <Import Project=""$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\BuildInfo\Microsoft.VisualStudio.ReleaseManagement.BuildInfo.targets" />

    ```

     任何可访问你的 Web 服务器的人都可以在生成清单中看见这些位置。 请确保你的源服务器是安全的。

6. 运行新的生成。

    转到[步骤 2：发布应用](#DeployRelease)

#### <a name="team-foundation-server-2012-or-2010"></a><a name="TFS2012_2010"></a> Team Foundation Server 2012 或 2010
 若要为项目自动创建生成清单（BuildInfo.config 文件）并将其置于你的项目的输出文件夹中，请执行以下步骤。 此文件在输出文件夹中显示为“*ProjectName*.BuildInfo.config”，但是在你发布应用后将在部署文件夹中重命名为“BuildInfo.config”。

1. 在你的 Team Foundation Build 服务器上安装 Visual Studio 2013（任意版本）。

2. 在你的生成管道中，指定保存符号的位置，以便自动为你的源编制索引。

     如果使用自定义模板，请确保该模板具有用于为源编制索引的活动。

3. 将这些 MSBuild 参数添加到你的生成管道：

    - **/p:VisualStudioVersion=12.0**

    - **/p:MSBuildAssemblyVersion=12.0**

    - **/tv:12.0**

    - **/p:IncludeServerNameInBuildInfo=True**

    - /p:BuildSymbolStorePath=\<*path to symbols*>

4. 运行新的生成。

    转到[步骤 2：发布应用](#DeployRelease)

### <a name="create-the-build-manifest-for-a-manual-build-using-visual-studio"></a><a name="ManualBuild"></a> 使用 Visual Studio 为手动生成创建生成清单
 若要为项目自动创建生成清单（BuildInfo.config 文件）并将其置于你的项目的输出文件夹中，请执行以下步骤。 此文件在输出文件夹中显示为“*ProjectName*.BuildInfo.config”，但是在你发布应用后将在部署文件夹中重命名为“BuildInfo.config”。

1. 在“解决方案资源管理器” 中，卸载 Web 项目。

2. 打开项目文件（.csproj、.vbproj）。 添加这些行：

    ```xml
    <!-- **************************************************** -->
    <!-- Build info -->
    <PropertyGroup>
       <!-- Generate the BuildInfo.config file -->
       <GenerateBuildInfoConfigFile>True</GenerateBuildInfoConfigFile>
       <!-- Include server name in build info -->
       <IncludeServerNameInBuildInfo>True</IncludeServerNameInBuildInfo>
       <!-- Include the symbols path so Visual Studio can find the matching deployed code when you start debugging. -->
       <BuildSymbolStorePath><path to symbols></BuildSymbolStorePath>
    </PropertyGroup>
    <!-- **************************************************** -->
    ```

3. 签入更新的项目文件。

4. 运行新的生成。

    转到[步骤 2：发布应用](#DeployRelease)

### <a name="create-the-build-manifest-for-a-manual-build-using-msbuildexe"></a><a name="MSBuild"></a> 使用 MSBuild.exe 为手动生成创建生成清单
 运行生成时添加这些生成参数：

 **/p:GenerateBuildInfoConfigFile=True**

 **/p:IncludeServerNameInBuildInfo=True**

 /p:BuildSymbolStorePath=\<*path to symbols*>

## <a name="step-2-release-your-app"></a><a name="DeployRelease"></a> 步骤 2：发布应用
 如果使用生成过程创建的 [Web.Deploy 包](/previous-versions/aspnet/dd394698(v=vs.110)) 来部署你的应用，则生成清单从“*ProjectName*.BuildInfo.config”自动重命名为“BuildInfo.config”，并在 Web 服务器上与应用的 Web.config 文件一起放在相同的文件夹中。

 如果你使用其他方法部署应用，请确保生成清单从“*ProjectName*.BuildInfo.config”重命名为“BuildInfo.config”，并且在 Web 服务器上与应用的 Web.config 文件一起放在相同的文件夹中。

## <a name="step-3-monitor-your-app"></a>步骤 3：监视应用
 在 Web 服务器上设置应用程序性能监视，以便可以监视应用程序中的问题、记录诊断事件并将这些事件保存到 IntelliTrace 日志文件中。 请参阅 [监视你的发布的部署问题](../debugger/using-the-intellitrace-stand-alone-collector.md)。

## <a name="step-4-find-the-problem"></a><a name="InvestigateEvents"></a> 步骤 4：查找问题
 你的开发计算机或另一台计算机上将需要 Visual Studio Enterprise，以查看记录的事件并使用 IntelliTrace 调试代码。 你还可以使用诸如 CodeLens、调试器映射和代码映射等工具帮助你诊断问题。

### <a name="open-the-intellitrace-log-and-matching-solution"></a>打开 IntelliTrace 日志和匹配的解决方案

1. 从 Visual Studio Enterprise 中打开 IntelliTrace 日志（.iTrace 文件）。 或者，如果在同一台计算机上装有 Visual Studio Enterprise，则只需双击该文件。

2. 如果该项目没有作为解决方案的一部分而生成，请选择“打开解决方案”  以让 Visual Studio 自动打开匹配的解决方案或项目。 [问：IntelliTrace 日志缺少有关部署的应用程序的信息。为何发生这种情况？我该怎么办？](#InvalidConfigFile)

     Visual Studio 在打开匹配的解决方案或项目时自动搁置挂起的更改。 若要获取有关搁置集的更多详细信息，请在“输出”  窗口或“团队资源管理器” 中查找。

     在进行任何更改之前，请确认你的源代码正确。 如果你使用分支，你可能在不同于 Visual Studio 找到匹配源的分支中工作，例如你的发布分支。

     ![从 IntelliTrace 日志打开解决方案](../debugger/media/ffr_itsummarypageopensolution.png "FFR_ITSummaryPageOpenSolution")

     如果你有映射到此解决方案或项目的现有工作区，Visual Studio 会选择用于放置找到的源的工作区。

     ![从源代码管理打开，到映射的工作区](../debugger/media/ffr_openprojectfromsourcecontrol_mapped.png "FFR_OpenProjectFromSourceControl_Mapped")

     否则，请选择其他工作区或创建新的工作区。 Visual Studio 会将整个分支映射到此工作区。

     ![从源代码管理打开 - 创建新的工作区](../debugger/media/ffr_openprojectfromsourcecontrol_createnewworkspace.png "FFR_OpenProjectFromSourceControl_CreateNewWorkspace")

     若要创建具有特定映射的工作区或不是计算机名称的名称，请选择“管理” 。

     [问：为什么 Visual Studio 提示我选中的工作区域是不合格的？](#IneligibleWorkspace)

     [问：为什么在选择团队集合或不同的集合前，无法继续？](#ChooseTeamProject)

### <a name="diagnose-a-performance-problem"></a>诊断性能问题

1. 在“性能冲突” 下，查看记录的性能事件、其总执行时间以及其他事件信息。 然后，深入查看在特定性能事件期间调用的方法。

     ![查看性能事件详细信息](../debugger/media/ffr_itsummarypageperformance.png "FFR_ITSummaryPagePerformance")

     也可以直接双击事件。

2. 在事件页上，查看这些调用的执行时间。 在执行树中查找缓慢调用。

     当你有多个调用（嵌套调用或其他调用）时，最慢的调用将显示在它们自己的部分中。

     展开调用以查看在该时间点记录的所有嵌套调用和值。 然后，从该调用开始调试。

     ![从方法调用开始调试](../debugger/media/ffr_itsummarypageperformancemethodscalled.png "FFR_ITSummaryPagePerformanceMethodsCalled")

     你也可以双击调用。

     如果方法在应用程序代码中，Visual Studio 将转到该方法。

     ![从性能事件转到应用程序代码](../debugger/media/ffr_itsummarypageperformancegotocode.png "FFR_ITSummaryPagePerformanceGoToCode")

     现在你可以查看其他记录的值和调用堆栈、单步执行代码，或者使用“IntelliTrace”  窗口在此性能事件期间调用的 [其他方法之间“及时”前后移动](../debugger/intellitrace.md) 。

    - [IntelliTrace 日志中所有这些其他事件和信息是什么？](../debugger/using-saved-intellitrace-data.md)
    - [我还能在此处执行什么操作？](#WhatElse)
    - [是否想了解有关性能事件的详细信息？](https://devblogs.microsoft.com/devops/performance-details-in-intellitrace/)

### <a name="diagnose-an-exception"></a>诊断异常

1. 在“异常数据” 下，查看记录的异常事件，它们的类型、消息以及异常发生的时间。 若要深入查看代码，请从异常组中的最近事件开始调试。

     ![从异常事件开始调试](../debugger/media/ffr_itsummarypageexception.png "FFR_ITSummaryPageException")

     也可以直接双击事件。

     如果应用程序代码发生异常，Visual Studio 将转到发生异常的位置。

     ![从异常事件转到应用程序代码](../debugger/media/ffr_itsummarypageexceptiongotocode.png "FFR_ITSummaryPageExceptionGoToCode")

     现在你可以查看其他记录的值和调用堆栈，或者使用“IntelliTrace”  窗口 [在其他记录的事件、相关代码和在这些时间点记录的值之间“及时”前后移动](../debugger/intellitrace.md)。

     [IntelliTrace 日志中所有这些其他事件和信息是什么？](../debugger/using-saved-intellitrace-data.md)

### <a name="what-else-can-i-do-from-here"></a><a name="WhatElse"></a> 我还能在此处执行什么操作？

- [获取有关此代码的详细信息](../ide/find-code-changes-and-other-history-with-codelens.md)。 若要查找对此代码、其更改历史记录、相关 bug、工作项、代码审阅或单元测试的参考（所有操作均无需离开编辑器），请使用编辑器中的 CodeLens 指示器。

     ![CodeLens - 查看对此代码的引用](../debugger/media/ffr_itsummarypageperformancecodelensreferences.png "FFR_ITSummaryPagePerformanceCodeLensReferences")

     ![CodeLens - 查看此代码的更改历史记录](../debugger/media/ffr_itsummarypageperformancecodelensauthors.png "FFR_ITSummaryPagePerformanceCodeLensAuthors")

- [调试时在代码中映射你的位置。](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md) 要直观地跟踪在你的调试会话期间调用的方法，请映射调用堆栈。

     ![在调试时映射调用堆栈](../debugger/media/ffr_itsummarypageperformancedebuggermap.png "FFR_ITSummaryPagePerformanceDebuggerMap")

### <a name="q--a"></a><a name="FAQ"></a> 问题解答

#### <a name="q-why-include-information-about-my-project-source-control-build-and-symbols-with-my-release"></a><a name="WhyInclude"></a> 问：为何在我的发布中包含有关我的项目、源代码管理、生成和符号的信息？
 Visual Studio 使用此信息针对你尝试调试的发布查找匹配的解决方案和源。 在你打开 IntelliTrace 日志并选择要开始调试的事件后，Visual Studio 使用符号查找并向你显示发生事件的代码。 然后你可以查看记录的值，并在代码的执行中向前或向后移动。

 如果在使用 TFS，而且此信息不在生成清单（BuildInfo.config 文件）中，Visual Studio 将在当前连接的 TFS 上查找匹配的源和符号。 如果 Visual Studio 找不到正确的 TFS 或匹配的源，将提示你选择不同的 TFS。

#### <a name="q-the-intellitrace-log-is-missing-information-about-my-deployed-app-why-did-this-happen-what-do-i-do"></a><a name="InvalidConfigFile"></a> 问：IntelliTrace 日志缺少有关部署的应用程序的信息。 为何发生这种情况？ 我该怎么办？
 当你从开发计算机部署或在部署期间未连接到 TFS 时，可能发生此情况。

1. 转到项目的部署文件夹。

2. 查找并打开生成清单（BuildInfo.config 文件）。

3. 确保此文件包含必需的信息：

- **ProjectName**

   Visual Studio 中你的项目的名称。 例如：

  ```xml
  <ProjectName>FabrikamFiber.Extranet.Web</ProjectName>
  ```

- **SourceControl**

- 有关你的源代码管理系统以及以下必需属性的信息：

  - **TFS**

    - ProjectCollectionUri：用于 Team Foundation Server 和项目集合的 URI

    - ProjectItemSpec：应用的项目文件（.csproj 或 .vbproj）的路径

    - ProjectVersionSpec：项目的版本

      例如：

    ```xml
    <SourceControl type="TFS">
       <TfsSourceControl>
          <ProjectCollectionUri>http://fabrikamfiber:8080/tfs/FabrikamFiber</ProjectCollectionUri>
          <ProjectItemSpec>$/WorkInProgress/FabrikamFiber/FabrikamFiber.CallCenter/FabrikamFiber.Web/FabrikamFiber.Web.csproj</ProjectItemSpec>
          <ProjectVersionSpec>LFabrikamFiber_BuildAndPublish_20130813@$/WorkInProgress</ProjectVersionSpec>
       </TfsSourceControl>
    </SourceControl>
    ```

  - **Git**

    - GitSourceControl：GitSourceControl 架构的位置

    - RepositoryUrl：用于 Team Foundation Server、项目集合和 Git 存储库的 URI

    - ProjectPath：应用的项目文件（.csproj 或 .vbproj）的路径

    - CommitId：你的提交的 ID

      例如：

    ```xml
    <SourceControl type="Git">
       <GitSourceControl xmlns="http://schemas.microsoft.com/visualstudio/deploymentevent_git/2013/09">
          <RepositoryUrl>http://gittf:8080/tfs/defaultcollection/_git/FabrikamFiber</RepositoryUrl>
          <ProjectPath>/FabrikamFiber.CallCenter/FabrikamFiber.Web/FabrikamFiber.Web.csproj</ProjectPath>
          <CommitId>50662c96502dddaae5cd5ced962d9f14ec5bc64d</CommitId>
       </GitSourceControl>
    </SourceControl>
    ```

- **生成**

   有关生成系统（ `"TeamBuild"` 或 `"MSBuild"`）以及以下所需属性的信息：

  - BuildLabel（用于 TeamBuild）：生成名称和编号。 此标签也用作部署事件的名称。 有关生成号的详细信息，请参阅 [使用生成号为已完成的生成提供有意义的名称](/azure/devops/pipelines/build/options?view=vsts&preserve-view=true)。

  - SymbolPath（推荐）：你的符号（PDB 文件）位置的 URI 列表，采用分号分隔。 这些 URI 可以是 URL 或 UNC。 它使 Visual Studio 更易于查找匹配的符号以帮助你进行调试。

  - BuildReportUrl（用于 TeamBuild）：TFS 中的生成报告的位置

  - BuildId（用于 TeamBuild）：TFS 中生成详细信息的 URI。 此 URI 也用作部署事件的 ID。 如果不使用 TeamBuild，则此 ID 必须唯一。

  - BuiltSolution：Visual Studio 用于查找和打开匹配的解决方案的解决方案文件的路径。 这是 **SolutionPath** MsBuild 属性的内容。

    例如：

  - **TFS**

    ```xml
    <Build type="TeamBuild">
       <MsBuild>
          <BuildLabel kind="label">FabrikamFiber_BuildAndPublish_20130813.1</BuildLabel>
          <SymbolPath>\\fabrikamfiber\FabrikamFiber.CallCenter\Symbols</SymbolPath>
          <BuildReportUrl kind="informative, url" url="http://fabrikamfiber:8080/tfs/FabrikamFiber/_releasePipeline/FindRelease?buildUri=fabrikamfiber%3a%2f%2f%2fBuild%2fBuild%2f448">Build Report Url</BuildReportUrl>
          <BuildId kind="id">1c4444d2-518d-4673-a590-dce2773c7744,fabrikamfiber:///Build/Build/448</BuildId>
          <BuiltSolution>$/WorkInProgress/FabrikamFiber/FabrikamFiber.CallCenter/FabrikamFiber.CallCenter.sln</BuiltSolution>
       </MsBuild>
    </Build>
    ```

  - **Git**

    ```xml
    <Build type="MSBuild">
       <MSBuild>
          <SymbolPath>\\gittf\FabrikamFiber.CallCenter\Symbols</SymbolPath>
          <BuiltSolution>/FabrikamFiber.CallCenter/FabrikamFiber.CallCenter.sln</BuiltSolution>
       </MSBuild>
    </Build>
    ```

#### <a name="q-why-does-visual-studio-say-my-selected-workspace-is-ineligible"></a><a name="IneligibleWorkspace"></a> 问：为什么 Visual Studio 提示我选中的工作区域是不合格的？
 **答：** 选中的工作区域没有源代码管理文件夹和本地文件夹之间的任何映射。 若要为此工作区创建映射，请选择“管理” 。 否则，请选择已映射的工作区或创建新的工作区。

 ![从没有映射工作区的源代码管理打开](../debugger/media/ffr_openprojectfromsourcecontrol_notmapped.png "FFR_OpenProjectFromSourceControl_NotMapped")

#### <a name="q-why-cant-i-continue-until-i-choose-a-team-collection-or-a-different-collection"></a><a name="ChooseTeamProject"></a> 问：为什么在选择团队集合或不同的集合前，无法继续？
 **答：** 这种情况可能是由于以下原因导致的：

- Visual Studio 未连接到 TFS。

     ![从源代码管理打开 - 未连接](../debugger/media/ffr_openprojectfromsourcecontrol_notconnected.png "FFR_OpenProjectFromSourceControl_NotConnected")

- Visual Studio 未在你的当前团队集合中找到解决方案或项目。

     当生成清单文件 (\<*ProjectName*>.BuildInfo.config) 未指定 Visual Studio 可在何处找到匹配的源时，Visual Studio 将使用你当前连接的 TFS 查找匹配的解决方案或项目。 如果当前团队集合没有匹配的源，Visual Studio 将会提示你连接到不同的团队集合。

- Visual Studio 未在由生成清单文件 (\<*ProjectName*>.BuildInfo.config) 指定的集合中找到解决方案或项目。

     指定的 TFS 可能不再具有匹配的源，甚至不存在（可能是因为你已迁移到新的 TFS）。 如果指定的 TFS 不存在，Visual Studio 在一分钟后可能会超时，然后会提示你连接到不同的集合。 若要继续，请连接到正确的 TFS 服务器。

     ![从源代码管理打开 - 已迁移](../debugger/media/ffr_openprojectfromsourcecontrol_migrated.png "FFR_OpenProjectFromSourceControl_Migrated")

#### <a name="q-whats-a-workspace"></a><a name="WhatWorkspace"></a> 问：什么是工作区？
 **答：** [工作区存储源的副本](/azure/devops/repos/tfvc/create-work-workspaces?view=vsts&preserve-view=true)，因此在签入工作之前，可以对其进行单独开发和测试。 如果尚未具备专门映射到找到的解决方案或项目的工作区，那么 Visual Studio 会提示你选择一个可用的工作区，或以你的计算机名称作为默认工作区名称创建新的工作区。

#### <a name="q-why-do-i-get-this-message-about-untrusted-symbols"></a><a name="UntrustedSymbols"></a> 问：为什么我收到了有关不受信任的符号的消息？
 ![使用不受信任的符号路径进行调试？](../debugger/media/ffr_ituntrustedsymbolpaths.png "FFR_ITUntrustedSymbolPaths")

 **答：** 当受信任的符号路径列表中不包含生成清单文件 (\<*ProjectName*>.BuildInfo.config) 中的符号路径时，会出现此消息。 你可将路径添加到调试器选项中的符号路径列表。