---
title: 源代码管理设计决策|Microsoft Docs
description: 了解实现源代码管理时要考虑的项目的几个关键设计决策。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], design decisions
ms.assetid: 5f60ec1a-5a74-4362-8293-817a4dd73872
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 79cbc22b16835e0f6c3fa9caa41ac9720c7022d8786520b1baf89d33c3b64948
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121275172"
---
# <a name="source-control-design-decisions"></a>源代码管理设计决策
实现源代码管理时，应针对项目考虑以下设计决策。

## <a name="will-information-be-shared-or-private"></a>信息是共享信息还是私有信息？
 可以做出最重要的设计决策是可共享的信息和私有信息。 例如，项目的文件列表是共享的，但在此文件列表中，某些用户可能希望具有私有文件。 编译器设置是共享的，但启动项目通常是私有的。 设置是纯共享、与重写共享或纯专用。 根据设计，私有项（如解决方案用户选项 (.suo) 文件）不会签入 [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] 。 请确保将任何私有信息存储在专用文件中，例如 .suo 文件或你创建的特定专用文件，例如 Visual C# 的 .csproj.user 文件或 Visual Basic 的 .vbproj.user 文件。

 此决策并非包含所有内容，可以按项做出。

## <a name="will-the-project-include-special-files"></a>项目是否包含特殊文件？
 另一个重要的设计决策是项目结构是否使用特殊文件。 特殊文件是隐藏文件，它们基于在解决方案资源管理器和签入和签出对话框中可见的文件。 如果使用特殊文件，请遵循以下准则：

1. 不要将特殊文件与项目根节点（即项目文件本身）关联。 项目文件必须是单个文件。

2. 在项目中添加、删除或重命名特殊文件时，必须使用标志集触发相应的事件，该标志集指示 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> 这些文件是特殊文件。 这些事件由环境调用，以响应调用相应方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> 的项目。

3. 当项目或编辑器调用文件时，不会自动签出与该文件关联的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 特殊文件。将特殊文件与父文件一起传递。 环境将检测传入的所有文件之间的关系，并适当隐藏签出 UI 中的特殊文件。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
