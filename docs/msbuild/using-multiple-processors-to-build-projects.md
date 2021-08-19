---
title: 使用多个处理器生成项目 | Microsoft Docs
description: 了解 MSBuild 如何通过为每个可用的处理器创建单独的生成过程来利用具有多个处理器或核心的系统。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- multiple processors
- MSBuild, multiple processor systems
ms.assetid: 49fa36c9-8e14-44f5-8a2b-34146cf6807b
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 814db4514454659780021c17e873a8e2363cb54f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122142437"
---
# <a name="use-multiple-processors-to-build-projects"></a>使用多个处理器生成项目

MSBuild 可以利用具有多个处理器或多核处理器的系统。 为每个可用处理器创建单独的生成进程。 例如，如果系统具有四个处理器，则创建四个生成进程。 MSBuild 可以同时处理这些生成，从而缩短总体生成时间。 但是，并行生成会在生成方式上引入了一些更改。 本主题将讨论这些更改。

## <a name="project-to-project-references"></a>项目到项目的引用

 如果 Microsoft 生成引擎使用并行生成来生成项目，在遇到项目到项目 (P2P) 的引用时，它将仅生成一次引用。 如果两个项目具有相同的 P2P 引用，则不会为每个项目重新生成该引用。 但是，生成引擎会将相同的 P2P 引用返回到依赖于它的两个项目。 会话中同一目标的后续请求将获得相同的 P2P 引用。

## <a name="cycle-detection"></a>循环检测

 循环检测的作用与其在 MSBuild 2.0 中的作用相同，只不过现在 MSBuild 可以报告在不同时间或在生成中的循环检测。

## <a name="errors-and-exceptions-during-parallel-builds"></a>并行生成期间的错误和异常

 在并行生成期间，错误和异常出现的时间可以与非并行生成期间的时间不同，并且如果一个项目未生成，将继续其他项目生成。 MSBuild 不会因一个项目失败而停止并行生成的任何项目生成。 其他项目将继续生成，直到最后成功或者失败。 但是，如果已启用 <xref:Microsoft.Build.Framework.IBuildEngine.ContinueOnError%2A>，则即使发生错误，也不会停止生成。

## <a name="c-project-vcxproj-and-solution-sln-files"></a>C++ 项目 (.vcproj) 和解决方案 (.sln) 文件

 可将 C++ 项目 (.vcxproj) 和解决方案 (.sln) 文件传递给 [MSBuild 任务](../msbuild/msbuild-task.md) 。 对于 C++ 项目，已调用 VCWrapperProject，然后创建了内部 MSBuild 项目。 对于 C++ 解决方案，已创建 SolutionWrapperProject，然后创建了内部 MSBuild 项目。 在这两种情况下，将生成的项目与任何其他 MSBuild 项目视为相同。

## <a name="multi-process-execution"></a>多进程执行

 几乎所有与生成相关的活动都要求当前目录在生成过程中保持不变，防止出现与路径相关的错误。 因此，项目无法在 MSBuild 中的不同线程上运行，因为它们可能会导致创建多个目录。

 为了避免此问题但仍启用多处理器生成，MSBuild 可使用“进程隔离”。 通过使用进程隔离，MSBuild 可以创建最多 `n` 个进程，其中 `n` 为系统上可用的处理器数。 例如，如果 MSBuild 在具有两个处理器的系统上生成解决方案，则仅创建两个生成进程。 重复使用这两个进程可生成解决方案中的所有项目。

## <a name="see-also"></a>另请参阅

- [并行生成多个项目](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)
- [任务](../msbuild/msbuild-tasks.md)
