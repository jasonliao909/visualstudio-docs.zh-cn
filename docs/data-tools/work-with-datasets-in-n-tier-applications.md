---
title: 在 n 层应用程序中使用数据集
description: 了解如何在 n 层应用程序中使用数据集。 N 层数据应用程序是以数据为中心的应用，分为多个逻辑层（或层）。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- datasets [Visual Basic], n-tier applications
- multi-tier database applications
- DataSet project [VS n-tier applications]
- distributed applications [VS n-tier applications]
- data [Visual Basic], n-tier applications
- TableAdapters, n-tier applications
- n-tier applications
- tiers, n-tier applications
- typed datasets, n-tier applications
- multiple tier applications
ms.assetid: f6ae2ee0-ea5f-4a79-8f4b-e21c115afb20
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 1b3873b3348c78462943204b02f570a5510e927f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601048"
---
# <a name="work-with-datasets-in-n-tier-applications"></a>在 n 层应用程序中使用数据集

“N 层数据应用程序”是以数据为中心且分为多个逻辑层（或“多层”）的应用程序 。 换句话说，N 层数据应用程序是分离到多个项目中的应用程序，数据访问层、业务逻辑层和表示层都在各自的项目中。 请参阅 [n 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)，了解更多相关信息。

类型化数据集经过改进，现在可以在相互独立的项目中生成 TableAdapter 和数据集类。 这使你可以快速分离各应用程序层及生成 N 层数据应用程序。

类型化数据集对 N 层的支持，使应用程序体系结构的迭代开发可以采取 N 层设计。同时，还无需手动将代码分离到多个项目中。 设计数据层从使用数据集设计器开始。 如果已准备好对应用程序体系结构采用 n 层设计，请设置数据集的“数据集项目”属性，以在另一个项目中生成数据集类。

## <a name="reference"></a>参考

- <xref:System.Data.DataSet>
- <xref:System.Data.TypedTableBase%601>

## <a name="see-also"></a>请参阅

- [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)
- [演练：创建 n 层数据应用程序](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [向 n 层应用程序中的 TableAdapter 添加代码](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)
- [向 n 层应用程序中的数据集添加代码](../data-tools/add-code-to-datasets-in-n-tier-applications.md)
- [向 n 层数据集添加验证](../data-tools/add-validation-to-an-n-tier-dataset.md)
- [将数据集和 TableAdapter 分离到不同的项目中](../data-tools/separate-datasets-and-tableadapters-into-different-projects.md)
- [分层更新](../data-tools/hierarchical-update.md)
- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
- [创建和配置 TableAdapter](../data-tools/create-and-configure-tableadapters.md)
- [使用 LINQ to SQL 的 n 层和远程应用程序](/dotnet/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql)
