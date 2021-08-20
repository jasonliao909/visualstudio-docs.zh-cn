---
title: Project上下文 |Microsoft Docs
description: 了解 Visual Studio IDE 如何使用项目上下文来确定用户添加或处理项目和项目项时如何执行操作。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- projects [Visual Studio SDK], opening items
ms.assetid: d1803f4a-24eb-44b0-b5d2-cb40c15534be
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: d4d789a597682ad881dd64f4a12580cd10b6e766
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122117847"
---
# <a name="project-context"></a>项目上下文
当用户添加或使用项目和项目项时，IDE 将使用项目上下文的概念来确定应如何执行不同的操作。

 通常，文件是用户通过选择 "**新建 Project** " 命令，或通过选择 "**文件**" 菜单上的 "**打开 Project** " 命令来显式创建的标准项目对象。 在这些情况下，将在项目的上下文中创建并打开文件，并且项目类型定义用于编辑文档的上下文。

 某些项目提供了非常丰富的上下文。 例如，项目为数据绑定管理项目范围、编程命名空间或项目范围的数据库连接。 用户可以使用特定的项目对象（例如解决方案资源管理器中显示的项目项），频繁地打开文件或数据库连接。

 在其他情况下，不显式指定项的项目上下文。 例如，当用户通过在 "**文件**" 菜单上选择 "**打开现有文件**" 命令、调试器对文件进行操作或用户在 "**查找和替换**" 对话框中单击 "**在文件中查找**" 命令打开文件时，项的上下文不可用。 为了处理这些情况，IDE 将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument> 以管理用于打开文档的最佳项目的过程。

## <a name="see-also"></a>请参阅
- [项目优先级](../../extensibility/internals/project-priority.md)
- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
