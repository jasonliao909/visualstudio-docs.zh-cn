---
title: 使用帮助查看器目录
description: 使用 Microsoft Help Viewer 在目录 (TOC) 中查找主题。 TOC 是可展开的列表，其中包含已安装丛书中的所有主题。
ms.date: 11/02/2017
ms.topic: how-to
f1_keywords:
- hv_contents
helpviewer_keywords:
- Help Viewer, table of contents filtering
- Help Viewer, Contents tab
- Contents tab [Help Viewer]
- table of contents filtering [Help Viewer]
ms.assetid: 8b98464d-2b05-4710-ad68-5647e78c6b7b
author: jasonchlus
ms.author: jasonchlus
manager: jmartens
ms.technology: vs-help-viewer
ms.workload:
- multiple
ms.openlocfilehash: 87f7e473756353758c6faed9f96213bf0f33988e
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139552546"
---
# 如何：在目录中查找主题

在“目录”选项卡中，可以使用目录 (TOC) 查找信息。 目录是可展开的列表，其中包含已安装丛书中的所有主题。 有关如何浏览 TOC 的辅助功能信息，请参阅[快捷键 (Help Viewer)](../help-viewer/shortcut-keys.md)。

> [!IMPORTANT]
> TOC 中的可用主题范围取决于所选择的筛选器。

## 筛选 TOC

可以筛选 TOC 来缩小“内容”选项卡中显示的主题范围。只有当标题包含所指定的术语根时才会在列表中显示。 例如，如果将“疑难解答”指定为筛选器，则只会显示包含“排除故障”或“疑难解答”的标题。 其标题不包含术语的节点会折叠为带省略号 (...) 的单个节点。

1. 选择“目录”选项卡。

2. 在“筛选目录”文本框中，输入一个词。

> [!NOTE]
> 如果筛选器运行很长时间，可以使用 `title:` 高级搜索运算符更快显示结果。

## 将主题与 TOC 同步

如果你已使用索引或全文搜索功能打开了一个主题，则可以通过将 TOC 与主题窗口同步确定该主题在 TOC 中的位置。

1. 查看主题。

2. 单击工具栏上的“在目录中显示主题”按钮，或按 Ctrl+S  。

     “目录”选项卡将打开并显示 TOC 中的主题位置。

## 另请参阅

- [如何：在索引中查找主题](../help-viewer/find-topics-index.md)
- [如何：搜索主题](../help-viewer/find-topics.md)
- [Microsoft Help Viewer](../help-viewer/overview.md)