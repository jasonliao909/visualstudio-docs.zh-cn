---
title: 分析应用程序SharePoint的性能|Microsoft Docs
description: 分析应用程序SharePoint运行缓慢或效率低下时的性能。 使用Visual Studio分析功能查找有问题的代码。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Profiling.SilverlightWebPartOnly
- VS.SharePointTools.Profiling.DotNetTrustLevel
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, profiling
- performance testing [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, performance testing
- profiling [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 0d230bc3f5f99f03661ec8322fa6e478b39c4048
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664783"
---
# <a name="profile-the-performance-of-sharepoint-applications"></a>分析应用程序SharePoint性能

如果SharePoint应用程序运行缓慢或效率低下，可以使用 Visual Studio 中的分析功能来识别有问题的代码和其他元素。 通过使用负载测试功能，可以确定应用程序在SharePoint（例如，当许多用户同时访问该应用程序时）的性能。 通过运行 Web 性能测试，可以度量应用程序在 Web 上的执行方式。 通过使用编码的 UI 测试，可以验证整个应用程序SharePoint（包括其用户界面）是否正常工作。 将这些测试一起使用时，它们可以帮助你在部署应用程序之前识别性能问题。

## <a name="profile-tools-overview"></a>配置文件工具概述

分析是指在应用程序运行时观察和记录应用程序的性能行为的过程。 通过分析应用程序，可以发现瓶颈、低效代码和内存分配问题等导致应用程序运行缓慢或使用过多内存的问题。 例如，可以使用分析来识别代码中的热点，这些热点是经常调用的代码段，可能会降低应用程序的整体性能。 识别热点后，通常可以优化或消除它们。

可以在集成开发环境中使用多个分析工具 (IDE) 来识别和查找此类性能问题。 这些工具对项目SharePoint与针对其他类型的项目相同Visual Studio方式。 性能分析工具向导将引导你创建使用指定的测试的性能会话。 性能会话是一组配置数据，用于从应用程序收集性能信息，以及一个或多个分析运行的结果。 性能会话存储在项目文件夹中，可以在 中查看 **性能资源管理器。** 有关详细信息，请参阅[了解性能收集方法](../profiling/understanding-performance-collection-methods.md)。

在应用程序中创建并运行配置文件分析后，报表会提供有关其性能的详细信息。 此报表可以包含一些项，例如一段时间的 CPU 使用率图、分层函数调用堆栈或调用树。 报表的确切内容可能会有所不同，具体取决于运行的测试类型，例如采样或检测。 有关详细信息，请参阅报表 [分析工具概述](../profiling/performance-report-overview.md)。

## <a name="performance-session-process"></a>性能会话进程

若要分析应用程序，首先使用分析工具向导创建性能会话。 在菜单栏上，选择"**分析"和****"启动性能向导"。** 完成向导后，请输入性能会话的所需信息，例如所需的配置文件方法和要分析的应用程序。 有关详细信息，请参阅 [如何：使用性能向导](../profiling/how-to-collect-performance-data-for-a-web-site.md)分析网站或 Web 应用程序。 或者，可以使用命令行选项来设置和运行性能会话。 有关详细信息，请参阅[Using the 分析工具 From the Command-Line。](../profiling/using-the-profiling-tools-from-the-command-line.md) 若要手动配置性能会话的各个方面，请参阅 [如何：](../profiling/how-to-manually-create-performance-sessions.md)手动创建性能会话分析工具。 还可以通过以下方法从单元测试 **创建** 性能会话：在测试结果窗口中打开单元测试的快捷菜单，然后选择"创建性能 **会话"。**

设置性能会话后，将保存会话配置，将服务器配置为提供分析数据，并运行应用程序。 使用应用程序时，性能数据将写入日志文件。 性能会话在 **"目标性能资源管理器** 下 **列出** 。 性能会话完成后，其报表将显示在 性能资源管理器 中的 **Reports 文件夹中**。 若要显示报表，请从 打开 **性能资源管理器。** 若要查看或配置性能会话的属性，请打开性能会话的快捷 **性能资源管理器，然后选择**"属性 **"。** 有关性能会话的特定属性详细信息，请参阅为性能会话[配置分析工具。](../profiling/configuring-performance-sessions.md) 若要了解如何解释性能会话的结果，请参阅 [分析分析工具数据](../profiling/analyzing-performance-tools-data.md)。

## <a name="stress-test"></a>压力测试

可以通过在应用程序中创建负载测试和 Web 性能测试来分析应用程序Visual Studio。 在 Visual Studio 中创建负载测试时，可以指定要测试应用程序的因素组合（称为方案）。 这些因素包括负载模式、测试组合模型、测试组合、网络组合和 Web 浏览器组合。 负载测试方案可以包括单元测试和 Web 性能测试。

图 1：负载测试结果示例

![运行负载测试图形视图](../sharepoint/media/load-webgraphs.png "运行负载测试图形视图")

Web 性能测试模拟最终用户如何与应用程序SharePoint交互。 可以通过在浏览器会话中记录 HTTP 请求或通过使用 Web 性能测试记录器 来创建 **Web 性能测试**。 在浏览器会话完成后，Web 性能测试编辑器 **Web** 请求显示在浏览器中。 然后，可以在 Web 性能查看器 中调试 **测试结果结果**。 此外，还可使用 Web 性能测试编辑器 来 **手动生成 Web 性能Web 性能测试编辑器。**

## <a name="test-user-interfaces"></a>测试用户界面

编码的 UI 测试通过其用户界面SharePoint UI 应用程序自动驱动 (UI) 。 这些测试涵盖 UI 控件（如按钮和菜单）以验证它们是否正常工作。 如果在 UI（例如网页）中执行验证或其他逻辑，此类测试特别有用。 还可使用编码的 UI 测试自动执行手动测试。 为应用程序创建编码的 UI SharePoint与为其他类型的应用程序创建测试的方式相同。 有关详细信息，请参阅[使用编码的 UI SharePoint测试 2010 应用程序](/previous-versions/visualstudio/visual-studio-2015/test/testing-sharepoint-2010-applications-with-coded-ui-tests?preserve-view=true&view=vs-2015)。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[演练：分析SharePoint应用程序](../sharepoint/walkthrough-profiling-a-sharepoint-application.md)|演示如何对应用程序执行采样SharePoint分析。|
|[发布前对应用进行性能测试](/azure/devops/test/load-test/run-performance-tests-app-before-release?view=vsts&preserve-view=true)|介绍如何创建负载测试，这有助于对应用程序SharePoint压力。|
|[对代码进行单元测试](../test/unit-test-your-code.md)|介绍如何使用单元测试在代码中查找逻辑错误。|
|[使用编码的 UI 测试来测试 SharePoint 2010 应用程序](/previous-versions/visualstudio/visual-studio-2015/test/testing-sharepoint-2010-applications-with-coded-ui-tests?preserve-view=true&view=vs-2015)|介绍如何测试应用程序应用程序的用户界面SharePoint。|

## <a name="see-also"></a>另请参阅

- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [提高代码质量](../test/improve-code-quality.md)