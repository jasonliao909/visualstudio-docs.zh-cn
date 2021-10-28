---
title: 获取架构集的概述
description: XML 架构设计器：了解如何使用 XML 架构资源管理器中的图形视图来查看架构集中节点的简要视图以及节点间的关系。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: c0df4b0d-52ef-4a6c-9676-1d8311aad7c7
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-xml-tools
ms.workload:
- multiple
ms.openlocfilehash: 1461653dff8e757ec462a3d47eb76ba7ed4f0ed5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736805"
---
# <a name="how-to-get-an-overview-of-a-schema-set-by-using-the-graph-view"></a>操作说明：使用图形视图获取架构集概览

本主题介绍如何使用[图形视图](../xml-tools/graph-view.md)来查看架构集中节点的简要视图以及节点间的关系。

## <a name="to-create-a-new-xsd-file-and-display-the-root-element-in-the-content-model-view"></a>创建新的 XSD 文件并显示内容模型视图中的根元素

1. 创建新的 XML 架构文件并将文件保存为 Relationships.xsd。

2. 单击起始视图上的“使用 XML 编辑器查看和编辑基础 XML 架构文件”链接。

3. 从[示例 XML 架构：关系](../xml-tools/sample-xsd-file-relationships.md)复制并粘贴 XML 架构示例代码，以替换默认情况下添加到新 XSD 文件的代码。

4. 在 XML 编辑器中的任何位置单击右键，并选择“视图设计器”。

5. 从“XSD 工具栏”选择图形视图。

6. 在“XML 架构资源管理器”中选择“架构集”节点，并将该节点拖到图形视图的设计图面上 。 您应当会看到所有全局节点，以及连接有关系节点的箭头。

     ![图形视图](../xml-tools/media/relationshipingraphview.gif)

7. 单击设计图面上的任何节点并查看痕迹栏，以了解所选节点在架构集中的位置。

8. 右键单击设计图面上的任何元素节点，并选择“生成示例 XML”以查看 XML 实例文档。
