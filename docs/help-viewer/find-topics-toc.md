---
title: 使用帮助查看器目录
description: 使用 Microsoft Help Viewer 在目录查找主题 (TOC) 。 TOC 是一个可展开列表，其中包含已安装书籍中的所有主题。
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
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-help-viewer
ms.workload:
- multiple
ms.openlocfilehash: ae8303c42b3bb281b87aba94f66725725ba0c26c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122124329"
---
# 如何：在目录中查找主题

在“目录”选项卡中，可以使用目录 (TOC) 查找信息。 目录是可展开的列表，其中包含已安装丛书中的所有主题。 有关如何浏览 TOC 的辅助功能信息，请参阅[快捷键 (Help Viewer)](../help-viewer/shortcut-keys.md)。

> [!IMPORTANT]
> TOC 中的可用主题范围取决于所选择的筛选器。

## 筛选 TOC

可以筛选 TOC 以缩小"内容"选项卡中显示 **的主题** 范围。只有在标题包含你指定的术语的根时，标题才显示在列表中。 例如，如果将“疑难解答”指定为筛选器，则只会显示包含“排除故障”或“疑难解答”的标题。 标题不包含该术语的节点将折叠为包含省略号的单个节点 (**...) 。**

1. 选择“目录”选项卡。

2. 在“筛选目录”文本框中，输入一个词。

> [!NOTE]
> 如果筛选器运行很长时间，可以使用 `title:` 高级搜索运算符更快显示结果。

## 将主题与 TOC 同步

如果你已使用索引或全文搜索功能打开了一个主题，则可以通过将 TOC 与主题窗口同步确定该主题在 TOC 中的位置。

1. 查看主题。

2. 单击工具栏 **上的"在内容中** 显示主题"按钮，或按 **Ctrl** + **S**。

     “目录”选项卡将打开并显示 TOC 中的主题位置。

## 请参阅

- [如何：查找索引中的主题](../help-viewer/find-topics-index.md)
- [如何：搜索主题](../help-viewer/find-topics.md)
- [Microsoft Help Viewer](../help-viewer/overview.md)