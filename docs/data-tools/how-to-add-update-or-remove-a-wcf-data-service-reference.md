---
title: 添加、更新或删除 WCF 数据服务引用
description: 查看如何添加、更新或删除 Windows Communication Foundation (WCF) 数据服务引用。
ms.date: 11/22/2021
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- service references [Visual Studio]
- WCF Data Service reference
- WCF data service references
- ADO.NET service references
- ADO.NET Data Service reference
ms.assetid: 892ebf37-3af4-472e-8744-92837677d611
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 662e93d7796ac9d611c274ace1f419a4f61e6111
ms.sourcegitcommit: 8671132ee0425b273b060fa35c75657e7ae02583
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/23/2021
ms.locfileid: "132924246"
---
# <a name="how-to-add-update-or-remove-a-wcf-data-service-reference"></a>如何：添加、更新或删除 WCF 数据服务引用

对于 .NET Framework 项目，服务引用使项目能够访问一个或多个 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]。 使用“添加服务引用”对话框通过本地、局域网或 Internet 在当前解决方案中搜索 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]。

:::moniker range=">=vs-2019"
对于 .NET Core 项目，可使用解决方案资源管理器中的连接服务节点访问 Microsoft WCF Web Service Reference 提供程序，该程序可管理 Windows Communication Foundation (WCF) 数据服务引用  。
:::moniker-end

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-a-wcf-service-reference"></a>添加 WCF 服务引用

### <a name="to-add-a-reference-to-an-external-service-net-framework-projects"></a>若要添加对外部服务的引用（.NET Framework 项目）

1. 在解决方案资源管理器中，右键单击要添加服务的项目的名称，然后单击“添加服务引用” 。

   此时将出现“添加服务引用”对话框。

1. 在“地址”框中，输入服务的 URL，然后单击“转到”以搜索服务 。 如果服务实施用户名和密码安全性，将提示你输入用户名和密码。

    > [!NOTE]
    > 应仅从受信任源引用服务。 从不受信任的源添加引用可能会危及安全性。

     还可以从“地址”列表中选择 URL，该列表存储先前 15 个指向有效服务元数据的 URL。

     执行搜索时会显示进度条。 可以随时单击“停止”来停止搜索。

1. 在“服务”列表中，展开你要使用的服务的节点，然后选择实体集。

1. 在“命名空间”框中，输入要用于参考的命名空间。

1. 单击“确定”将参考添加到项目中。

     然后会生成服务客户端（代理），描述服务的元数据也会添加到 app.config 文件中。

:::moniker range=">=vs-2019"
### <a name="to-add-a-reference-to-an-external-service-net-core-projects-including-net-5-and-later"></a>若要添加对外部服务的引用（.NET Core 项目，包括 .NET 5 及更高版本）

1. 在解决方案资源管理器中，双击或点击连接服务节点 。

   此时会打开“配置服务”选项卡。

1. 选择“Microsoft WCF Web 服务引用提供程序”。

   此时会显示“配置 WCF Web 服务引用”对话框。

   ![WCF Web 服务提供程序对话框的屏幕截图](media/vs-2019/configure-wcf-web-service-reference-dialog.png)

1. 在“URI”框中，输入服务的 URL，然后单击“转到”以搜索服务 。 如果服务实施用户名和密码安全性，将提示你输入用户名和密码。

    > [!NOTE]
    > 应仅从受信任源引用服务。 从不受信任的源添加引用可能会危及安全性。

     还可以从“URL”列表中选择 URL，该列表存储先前 15 个指向有效服务元数据的 URL。

     执行搜索时会显示进度条。 可以随时单击“停止”来停止搜索。

1. 在“服务”列表中，展开你要使用的服务的节点，然后选择实体集。

1. 在“命名空间”框中，输入要用于参考的命名空间。

1. 单击“完成”将参考添加到项目中。

     然后会生成服务客户端（代理），描述服务的元数据也会添加到 app.config 文件中。
:::moniker-end

### <a name="to-add-a-reference-to-a-service-in-the-current-solution-net-framework-projects"></a>若要在当前解决方案中添加对服务的引用（.NET Framework 项目）

1. 在解决方案资源管理器中，右键单击要添加服务的项目的名称，然后单击“添加服务引用” 。

    此时将出现“添加服务引用”对话框。

1. 单击“发现”。

    当前解决方案中的所有服务（[!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 和 WCF 服务）都添加到“服务”列表中。

1. 在“服务”列表中，展开你要使用的服务的节点，然后选择实体集。

1. 在“命名空间”框中，输入要用于参考的命名空间。

1. 单击“确定”将参考添加到项目中。

    然后会生成服务客户端（代理），描述服务的元数据也会添加到 app.config 文件中。

:::moniker range=">=vs-2019"

### <a name="to-add-a-reference-to-a-service-in-the-current-solution-net-core-projects"></a>若要在当前解决方案中添加对服务的引用（.NET Core 项目）

1. 在解决方案资源管理器中，双击或点击连接服务节点 。 

   此时会打开“配置服务”选项卡。

1. 选择“Microsoft WCF Web 服务引用提供程序”。

   此时会显示“配置 WCF Web 服务引用”对话框。

1. 单击“发现”。

    当前解决方案中的所有服务（[!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 和 WCF 服务）都添加到“服务”列表中。

1. 在“服务”列表中，展开你要使用的服务的节点，然后选择实体集。

1. 在“命名空间”框中，输入要用于参考的命名空间。

1. 单击“完成”将参考添加到项目中。

    然后会生成服务客户端（代理），描述服务的元数据也会添加到 app.config 文件中。

:::moniker-end

## <a name="update-a-service-reference"></a>更新服务引用

[!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 的实体数据模型有时会发生变化。 发生这种情况时，必须更新服务引用。

### <a name="to-update-a-service-reference"></a>更新服务引用

- 在解决方案资源管理器中，右键单击服务引用，然后单击“更新服务引用” 。

     从引用的初始位置对其进行更新时会显示一个进度对话框，并且会重新生成服务客户端以显示元数据中的所有更改。

## <a name="remove-a-service-reference"></a>删除服务引用

如果不再使用服务引用，可以将其从解决方案中删除。

### <a name="to-remove-a-service-reference"></a>删除服务引用

- 在解决方案资源管理器中，右键单击服务引用，然后单击“删除” 。

     服务客户端将从解决方案中删除，描述服务的元数据将从 app.config 文件中删除。

    > [!NOTE]
    > 必须手动删除所有引用服务引用的代码。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
