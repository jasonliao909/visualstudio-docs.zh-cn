---
title: 设计业务数据连接模型 |Microsoft Docs
description: " (BDC) 模型中设计业务数据连接。 添加实体和方法。 定义方法参数。 添加筛选器描述符。 验证 BDC 模型。"
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], designing a model
- Business Data Connectivity service [SharePoint development in Visual Studio], designing a model
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: d7f8fec702baa493183753c2f23f945842f48bc3b9fbbad80833e33a3ea6c313
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121353002"
---
# <a name="design-a-business-data-connectivity-model"></a>设计业务数据连接模型
  您可以通过将实体和方法添加到模型文件来开发业务数据连接 (BDC) 服务的模型。 实体描述数据字段的集合。 例如，实体可以表示数据库中的表。 方法执行添加、删除或更新实体表示的数据等任务。 有关详细信息，请参阅将[业务数据集成到 SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)。

## <a name="add-entities"></a>添加实体
 可以通过将 **实体** 从 Visual Studio **工具箱** 拖动或复制到 BDC 设计器来添加实体。 有关详细信息，请参阅 [如何：将实体添加到模型](../sharepoint/how-to-add-an-entity-to-a-model.md)。

 在类中定义实体的字段。 例如，可以将名为的字段添加 `Address` 到 `Customer` 类中。 您可以将新类添加到项目中，也可以使用通过使用其他工具（如对象关系设计器 (O/R 设计器) 创建的现有类）。 实体的名称和表示该实体的类的名称不必匹配。 定义模型中的方法时，将类与实体相关联。

## <a name="add-methods"></a>添加方法
 当用户查看、添加、更新或删除基于模型的列表或 Web 部件中的信息时，BDC 服务将调用模型中的方法。 必须为用户可以执行的每个任务将方法添加到模型。 通过从 " **BDC 方法详细信息** " 窗口中选择五种基本方法类型中的任意一种，创建方法。 下表介绍了 BDC 模型的五种基本方法。

|方法|说明|
|------------|-----------------|
|程序|返回实体实例的集合。 当用户打开列表或 Web 部件时调用。 有关详细信息，请参阅 [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)。|
|特定的 Finder|返回特定的实体实例。 当用户查看列表中特定项的详细信息时调用。 有关详细信息，请参阅 [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)。|
|创建者|将新数据添加到实体的数据源。 当用户在基于模型的列表的功能区上选择 " **新建项** " 按钮时调用。 有关详细信息，请参阅 [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)。|
|更新者|修改列表中的数据。 当用户更新列表中的信息时调用。 有关详细信息，请参阅 [如何：添加更新方法](../sharepoint/how-to-add-an-updater-method.md)。|
|删除者|删除数据。 当用户从列表中删除某个项时调用。 有关详细信息，请参阅 [如何：添加删除器方法](../sharepoint/how-to-add-a-deleter-method.md)。|

