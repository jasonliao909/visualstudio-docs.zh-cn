---
title: 工作簿包含无法加载 ActiveX 控件
description: 了解如何解决当工作簿包含无法加载 ActiveX 控件时发生的错误。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: error-reference
f1_keywords:
- VST.SelectDocWizard.ContainsActiveXControls
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: e89484f9da4868ff04cbaeaa72247e39be147185
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122147721"
---
# <a name="the-workbook-contains-activex-controls-that-cannot-be-loaded"></a>工作簿包含无法加载 ActiveX 控件

  当你以编程方式将控件添加到 Word 文档或 Excel 工作表时，如果显示 "用于创建此项目的工作簿包含 ActiveX 控件"，则将显示 "该工作簿包含设计器无法加载的控件"，保存文档或工作簿，然后基于文档或工作簿创建新的文档级解决方案。

 介绍控件托管类型的信息不会随文档或工作簿一起保存。 基于该文档或工作簿创建新的解决方案时，Visual Studio 没有足够的信息来加载主机项设计器中的控件。

## <a name="to-correct-this-error"></a>更正此错误

1. 打开文档或工作簿。

2. 删除在运行时添加的控件。 为此，可以在文档或工作簿中选择它们并按 **Delete** 键。

3. 基于文档或工作簿创建文档级解决方案。

## <a name="see-also"></a>请参阅
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
