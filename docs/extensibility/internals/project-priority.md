---
title: Project优先级 |Microsoft Docs
description: 了解 Visual Studio IDE 使用的优先级方案，如果项是多个项目的成员，则确定用于打开该项的最佳项目。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- projects [Visual Studio SDK], opening items
ms.assetid: 9f707592-2fb6-4f75-9269-f6d4700a998e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 9a6b804836daffbd0520ed83fd9d1f6d1fa9b566
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122049709"
---
# <a name="project-priority"></a>项目优先级
项目项通常是解决方案中的一个项目的成员。 因此，IDE 可以轻松确定用于打开项的项目。 但是，如果项是多个项目的成员，则 IDE 将使用优先级方案来确定用于打开该项的最佳项目。

 下面的列表显示项目优先级方案：

- IDE 为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2.IsDocumentInProject%2A> 解决方案中的每个项目调用方法，以确定该文档是否为该项目的成员。

- 如果文档是项目的成员，则该项目将根据其对该文档的处理分配的优先级进行响应。 例如，语言项目对其语言源文件做出高优先级的响应，但对无法识别的文件类型（不会在生成过程中使用）的优先级进行响应。

- 为文档提供自定义的特定于项目的编辑器或设计器的项目也具有高优先级。

- <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>枚举提供文档优先级值。

- 指定最高优先级的项目将被赋予上下文来打开文档。 如果两个项目返回相同的优先级值，则首选活动项目。 如果解决方案中没有项目响应它可以打开文档，IDE 会将文档放入 "杂项文件" 项目。 有关详细信息，请参阅[杂项文件 Project](../../extensibility/internals/miscellaneous-files-project.md)。

## <a name="see-also"></a>请参阅
- [杂项文件项目](../../extensibility/internals/miscellaneous-files-project.md)
- [如何：打开开放文档的编辑器](../../extensibility/how-to-open-editors-for-open-documents.md)
- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
