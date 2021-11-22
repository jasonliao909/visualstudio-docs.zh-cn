---
title: 分析 SharePoint 应用程序的性能 | Microsoft Docs
description: 如果应用程序运行缓慢或效率低下，则分析 SharePoint 应用程序的性能。 使用 Visual Studio 分析功能查找存在问题的代码。
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
# <a name="profile-the-performance-of-sharepoint-applications"></a>分析 SharePoint 应用程序的性能

如果 SharePoint 应用程序运行缓慢或效率低下，可以使用 Visual Studio 中的分析功能来识别存在问题的代码和其他元素。 通过使用负载测试功能，可以确定 SharePoint 应用程序在压力下的性能情况，例如在许多用户同时访问应用程序时。 通过运行 Web 性能测试，可以度量应用程序在 Web 上性能情况。 通过使用编码的 UI 测试，可以验证整个 SharePoint 应用程序（包括其用户界面）是否正常工作。 将这些测试一起使用时，它们可以帮助你在部署应用程序之前识别性能问题。

## <a name="profile-tools-overview"></a>分析工具概述

分析是指在应用程序运行时观察和记录应用程序的性能行为的过程。 通过对应用程序进行分析，可以发现瓶颈、低效代码和内存分配问题等问题，这些问题会导致应用程序运行缓慢或使用过多内存。 例如，可以使用分析来识别代码中的热点，这些热点是经常调用的代码段，可能会降低应用程序的整体性能。 识别热点后，可以经常优化或消除它们。

可以在集成开发环境中 (IDE) 使用多个分析工具来识别和查找此类性能问题。 对于 SharePoint 项目和其他 Visual Studio 项目，这些工具的工作方式相同。 分析工具性能向导可以引导你创建使用指定的测试的性能会话。 性能会话是一组配置数据，用于从应用程序收集性能信息，以及一个或多个分析运行的结果。 性能会话存储在项目文件夹中，你可以在“性能资源管理器”中查看它们。 有关详细信息，请参阅[了解性能收集方法](../profiling/understanding-performance-collection-methods.md)。

在应用程序中创建并运行配置文件分析后，报表会提供有关其性能的详细信息。 该报表可以包含一些项，例如一段时间的 CPU 使用情况图、分层函数调用堆栈或调用树。 报表的确切内容可能会有所不同，具体取决于运行的测试类型，例如采样或检测。 有关详细信息，请参阅[分析工具报告视图](../profiling/performance-report-overview.md)。

## <a name="performance-session-process"></a>性能会话进程

若要对应用程序进行分析，首先从使用“分析工具性能向导”创建性能会话开始。 在菜单栏上，依次选择“分析”和“启动性能向导” 。 完成向导后，请输入性能会话的所需信息，例如所需的分析方法和要分析的应用程序。 有关详细信息，请参阅[如何：使用性能向导分析网站或 Web 应用程序](../profiling/how-to-collect-performance-data-for-a-web-site.md)。 或者，可以使用命令行选项来设置和运行性能会话。 有关更多详细信息，请参阅[通过命令行使用分析工具](../profiling/using-the-profiling-tools-from-the-command-line.md)。 若要手动配置性能会话的各个方面，请参阅[如何：通过分析工具手动创建性能会话](../profiling/how-to-manually-create-performance-sessions.md)。 还可以通过在“测试结果”窗口中打开单元测试的快捷菜单，然后选择“创建性能会话”来从单元测试创建性能会话。

设置性能会话后，会保存会话配置，将服务器配置为提供分析数据，并运行应用程序。 使用应用程序时，性能数据将写入日志文件。 性能会话列在“目标”文件夹下的“性能资源管理器”中 。 性能会话完成后，其报表将显示在“性能资源管理器”的“报表”文件夹中。  若要显示报表，请在“性能资源管理器”中将其打开。 若要查看或配置性能会话的属性，请在“性能资源管理器”中打开其快捷菜单，然后选择“属性”。  有关性能会话的特定属性的详细信息，请参阅[为分析工具配置性能会话](../profiling/configuring-performance-sessions.md)。 有关如何解释性能会话的结果的信息，请参阅[分析分析工具数据](../profiling/analyzing-performance-tools-data.md)。

## <a name="stress-test"></a>压力测试

可以通过在 Visual Studio 中创建负载测试和 Web 性能测试来分析应用程序的压力性能。 在 Visual Studio 中创建负载测试时，指定要针对应用程序测试的因素组合（称为方案）。 这些因素包括负载模式、测试组合模型、测试组合、网络组合和 Web 浏览器组合。 负载测试方案可以包括单元测试和 Web 性能测试。

图 1：负载测试结果示例

![运行负载测试图形视图](../sharepoint/media/load-webgraphs.png "运行负载测试图形视图")

Web 性能测试模拟最终用户与 SharePoint 应用程序的交互方式。 可以通过在浏览器会话中记录 HTTP 请求或使用 Web 性能测试记录器来创建 Web 性能测试。 浏览器会话完成后，web 结果将显示在 Web 性能测试编辑器中。 然后，可以在 Web 性能测试结果查看器中调试结果。 此外，还可以使用 Web 性能测试编辑器手动生成 Web 性能结果。

## <a name="test-user-interfaces"></a>测试用户界面

编码的 UI 测试通过其用户界面 (UI) 自动驱动 SharePoint 应用程序。 这些测试涵盖 UI 控件（如按钮和菜单），以验证它们是否正常工作。 在 UI（例如网页）中执行验证或其他逻辑时，此类测试特别有用。 还可以使用编码的 UI 测试来自动执行手动测试。 为 SharePoint 应用程序创建编码的 UI 测试的方式与为其他类型的应用程序创建测试的方式相同。 有关更多信息，请参阅[使用编码的 UI 测试来测试 SharePoint 2010 应用程序](/previous-versions/visualstudio/visual-studio-2015/test/testing-sharepoint-2010-applications-with-coded-ui-tests?preserve-view=true&view=vs-2015)。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[演练：分析 SharePoint 应用程序](../sharepoint/walkthrough-profiling-a-sharepoint-application.md)|演示如何在 SharePoint 应用程序上执行采样分析。|
|[发布前对应用进行性能测试](/azure/devops/test/load-test/run-performance-tests-app-before-release?view=vsts&preserve-view=true)|介绍如何创建负载测试，这有助于对 SharePoint 应用程序进行压力测试。|
|[单元测试代码](../test/unit-test-your-code.md)|介绍如何使用单元测试在代码中查找逻辑错误。|
|[使用编码的 UI 测试来测试 SharePoint 2010 应用程序](/previous-versions/visualstudio/visual-studio-2015/test/testing-sharepoint-2010-applications-with-coded-ui-tests?preserve-view=true&view=vs-2015)|介绍如何测试 SharePoint 应用程序的用户界面。|

## <a name="see-also"></a>另请参阅

- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [提高代码质量](../test/improve-code-quality.md)