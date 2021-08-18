---
title: 管理Project解决方案中的加载|Microsoft Docs
description: 了解开发人员如何通过创建解决方案负载管理器来缩短解决方案加载时间并管理项目加载行为。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, managing project loading
ms.assetid: 097c89d0-f76a-4aaf-ada9-9a778bd179a0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: eb240a99b486d7faeb481d78052e66fc6fd40024
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122102280"
---
# <a name="manage-project-loading-in-a-solution"></a>管理解决方案中的项目加载
Visual Studio解决方案可以包含大量项目。 默认Visual Studio是在解决方案打开时加载解决方案中所有项目，而不是允许用户访问任何项目，直到所有项目都完成加载。 当项目加载过程持续两分钟以上时，将显示一个进度栏，其中显示加载的项目数和项目总数。 用户可以在使用多个项目的解决方案中卸载项目，但此过程有一些缺点：卸载的项目不是作为"重新生成解决方案"命令的一部分生成，并且不显示已关闭项目的类型和成员的 IntelliSense 说明。

 开发人员可以通过创建解决方案加载管理器来缩短解决方案加载时间并管理项目加载行为。 解决方案加载管理器可以确保在启动后台生成之前加载项目，延迟后台加载，直到其他后台任务完成，并执行其他项目负载管理任务。

## <a name="create-a-solution-load-manager"></a>创建解决方案负载管理器
 开发人员可以通过实现解决方案负载管理器并Visual Studio <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager> 解决方案负载管理器处于活动状态这一建议来创建解决方案负载管理器。

### <a name="activate-a-solution-load-manager"></a>激活解决方案负载管理器
 Visual Studio一个给定时间只允许一个解决方案负载管理器，因此，Visual Studio激活解决方案负载管理器时，必须提供建议。 如果稍后激活了第二个解决方案负载管理器，则解决方案负载管理器将断开连接。

 必须获取 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> 服务并设置 [__VSPROPID4。VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>) 属性：

```csharp
IVsSolution pSolution = GetService(typeof(SVsSolution)) as IVsSolution;
object objLoadMgr = this;   //the class that implements IVsSolutionManager
pSolution.SetProperty((int)__VSPROPID4.VSPROPID_ActiveSolutionLoadManager, objLoadMgr);
```

 当正在关闭Visual Studio，或者当另一个包作为活动解决方案负载管理器接管时，会调用 方法，方法是 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager.OnDisconnect%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.SetProperty%2A> 使用[__VSPROPID4。VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>)属性。

#### <a name="strategies-for-different-kinds-of-solution-load-manager"></a>不同类型的解决方案负载管理器的策略
 可以通过不同方式实现解决方案负载管理器，具体取决于它们要管理的解决方案类型。

 如果解决方案加载管理器旨在一般情况下管理解决方案加载，则它可以作为 VSPackage 的一部分实现。 应在 VSPackage 上添加值为 的 ，将包 <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> 设置为自动加载 <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionOpening_guid> 。 然后，可以在 方法中激活解决方案负载 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 管理器。

> [!NOTE]
> 有关自动加载包的信息，请参阅[加载 VSPackage。](../extensibility/loading-vspackages.md)

 由于Visual Studio仅识别要激活的最后一个解决方案负载管理器，因此一般解决方案负载管理器应始终在激活自身之前检测是否有现有的负载管理器。 如果在 `GetProperty()` 解决方案服务上调用 [__VSPROPID4。VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>) 返回 `null` ，则没有活动的解决方案负载管理器。 如果它不返回 null，请检查对象是否与解决方案加载管理器相同。

 如果解决方案负载管理器只管理几种类型的解决方案，则 VSPackage 可以通过调用) 来订阅解决方案加载事件 (，并使用 的事件处理程序来激活解决方案负载管理器。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>

 如果解决方案负载管理器旨在仅管理特定解决方案，则可以通过调用"解决方案前"部分来将激活信息保留为解决方案 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A> 文件的一部分。

 特定解决方案负载管理器应在事件处理程序中停用自身，以便 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents.OnAfterCloseSolution%2A> 不与其他解决方案负载管理器冲突。

 如果只需使用解决方案负载管理器来持久保存全局项目加载属性 (例如，在"选项"页) 上设置的属性，可以在事件处理程序中激活解决方案加载管理器，在解决方案属性中保留设置，然后停用解决方案负载管理器。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>

## <a name="handle-solution-load-events"></a>处理解决方案加载事件
 若要订阅解决方案加载事件，在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A> 激活解决方案负载管理器时调用 。 如果实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents> ，可以响应与不同项目加载属性相关的事件。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>：在打开解决方案之前触发此事件。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeBackgroundSolutionLoadBegins%2A>：在完全加载解决方案之后，但在后台项目加载重新开始之前，将触发此事件。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterBackgroundSolutionLoadComplete%2A>：在解决方案最初完全加载后，无论解决方案负载管理器是否存在，都触发此事件。 每当解决方案完全加载时，也会在后台加载或按需加载后触发它。 同时， <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExistsAndFullyLoaded_guid> 被重新激活。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnQueryBackgroundLoadProjectBatch%2A>：在加载项目或项目之前 (此事件) 。 若要确保在加载项目之前完成其他后台进程，请设置为 `pfShouldDelayLoadToNextIdle` **true。**

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeLoadProjectBatch%2A>：当即将加载一批项目时，将触发此事件。 如果 为 true，则在后台加载项目;如果 为 false，则项目将同步加载为用户请求的结果，例如，如果用户在 解决方案资源管理器 中展开 `fIsBackgroundIdleBatch` `fIsBackgroundIdleBatch` 挂起的项目。 可以处理此事件，以执行成本高昂的工作，否则需要在 中完成 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> 。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterLoadProjectBatch%2A>：加载一批项目后，将触发此事件。

## <a name="detect-and-manage-solution-and-project-loading"></a>检测和管理解决方案和项目加载
 若要检测项目和解决方案的加载状态，请调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProperty%2A> ，并具有以下值：

- [__VSPROPID4。VSPROPID_IsSolutionFullyLoaded](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsSolutionFullyLoaded>)： `var` 如果加载解决方案及其所有项目，则返回 `true` ;否则返回 `false` 。

- [__VSPROPID4。VSPROPID_IsInBackgroundIdleLoadProjectBatch](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsInBackgroundIdleLoadProjectBatch>)：如果当前在后台加载一批项目，则返回 `var` `true` ;否则返回 `false` 。

- [__VSPROPID4。VSPROPID_IsInSyncDemandLoadProjectBatch：](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsInSyncDemandLoadProjectBatch>)如果当前由于用户命令或其他显式加载而同步加载一批项目，则返回 `var` `true` ;否则返回 `false` 。

- [__VSPROPID2。VSPROPID_IsSolutionClosing](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2.VSPROPID_IsSolutionClosing>)： `var` 如果 `true` 解决方案当前处于关闭状态，则返回 ;否则返回 `false` 。

- [__VSPROPID。VSPROPID_IsSolutionOpening](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID.VSPROPID_IsSolutionOpening>) `var` ： 如果 `true` 当前正在打开解决方案，则返回 ;否则返回 `false` 。

还可通过调用以下方法之一来确保加载项目和解决方案：

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureSolutionIsLoaded%2A>：调用此方法会强制在方法返回之前加载解决方案中的项目。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectIsLoaded%2A>：调用此方法会强制 在 方法返回 `guidProject` 之前加载 中的项目。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectsAreLoaded%2A>：调用此方法会强制 在 方法返回 `guidProjectID` 之前加载 中的项目。
