---
title: 提供 Code 自动化|Microsoft Docs
description: 了解如何实现代码模型，这需要实现由内部数据结构确定的接口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CodeModel object
ms.assetid: 21cb3e63-f25c-404b-bc1d-a32ad0fdd4d5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6d81843ebe6782f1f65acb64c0816f94e958ae82343f3d55efb4dbd8094e9625
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121275354"
---
# <a name="providing-automation-for-code"></a>提供适用于 Code 的自动化
无需为代码创建自动化模型。 环境 SDK 不提供执行此操作的示例。 有关代码模型的见解，请参阅 <xref:EnvDTE.CodeModel> 对象。

 若要实现代码模型，必须实现由内部数据结构确定的任何接口。 对象必须派生自 `IDispatch` 类。

 扩展的对象 和 可从 对象获得， <xref:EnvDTE.CodeModel> <xref:EnvDTE.FileCodeModel> <xref:EnvDTE.Project> 如下所示：

- <xref:EnvDTE.Project.CodeModel%2A>

- <xref:EnvDTE.ProjectItem.FileCodeModel%2A>

 可以选择在从 和 对象返回的 对象中仅实现 `CodeModel` `FileCodeModel` 或 `Project` <xref:EnvDTE.ProjectItem> 接口。 提供此接口中适用于项目系统的任何功能。

 如果要添加标准和接口中不可用的功能（如方法或属性），请创建从标准继承 `CodeModel` `FileCodeModel` 的自己的接口。 请务必将该文件记录到项目系统中，以便最终用户知道要查找它。 返回标准接口，但用户可以调用 方法，或强制转换到接口（如果 `QueryInterface` 已知存在）。

## <a name="see-also"></a>另请参阅
- [自动化模型概述](../../extensibility/internals/automation-model-overview.md)