## <a name="define-method-parameters"></a>定义方法参数
 创建方法时，Visual Studio 添加适用于方法类型的输入参数和输出参数。 这些参数只是占位符。 在大多数情况下，必须修改参数，使其传入或返回正确类型的数据。 例如，默认情况下，Finder 方法返回一个字符串。 在大多数情况下，你想要修改 Finder 方法的返回参数，使其返回实体的集合。 可以通过修改参数的类型描述符来实现此目的。 类型描述符是描述参数的数据类型的特性的集合。 有关详细信息，请参阅 [如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

 Visual Studio 使你能够在模型中的参数之间复制类型描述符。 例如，您可以为 `CustomerTD` 方法的返回参数定义一个名为的类型描述符 `GetCustomer` 。 可以 `CustomerTD` 在 **BDC 资源管理器** 中复制类型描述符，然后将该类型描述符粘贴到方法的输入参数 `CreateCustomer` 。 这可以防止您不得不多次定义同一类型描述符。

## <a name="method-instances"></a>方法实例
 创建方法时，Visual Studio 添加默认的方法实例。 方法实例是对方法的引用，外加参数的默认值。 单个方法可具有多个方法实例。 每个实例都是方法签名和一组默认值的组合。 有关详细信息，请参阅 [如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

 运行该项目时，方法实例显示在 SharePoint 列表上方的下拉列表中。 用户可以选择方法实例来查看数据。

 若要向方法实例添加默认值，则必须直接修改模型的 XML。 有关详细信息，请参阅 [DefaultValue](/previous-versions/office/developer/sharepoint-2010/ee559319(v=office.14))。

## <a name="add-filter-descriptors"></a>添加筛选器描述符
 模型的使用者可能希望检索符合某些条件的实体的实例。 若要启用此功能，可以将筛选器描述符添加到方法。 通过筛选器描述符，模型使用者可以通过在执行方法之前传递值来筛选方法结果集。 有关详细信息，请参阅 [如何：将筛选器参数添加到操作，以限制外部系统中的实例](/previous-versions/office/developer/sharepoint-2010/ee554889(v=office.14))。

 SharePoint 提供多种功能，使用户能够提供筛选器值。 例如，"业务数据" Web 部件提供筛选器文本框。 用户可通过在该文本框中输入值来限制列表中的数据。 有关如何向方法添加筛选器描述符的详细信息，请参阅 [如何：向 Finder 方法添加筛选器描述符](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md)。

### <a name="filter-descriptor-properties"></a>筛选器描述符属性
 必须设置筛选器描述符的 **关联类型描述符**、 **名称** 和 **类型** 属性的值。 所有其他属性都是可选的。

 **关联的类型描述符** 属性将筛选器描述符与输入参数相关联。 当用户提供筛选值时，BDC 服务将使用输入参数将该值传递到方法中。

 **Type** 属性描述您要使用的筛选模式。 在 SharePoint 中，所选筛选模式将影响在用户界面 (UI) 中显示的文本。 例如，对于比较运算符筛选模式，文本 **等于** 显示为业务数据 Web 部件上的控件。 有关每个筛选模式的详细信息，请参阅 [BDC 支持的筛选器类型](/previous-versions/office/developer/sharepoint-2010/ee556392(v=office.14))。

 有关筛选器描述符的属性的详细信息，请参阅 [FilterDescriptor](/previous-versions/office/developer/sharepoint-2010/ee557835(v=office.14))。

### <a name="provide-default-values"></a>提供默认值
 在某些情况下，用户可能无法提供筛选器值。 可以通过将默认值添加到方法实例来提供默认值，也可以通过在方法的代码中设置默认值来提供默认值。 有关如何向方法实例添加默认值的详细信息，请参阅 [MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14))。 有关如何在方法的代码中设置输入参数的默认值的示例，请参阅 [如何：向 Finder 方法添加筛选器描述符](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md)。

## <a name="validate-the-model"></a>验证模型
 你可以在开发过程中验证模型。 Visual Studio 确定可阻止模型按预期方式工作的问题。 这些问题出现在 Visual Studio **错误列表** 中。

 您可以通过打开 "BDC 设计器" 的快捷菜单，然后选择 " **验证**" 来验证模型。 如果模型包含任何错误，它们将出现在 **错误列表** 中。 你可以通过双击列表中的错误，快速将光标移至包含错误的代码。 或者，可以重复选择 **F8** 或 **Shift** F8 键，以向前或向后单步执行 + 列表中的错误。

 当以某种方式违反模型规则时，可能会发生验证错误。 例如，如果类型 **描述符的 IsCollection** 属性设置为 **true，** 但不存在子类型描述符，则会出现验证错误。 可能需要参考 BDC 模型的规则，以了解错误列表 Visual Studio **错误**。 有关 BDC 模型规则的信息，请参阅 [BDCMetadata 架构](/previous-versions/office/developer/sharepoint-2010/ee556387(v=office.14))。

## <a name="debug-the-solution-that-contains-the-model"></a>调试包含模型的解决方案
 可以像调试代码中的任何代码一样调试Visual Studio。 若要调试代码，请设置代码中任意位置的断点，然后启动调试器。 Visual Studio打开SharePoint站点。 在SharePoint，创建使用业务数据的列表或 Web 部件。 然后，可以逐步执行代码。 有关调试 SharePoint 项目的详细信息，请参阅 [SharePoint 解决方案疑难解答](../sharepoint/troubleshooting-sharepoint-solutions.md)。

 还可以调试添加到项目的自定义程序集中的代码。 但是，若要调试自定义程序集中的代码，必须将该程序集添加到解决方案包。 有关详细信息，请参阅 [如何：添加和删除其他程序集](../sharepoint/how-to-add-and-remove-additional-assemblies.md)。

 有关将自定义程序集添加到项目的信息，请参阅 [如何：在 BDC 功能 中包括自定义程序集](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)。

### <a name="configure-bdc-security"></a>配置 BDC 安全性
 在调试解决方案之前，可能需要SharePoint中的安全设置。 若要修改这些设置，请打开 SharePoint 2010 管理中心网站中的"业务数据连接服务应用程序"。 在 **"设置元数据存储** 权限"对话框中，添加用户帐户，然后选择以下任一选项：

|任务|选项|
|----------|------------|
|将模型部署到 BDC 服务。|编辑|
|使用外部内容Web 部件创建列表和 (模型中) 实体。|客户端中的可选项|
|创建、读取、更新和删除实体数据。|执行|

 有关这些设置详细信息，请参阅 [业务数据连接服务管理](/previous-versions/office/sharepoint-server-2010/ee661742(v=office.14))。

 还可以为单个模型或外部内容类型设置安全权限。 若要详细了解如何设置模型的安全权限，请参阅 [BDC 模型管理](/previous-versions/office/sharepoint-server-2010/ee524073(v=office.14))。 若要详细了解如何设置外部内容类型的安全权限，请参阅 [外部内容类型管理](/previous-versions/office/sharepoint-server-2010/ee524076(v=office.14))。

> [!NOTE]
> 使用这些设置在本地服务器中调试SharePoint解决方案。 有关如何在生产环境中配置与 BDC 相关的安全设置SharePoint，请参阅[业务数据连接服务安全概述](/previous-versions/office/sharepoint-server-2010/ee661743(v=office.14))。

### <a name="retract-models-that-become-corrupt"></a>收回损坏的模型
 当您第一次启动调试器时，Visual Studio 会将整个模型部署到 SharePoint。 此后，每次Visual Studio，SharePoint在部署之间做出的任何更改来更新模型中的模型。

 在某些情况下，你可能希望Visual Studio模型完全收回SharePoint模型。 例如，模型可能会损坏。  若要将模型重新部署SharePoint，将模型的 **Incremental Update** 属性设置为 **False，** 然后启动调试器。 选择 **在** **BDC** 资源管理器中表示模型的节点时，"增量更新"属性将显示在"属性"窗口中。 默认情况下，模型的名称为 **BdcModel1**。

### <a name="change-identifier-names-of-entities-in-the-model"></a>更改模型中实体的标识符名称
 如果在部署模型后更改标识符的名称，可能会收到部署错误。 无法将模型的 Incremental **Update** 属性设置为 False 来解决 **此错误**。 必须手动收回模型，然后再次部署解决方案。 有关详细信息，请参阅故障排除[SharePoint解决方案](../sharepoint/troubleshooting-sharepoint-solutions.md)。 在最初部署模型之前，可以通过将 **"增量更新** "属性设置为 **False** 来避免此错误。

## <a name="locate-documentation-for-bdc-model-elements"></a>查找 BDC 模型元素的文档
 Visual Studio为创建的每个实体、方法或其他项向模型添加 XML 元素。 元素属性在"属性"窗口中 **显示为** 属性。 有关在设计模型时Visual Studio元素和属性的信息，请参阅[BDCMetadata 架构](/previous-versions/office/developer/sharepoint-2010/ee556387(v=office.14))。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)|介绍可用于直观地为 BDC 设计模型的工具。|
