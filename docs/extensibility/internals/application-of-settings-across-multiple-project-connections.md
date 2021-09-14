---
title: 跨多个项目连接应用设置
description: 了解如何通过使用源代码管理插件执行批处理操作，跨多个项目连接应用设置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, application of settings
ms.assetid: 2116d3d0-c46c-4d0a-b482-08a178584f46
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 21c1486855dba6906937f95f10cae2f323ff0383
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665338"
---
# <a name="application-of-settings-across-multiple-project-connections"></a>跨多个项目连接应用设置
使用源代码管理插件 API 版本 1.2 构建的源代码管理插件可以使用批处理操作跨多个项目或多个连接上下文执行相同的源代码管理操作。 批处理可用于消除用户体验中每个项目的冗余对话框。

 例如，如果用户在使用源代码管理插件 API 版本 1.1 (构建的源代码管理插件中选择属于多个连接的多个项，则不同文件共享计算机上有两个 Web 项目) 并检查它们，则用户将反复看到同一对话框。 即使用户单击对话框中的"全部应用"复选框，也会出现此情况，因为 IDE 会重置每个连接上下文的状态。

## <a name="new-capability-flag"></a>新功能标志
 `SccBeginBatch`函数设置 `SCC_CAP_BATCH` 标志以指示批处理操作正在进行。

## <a name="new-functions"></a>新函数
以下新函数支持批处理操作：

- [SccBeginBatch](../../extensibility/sccbeginbatch-function.md)

- [SccEndBatch](../../extensibility/sccendbatch-function.md)

`SCCBeginBatch`函数启动一组源代码管理操作。 `SccEndBatch`函数关闭组。 组不能嵌套。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
