---
title: 持久性和正在运行的文档表|Microsoft Docs
description: 了解项目如何在正在运行的文档表中协调文档打开、保存和重命名，该表跟踪 IDE 中的文档Visual Studio状态。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, managing
- IVsPersistHierarchyItem interface, implementing
- architecture, persistence
- running document table (RDT), architecture
ms.assetid: 27117eae-6c58-4189-a61a-1397a43b5ecf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 1c4b37e5ae834a614cb741cb7589dad9dd1d6677
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122063117"
---
# <a name="persistence-and-the-running-document-table"></a>持久性和正在运行的文档表
在 IDE 中，项目完全负责管理其项目项的持久性，这些项目项是使用服务 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 完成的 <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> 。 文档是数据环境中的基本Visual Studio单元。 项目使用正在运行的文档表 (RDT) （跟踪所有打开的文档的状态的资源）协调文档的打开、保存和重命名。

## <a name="managing-persistence"></a>管理持久性
 项目通过实现 接口来控制环境的持久性 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem> 服务。 虽然环境永远不会直接要求文档自行保存，但它要求拥有的项目 (层次结构) 保存文档。 这使项目能够将其项目项数据保存到本地文件、远程文件、数据库、存储库或其他介质中。

 全局环境维护 RDT。 环境维护 RDT 中所有打开的窗口和文档的条目，这使它们能够接收特殊通知，例如解决方案关闭时。 此外，RDT 使环境能够跟踪中其 **解决方案资源管理器。** RDT 维护每个打开的可持久化对象（包括项目文件和项目项文档）的一条记录。

## <a name="see-also"></a>请参阅
- [运行文档表](../../extensibility/internals/running-document-table.md)
- [IDE 中的选择和货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)