|[如何：向模型添加实体](../sharepoint/how-to-add-an-entity-to-a-model.md)|演示如何向模型添加外部内容类型或实体。|
|[如何：添加查找器方法](../sharepoint/how-to-add-a-finder-method.md)|演示如何添加使用户能够查看列表或 Web 部件中的实体列表的方法。|
|[如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)|演示如何添加使用户能够查看特定实体详细信息的方法。|
|[如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)|演示如何添加方法，使用户可以直接从列表或 Web 部件向数据源添加记录。|
|[如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)|演示如何添加一种方法，以便用户通过使用列表或 Web 部件用户界面 (UI) 中删除数据源的数据。|
|[如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)|演示如何添加使用户能够直接从列表或 Web 部件更改数据源中数据记录的方法。|
|[如何：向方法添加参数](../sharepoint/how-to-add-a-parameter-to-a-method.md)|演示如何使用方法中的"方法详细信息Visual Studio向方法添加输入和返回参数。|
|[如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)|演示如何在模型中定义参数数据类型。|
|[如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)|演示如何创建 BDC 执行的方法的实例。|
|[如何：向 Finder 方法添加筛选器描述符](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md)|演示如何让用户限制 Finder 方法返回的实例数。|
|[创建实体之间的关联](../sharepoint/creating-an-association-between-entities.md)|描述如何定义模型中实体之间的关系。 业务Web 部件、外部列表和自定义应用程序可以在用户界面中显示这些数据 (UI) 。|
|[如何：创建实体之间的关联](../sharepoint/how-to-create-an-association-between-entities.md)|演示如何定义模型中实体之间的关系。|
|[演练：使用业务数据在 SharePoint创建外部列表](../sharepoint/walkthrough-creating-an-external-list-in-sharepoint-by-using-business-data.md)|提供分步说明，说明如何创建和测试在外部列表中显示联系人SharePoint模型。|
|[将业务数据集成到 SharePoint 中](../sharepoint/integrating-business-data-into-sharepoint.md)|概述如何为 BDC 服务创建和设计模型。|
