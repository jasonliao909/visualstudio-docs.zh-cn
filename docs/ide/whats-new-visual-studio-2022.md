---
title: Visual Studio 2022 中的新增功能
titleSuffix: ''
description: 了解 Visual Studio 2022 中的新增功能。
ms.date: 01/26/2022
helpviewer_keywords:
- Visual Studio, what's new
- what's new [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: ''
ms.prod: visual-studio-dev17
ms.topic: conceptual
ms.workload:
- multiple
ms.openlocfilehash: 3b5181f8cbc173a90146f38ecae1f22ff6bae76c
ms.sourcegitcommit: ebd651e00fe3bae5914c211c4828219bf7d1fc70
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2022
ms.locfileid: "137798530"
---
# <a name="whats-new-in-visual-studio-2022"></a>Visual Studio 2022 中的新增功能

已针对 17.0 GA（正式发布）版进行了更新。 参阅[完整的发行说明](/visualstudio/releases/2022/release-notes) | 查看[产品路线图](/visualstudio/productinfo/vs-roadmap/)

>[!div class="button"]
>[下载 Visual Studio 2022](https://visualstudio.microsoft.com/downloads/)

使用 [Visual Studio 2022](https://visualstudio.microsoft.com/vs/)，你将始终获得可供任何开发人员、应用和平台使用的一流工具和服务。 无论是首次使用 Visual Studio 还是已经使用多年，此最新版本都有很多让你惊艳的地方！

> [!TIP]
> 请在我们的 [YouTube 频道](https://www.youtube.com/visualstudio)上观看 [Visual Studio 2022 发布活动](https://www.youtube.com/watch?v=f8jXO946eDw)。 你也可以在我们的 [Twitch 频道](https://www.twitch.tv/visualstudio)上收看。

## <a name="performance-improvements"></a>性能改进

Visual Studio 2022 速度更快、更容易上手且更轻量，专为学习者和工业级解决方案生成者而设计。

### <a name="visual-studio-2022-is-64-bit"></a>Visual Studio 2022 为 64 位

Windows 上的 Visual Studio 2022 现在是 64 位应用程序。 这意味着，可以在不耗尽内存的情况下打开、编辑、运行和调试最大且最复杂的解决方案。 有关详细信息，请参阅 [Visual Studio 2022 愿景](https://devblogs.microsoft.com/visualstudio/visual-studio-2022/)和 [Visual Studio 2022 Preview 1](https://devblogs.microsoft.com/visualstudio/visual-studio-2022-preview-1-now-available/) 博客文章。

### <a name="find-in-files-is-faster"></a>在文件中更快地查找

在[Visual Studio 2022](https://devblogs.microsoft.com/visualstudio/visual-studio-2022-preview-4-is-now-available/)中，我们将重点放在改善几个关键功能的性能上。 例如，在搜索 [Orchard Core](https://github.com/OrchardCMS/OrchardCore) 等大型解决方案时，[在文件中查找](find-in-files.md)功能的速度现在比以前快了 3 倍。

:::image type="content" source="media/vs-2022/find-files-faster.gif" alt-text="&quot;在文件中查找&quot; 功能的动画在搜索大型 c # 解决方案比以前版本的 Visual Studio 快三倍。":::

> [!NOTE]
> **17.1 预览版3中的新增** 内容：通过新的索引搜索，"在文件中查找" 的速度更快！ 有关详细信息，请参阅[Visual Studio 2022 中的代码搜索即将获得更快](https://devblogs.microsoft.com/visualstudio/code-search-in-visual-studio-is-about-to-get-much-faster/)的博客文章。

## <a name="build-modern-apps"></a>生成新式应用

使用 Visual Studio 2022 可以在 Azure 中快速轻松地生成新式基于云的应用程序。 同样，我们的新版本还对 Windows 和 Mac 开发人员的 web、客户端和移动应用程序的[.net 6](https://devblogs.microsoft.com/dotnet/announcing-net-6/)及其统一框架提供完全支持。 而且，Visual Studio 2022 提供对 c + + 工作负荷的强大支持，其中包含新的工作效率功能、c + + 20 工具和[IntelliSense](using-intellisense.md)。

### <a name="better-dev-tools-for-c-and-net-and-hot-reload"></a>适用于 C++、.NET 和热重载的更佳开发工具

[Visual Studio 2022](https://devblogs.microsoft.com/visualstudio/visual-studio-2022-preview-2-is-out/)包括更好的跨平台应用开发工具和最新版本的 c + + 生成工具，以提供 c + + 20 支持。

同时，我们正在更新热重载，以便可以在应用程序运行时编辑 C++ 或 .NET 项目。 有关详细信息，请参阅[在 Visual Studio 2022 中使用热重载加快 .NET 和 C++ 开发](https://devblogs.microsoft.com/visualstudio/speed-up-your-dotnet-and-cplusplus-development-with-hot-reload-in-visual-studio-2022/)博客文章，以及[在 Visual Studio 中使用 C#、C++ 或 Visual Basic 通过热重载编写和调试正在运行的代码](../debugger/hot-reload.md)文档页面。

### <a name="updates-for-blazor--razor-editors--hot-reload-for-aspnet"></a>对 Blazor 和 Razor 编辑器 + 适用于 ASP.NET 的热重载的更新

[Visual Studio 2022](https://devblogs.microsoft.com/visualstudio/visual-studio-2022-preview-4-is-now-available/)包含 Blazor 和 [Razor](https://devblogs.microsoft.com/visualstudio/introducing-the-new-razor-editor-in-visual-studio-2022/)编辑器的重要更新，**并在 ASP.NET Core** 包括在 &mdash; 保存文件时或将更改应用到 CSS 文件时进行 **热** 重载这一新功能！

:::image type="content" source="media/vs-2022/hot-reload-blazor-css-live.gif" alt-text="Razor 和 Blazor 应用以及实时 CSS 文件中的热重载动画。":::

## <a name="innovation-at-your-fingertips"></a>创新触手可及

通过实时 & 异步协作工具来改善与你的每日工作流无缝集成的见解和生产力工具，Visual Studio 2022 具有此功能。

### <a name="multi-repo-support-with-git-in-the-ide"></a>在 IDE 中使用 Git 的多存储库支持

如果你处理过托管在不同 Git 存储库上的项目，你可能已使用外部工具或多个 Visual Studio 实例与它们连接。 在[Visual Studio 2022](https://devblogs.microsoft.com/visualstudio/visual-studio-2022-preview-3-now-available/)中，你可以使用单个解决方案，该解决方案具有多个存储库中的项目，并从单个 Visual Studio 实例中对这些项目进行贡献。 若要了解详细信息，请参阅 [Visual Studio 中的多存储库支持](https://devblogs.microsoft.com/visualstudio/multi-repo-support-in-visual-studio/)博客文章。

> [!NOTE]
> **17.1 预览版2中的新增** 功能：我们将继续为 Git 功能集添加更多的功能。 有关最新信息，请参阅[新的 Git 功能简介 Visual Studio 2022](https://devblogs.microsoft.com/visualstudio/introducing-new-git-features-to-visual-studio-2022/)博客文章。

### <a name="intellicode-improvements"></a>IntelliCode 改进

* 整行完成：在 Visual Studio 2022 中，[IntelliCode](/visualstudio/intellicode/) 功能现在可以一次自动完成整行代码。 有关详细信息，请参阅[借助 IntelliCode 完成键入较少内容即可获得较多代码](https://devblogs.microsoft.com/visualstudio/type-less-code-more-with-intellicode-completions/)博客文章。

* **快速操作建议**： [Visual Studio 2022](https://devblogs.microsoft.com/visualstudio/visual-studio-2022-preview-4-is-now-available/)中的新增内容，IntelliCode 现在可以在你执行常见任务时发现，并建议正确的 [快速操作](quick-actions.md)，并在你键入时正确完成此操作。 有关详细信息，请参阅[使用 IntelliCode 在键入时发现常见任务的快速操作](https://devblogs.microsoft.com/visualstudio/discover-quick-action-intellicode/)博客文章。

## <a name="designing-for-everyone"></a>为每个人设计

我们正在重新整理用户界面，以便使你的操作更加顺畅。 其中一些更改包括外观修改，目的是使 UI 现代化或减轻元素拥挤情况。

### <a name="look--feel"></a>外观和感觉

从新的图标到细微的颜色对比度调整和新的 [Cascadia Code](https://github.com/microsoft/cascadia-code#welcome) 字体，我们致力于使每个人都能更轻松地使用 Visual Studio 2022。 有关所有详细信息，请参阅[我们已升级 Visual Studio 2022 中的 UI](https://devblogs.microsoft.com/visualstudio/weve-upgraded-the-ui-in-visual-studio-2022/) 博客文章。

:::image type="content" source="media/vs-2022/icon-refresh.png" alt-text="屏幕快照显示了 Visual Studio 中之前的图标和刷新后的图标之间的对比。":::

### <a name="personalization"></a>个性化设置

我们的主要重点之一是使 Visual Studio 更加个性化和灵活，使 IDE 成为你自己的 IDE。 例如， [Visual Studio 2022](https://devblogs.microsoft.com/visualstudio/visual-studio-2022-preview-3-now-available/)使你能够与 Windows 主题进行同步。 因此，如果你在其中启用了“夜灯”功能，Visual Studio 也将使用此功能。 有关详细信息，请参阅[个性化设置 Visual Studio 2022](https://devblogs.microsoft.com/visualstudio/personalize-your-visual-studio-2022/) 博客文章。

## <a name="whats-next"></a>后续步骤

想要详细了解我们对 Visual Studio 2022 制定的计划吗？ 有关详细信息，请参阅[路线图](/visualstudio/productinfo/vs-roadmap/)页和 [Visual Studio 2022 预览版](/visualstudio/releases/2022/release-notes-preview/)发行说明 。

## <a name="give-us-feedback"></a>给我们提供反馈

为什么将反馈发送至 Visual Studio 团队？ 因为我们严肃对待客户反馈。 这会给予我们巨大的行事动力。

* 如果想对如何改进 Visual Studio 提出建议，可以使用[功能建议](suggest-a-feature.md)工具。

* 如果遇到 Visual Studio 停止响应、崩溃或其他性能问题，可利用[报告问题](how-to-report-a-problem-with-visual-studio.md)工具与我们轻松共享重现步骤和支持文件。

## <a name="see-also"></a>请参阅

* [Visual Studio 2022 现已推出](https://devblogs.microsoft.com/visualstudio/visual-studio-2022-now-available/)
* [发布：Visual Studio 2022 GA（正式发布）](https://devblogs.microsoft.com/visualstudio/join-us-november-8th-for-the-launch-of-visual-studio-2022/)
* [Visual Studio 2022 RC（候选发布版本）](https://devblogs.microsoft.com/visualstudio/join-us-november-8th-for-the-launch-of-visual-studio-2022/)
* [Visual Studio 2022 预览版 4](https://devblogs.microsoft.com/visualstudio/visual-studio-2022-preview-4-is-now-available/)
* [Visual Studio 2022 预览版 3](https://devblogs.microsoft.com/visualstudio/visual-studio-2022-preview-3-now-available/)
* [Visual Studio 2022 预览版 2](https://devblogs.microsoft.com/visualstudio/visual-studio-2022-preview-2-is-out/)
* [Visual Studio 2022 预览版 1](https://devblogs.microsoft.com/visualstudio/visual-studio-2022-preview-1-now-available/)
* [Visual Studio 2022 愿景](https://devblogs.microsoft.com/visualstudio/visual-studio-2022/)