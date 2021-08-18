---
title: 旧版语言服务中的自动格式设置|Microsoft Docs
description: 了解旧版语言服务中的自动格式设置，在开始键入已知代码构造时自动插入代码片段。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, automatic formatting
ms.assetid: c210fc94-77bd-4694-b312-045087d8a549
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 1d5e824c96860030f0299fe6e1178515b7d1693d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122124797"
---
# <a name="automatic-formatting-in-a-legacy-language-service"></a>旧版语言服务中的自动格式设置
使用自动格式设置时，当用户开始键入已知代码构造时，语言服务会自动插入代码片段。

## <a name="automatic-formatting-behavior"></a>自动格式设置行为
 例如，如果键入 ，则语言服务会自动插入匹配的大括号，或者如果按 ENTER 键，则语言服务会强制将新行上的插入点强制到适当的缩进级别，具体取决于前一行是否打开了新范围。

 用于语言服务其余部分的命令筛选器还可用于自动格式设置。 还可通过调用 突出显示匹配的大括号 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A> 。

## <a name="see-also"></a>请参阅
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
