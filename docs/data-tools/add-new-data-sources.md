---
title: 添加新数据源
description: 在 Visual Studio 中添加新数据源。 数据源是一个 .NET 对象，它连接到数据存储，使数据可供 .NET 应用程序使用。
ms.custom: SEO-VS-2020
ms.date: 11/21/2018
ms.topic: how-to
f1_keywords:
- vs.datasource.datasourcefieldspicker
helpviewer_keywords:
- data [Visual Studio], data sources
- data sources
ms.assetid: ed28c625-bb89-4037-bfde-cfa435d182a2
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: a0d93a2c80afe7863490f0af5578684d699a5980
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601234"
---
# <a name="add-new-data-sources"></a>添加新数据源

:::moniker range=">=vs-2019"
> [!NOTE]
> 本文中所述的功能适用于.NET Framework Windows窗体和 WPF 开发。 WPF 和 Windows 不支持 .NET Core 开发。
:::moniker-end

在 Visual Studio .NET 数据工具的上下文中，术语"数据源"是指连接到数据存储并可供 .NET 应用程序使用的数据的 .NET 对象。 在Visual Studio"数据源"窗口中拖放数据库对象时，这些设计器可以使用数据源的输出来生成将数据绑定到窗体的样 **板** 代码。 此类数据源可以是：

- 与某种实体框架关联的数据库模型中的类。

- 与某种数据库关联的数据集。

- 表示网络服务的类，如 Windows Communication Foundation (WCF) 或 REST 服务。

- 一个表示服务SharePoint类。

- 解决方案中的类或集合。

> [!NOTE]
> 如果不使用数据绑定功能、数据集、实体框架、LINQ to SQL、WCF 或 SharePoint，则"数据源"的概念不适用。 只需使用 SQLCommand 对象直接连接到数据库，并直接与数据库通信。

通过使用数据源配置向导在窗体或窗体应用程序中创建Windows编辑Windows Presentation Foundation数据源。 对于实体框架，请首先创建实体类，然后通过选择"Project添加新数据源" (本文稍后部分将更详细地介绍  >  ) 。

![数据源配置向导](../data-tools/media/data-source-configuration-wizard.png)

## <a name="data-sources-window"></a>“数据源”窗口

创建数据源后，该数据源将显示在" **数据源"** 工具窗口中。

> [!TIP]
> 若要打开 **"数据源"** 窗口，请确保项目已打开，然后按 **Shift** Alt D 或选择"查看其他Windows +  +   >    >  **数据源"。**

可以将数据源从"数据源"窗口拖动到窗体设计图面或控件上。 这将导致生成样本代码，用于显示数据存储的数据。

下图显示了一个数据集，该数据集已Windows窗体。 如果在应用程序上选择 **F5，** 则基础数据库中的数据将显示在窗体的控件中。

![数据源拖动操作](../data-tools/media/raddata-data-source-drag-operation.png)

## <a name="data-source-for-a-database-or-a-database-file"></a>数据库或数据库文件的数据源

可以创建数据集或实体框架模型，用作数据库或数据库文件的数据源。

### <a name="dataset"></a>数据集

若要将数据集创建为数据源，请通过选择"添加新数据源"Project  >  **运行数据源配置向导**。 选择 **"数据库** 数据源类型"，然后按照提示指定新的或现有的数据库连接或数据库文件。

### <a name="entity-classes"></a>实体类

若要创建实体框架模型作为数据源：

1. 运行实体数据模型 **向导** 以创建实体类。 选择  >  **Project"添加新项**  >  **ADO.NET 实体数据模型"。**

   ![新建实体框架模型项目项](../data-tools/media/raddata-new-entity-framework-model-project-item.png)

1. 选择要生成模型的方法。

   ![实体数据模型向导](../data-tools/media/raddata-entity-data-model-wizard.png)

1. 将模型添加为数据源。 选择"对象"类别时 **，** 生成的类将显示在数据源配置 **向导** 中。

   ![包含实体类的数据源配置向导](../data-tools/media/raddata-data-source-configuration-wizard-with-entity-classes.png)

## <a name="data-source-for-a-service"></a>服务的数据源

若要从服务创建数据源，请运行 **数据源配置向导并选择****"服务** 数据源类型"。 这只是"添加服务引用"对话框的快捷方式，也可以右键单击 解决方案资源管理器 并选择"添加服务引用 **"来** 访问 **该对话框**。

从服务创建数据源时，Visual Studio向项目添加服务引用。 Visual Studio还会创建与服务返回的对象相对应的代理对象。 例如，返回数据集的服务在项目中表示为数据集;返回特定类型的服务在项目中表示为返回的类型。

可以从以下类型的服务创建数据源：

- [WCF 数据服务](/dotnet/framework/data/wcf/wcf-data-services-overview)

- [WCF 服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)

- Web 服务

    > [!NOTE]
    > "数据源"窗口中 **显示** 的项目取决于服务返回的数据。 某些服务可能没有为“数据源配置”向导创建可绑定的对象提供足够的信息。 例如，如果服务返回非类型化数据集，则完成向导后，"数据源"窗口中不会显示任何项。 这是因为非类型化数据集不提供架构，因此向导没有足够的信息来创建数据源。

## <a name="data-source-for-an-object"></a>对象的数据源

可以通过运行"数据源配置向导"，然后选择"对象数据源类型"，从公开一个或多个公共属性的任何 **对象** 创建数据源。 对象的所有公共属性都显示在"数据源 **"窗口中** 。 如果使用 实体框架并生成了模型，则在这里可以找到作为应用程序的数据源的实体类。

在 **"选择数据对象"** 页上，展开树视图中的节点以找到要绑定到的对象。 树视图包含项目的节点，以及项目引用的程序集和其他项目的节点。

如果要绑定到未显示在树视图中的程序集或项目中的对象，请单击"添加引用"并使用"添加引用"对话框添加对程序集或项目的引用。 添加引用后，程序集或项目将添加到树视图中。

> [!NOTE]
> 在树视图中显示对象之前，可能需要生成包含对象的项目。

> [!NOTE]
> 若要支持拖放数据绑定，实现 或 接口 <xref:System.ComponentModel.ITypedList> <xref:System.ComponentModel.IListSource> 的对象必须具有默认构造函数。 否则，Visual Studio实例化数据源对象，并将项拖动到设计图面时显示错误。

## <a name="data-source-for-a-sharepoint-list"></a>数据源列表SharePoint数据源

可以通过运行数据源配置向导并选择SharePoint数据源类型，从 **SharePoint创建数据源**。  SharePoint通过 WCF Data Services 公开数据，因此SharePoint数据源与从服务创建数据源相同。 在 **"SharePoint****配置** 向导"中选择"添加服务引用"项会打开"添加服务引用"对话框，通过指向 SharePoint 服务器连接到 SharePoint 数据服务。  这需要 SharePoint SDK。

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
