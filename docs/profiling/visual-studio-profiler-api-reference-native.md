---
title: Visual Studio 探查器 API 参考（本机）
description: 了解如何通过 Visual Studio 探查器 API 以编程方式控制收集的数据量，并在分析期间插入时间戳和分析标记。
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- performance tools, API
- Profiler, API
ms.assetid: a0c3be92-c263-4678-9fb9-bafead3bd5f5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- cplusplus
ms.openlocfilehash: edcc3bb968504d63b18adad2217f23c5a8bb5889
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129973033"
---
# <a name="visual-studio-profiler-api-reference-native"></a>Visual Studio 探查器 API 参考（本机）
Visual Studio 探查器 API 允许你以编程方式控制收集的数据量，并在分析期间插入时间戳和分析标记。 若要使用本机 API，请包含 VSPerf.h 头文件，并在项目中添加 VSPerf.lib。

> [!NOTE]
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。

## <a name="in-this-section"></a>本节内容
[CommentMarkAtProfile](../profiling/commentmarkatprofile.md)

[CommentMarkProfile](../profiling/commentmarkprofile.md)

[MarkProfile](../profiling/markprofile.md)

[NameProfile](../profiling/nameprofile.md)

[ResumeProfile](../profiling/resumeprofile.md)

[StartProfile](../profiling/startprofile.md)

[StopProfile](../profiling/stopprofile.md)

[SuspendProfile](../profiling/suspendprofile.md)

[PROFILE_CURRENTID](../profiling/profile-currentid.md)

## <a name="see-also"></a>另请参阅

- [分析工具 API](../profiling/profiling-tools-apis.md)
- [演练：使用探查器 API](../profiling/walkthrough-using-profiler-apis.md)
