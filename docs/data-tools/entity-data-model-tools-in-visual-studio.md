---
title: 实体框架工具
description: 了解 Visual Studio 中的 Entity Framework Tools。 Entity Framework Tools 旨在帮助你生成实体框架 (EF) 应用程序。
ms.custom: SEO-VS-2020
ms.date: 11/01/2021
ms.topic: conceptual
ms.assetid: 1b06b573-84aa-4458-b3f5-e238df47bf45
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: c7b9d4fceff3b4063856fe7df88bf816fdfb70bf
ms.sourcegitcommit: 7a820b7698a8dcf076eb36e3d766fb0751f56bb1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2021
ms.locfileid: "131126488"
---
# <a name="entity-framework-tools-in-visual-studio"></a>Visual Studio 中的 Entity Framework Tools

实体框架是一种对象关系映射技术，可方便 .NET 开发人员使用域特定对象处理关系数据。 开发人员无需再像往常一样编写大部分数据访问代码。 对于新的 .NET 应用程序，实体框架是推荐的对象关系映射 (ORM) 建模技术。

Entity Framework Tools 旨在帮助你生成实体框架 (EF) 应用程序。 实体框架的完整文档位于此处：[概述 - EF 6](/ef/ef6/)。

  > [!NOTE]
  > 本页中所述的 Entity Framework Tools 用于生成 .edmx 文件，这些文件在 EF Core 中不受支持。 若要从现有数据库生成 EF Core 模型，请参阅[反向工程 - EF Core](/ef/core/managing-schemas/scaffolding)。 有关 EF 6 与 EF Core 之间的差异的详细信息，请参阅[比较 EF 6 和 EF Core](/ef/efcore-and-ef6/)。

通过 Entity Framework Tools，可以从现有数据库创建概念模型，然后以图形方式直观显示和编辑概念模型。 或者，您可以首先以图形方式创建概念模型，然后生成支持模型的数据库。 无论哪种情况，你都可以在基础数据库更改时自动更新模型，并为应用程序生成对象层代码。 数据库生成和对象层代码生成是可自定义的。

Entity Framework Tools 在 Visual Studio 安装程序中作为数据存储和处理工作负载的一部分安装。 还可以将其作为“SDK、库和框架”类别下的单个组件进行安装。

这些是在 Visual Studio 中组成 Entity Framework Tools 的特定工具：

- 使用 [!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)] [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] 设计器（实体设计器）可以直观地创建和修改实体、关联、映射和继承关系。 实体设计器还可生成 [!INCLUDE[TLA#tla_cshrp](../data-tools/includes/tlasharptla_cshrp_md.md)] 或 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 对象层代码。

- 你可以使用 [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] 向导从现有数据库生成概念模型并将数据库连接信息添加到应用程序。

- 使用创建数据库向导可以首先创建概念模型，然后创建支持该模型的数据库。

- 你可以使用模型更新向导在对基础数据库进行更改后更新概念模型、存储模型以及映射。

  > [!NOTE]
  > 从 Visual Studio 2010 开始，Entity Framework Tools 不支持 [!INCLUDE[ss2k](../data-tools/includes/ss2k_md.md)]。

这些工具可生成或修改 .edmx 文件。 此 .edmx 文件包含描述概念模型、存储模型以及这两种模型之间的映射的信息。 有关详细信息，请参阅[EDMX](/ef/ef6/)。

[Entity Framework 6 Power Tools](https://marketplace.visualstudio.com/items?itemName=EntityFrameworkTeam.EntityFrameworkPowerToolsBeta4) 可帮助生成使用实体数据模型的应用程序。 Power Tools 可以生成概念模型、验证现有模型、生成包含基于概念模型的对象类的源代码文件以及生成包含模型生成的视图的源代码文件。 有关详细信息，请参阅[预生成的映射视图](/ef/ef6/fundamentals/performance/pre-generated-views)。

## <a name="related-topics"></a>相关主题

| Title | 说明 |
| - | - |
| [ADO.NET 实体框架](/dotnet/framework/data/adonet/ef/index) | 描述如何使用 [!INCLUDE[adonet_ef](../data-tools/includes/adonet_ef_md.md)] 提供的 [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] 工具创建应用程序。 |
| [实体数据模型](/dotnet/framework/data/adonet/entity-data-model) | 提供用于处理数据的链接和信息，这些数据供在 [!INCLUDE[adonet_ef](../data-tools/includes/adonet_ef_md.md)] 上构建的应用程序使用。 |
| [实体框架 (EF) 文档](/ef/ef6/get-started) | 提供视频、教程和高级文档的索引，以充分利用实体框架。 |

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
