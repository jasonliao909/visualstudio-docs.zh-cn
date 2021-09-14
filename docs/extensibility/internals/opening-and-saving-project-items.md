---
title: 打开和保存Project项|Microsoft Docs
description: 了解在 IDE 中打开和保存新项目类型的Visual Studio方法。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], file persistence
- files [Visual Studio], opening and saving
- editors [Visual Studio SDK], file persistence
ms.assetid: f71898ad-335f-4c43-a177-4da87078afd1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 934ce1f393d7276d0eeffd66515b8c7a874c9fd9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664356"
---
# <a name="opening-and-saving-project-items"></a>打开和保存项目项
添加新项目类型时，必须在 IDE (集成开发环境中管理项目的打开 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 和) 。 以下主题讨论打开和保存文件的不同方法。

## <a name="in-this-section"></a>本节内容
- [使用“打开文件”命令显示文件](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)

 提供有关 IDE 如何处理"打开文件"命令以及项目在响应此命令中的角色的分步说明。

- [使用“通过命令打开”显示文件](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)

 提供有关 IDE 如何处理 **Open With** 命令的详细分步说明，提示打开具有某些选择的标准编辑器的文件。

- [如何：打开项目特定的编辑器](../../extensibility/how-to-open-project-specific-editors.md)

 提供分步说明，用于指定应该使用特定于项目的编辑器打开项目中特定类型的文件。

- [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)

 提供用于指定如何启用 IDE 以打开项目类型中文件的标准编辑器的分步说明。

- [如何：打开开放文档的编辑器](../../extensibility/how-to-open-editors-for-open-documents.md)

 提供分步说明，为打开的文件打开特定于项目的编辑器。

- [保存标准文档](../../extensibility/internals/saving-a-standard-document.md)

 详细说明 IDE 如何处理在标准编辑器中打开的文档的"保存"、"另存为"和"全部保存"命令。 

- [保存自定义文档](../../extensibility/internals/saving-a-custom-document.md)

 提供有关 IDE 如何处理在自定义编辑器中打开的文档的 **"** 保存"、"另存为"和"全部保存"命令的关系图和详细说明。 

- [确定使用哪个编辑器打开项目中的文件](../../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)

 讨论 IDE 为文件选择适当的编辑器或设计器所遵循的过程。

## <a name="related-sections"></a>相关章节
- [创建自定义编辑器和设计器](../../extensibility/creating-custom-editors-and-designers.md)

 列出 IDE 可以托管的四种类型的编辑器，并给出每个编辑器的说明。

- [项目类型](../../extensibility/internals/project-types.md)

 讨论项目如何控制代码的编译和生成方式、编辑器的打开方式以及项目项的格式设置。
