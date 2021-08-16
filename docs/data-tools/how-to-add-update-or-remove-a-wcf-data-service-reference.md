---
title: 添加、更新或删除 WCF 数据服务引用
description: 查看如何添加、更新或删除 WINDOWS WCF (WCF) 数据服务引用。
ms.date: 11/04/2016
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
ms.openlocfilehash: ffe1d6cea14568f9d8859e005ee56bf45910348488864fe65f24c8b0512890de
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121347191"
---
# <a name="how-to-add-update-or-remove-a-wcf-data-service-reference"></a>如何：添加、更新或删除 WCF 数据服务引用

::: moniker range="vs-2017"
服务 *引用* 使项目能够访问一个或多个 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 。 使用 **"添加服务引用"** 对话框在当前解决方案中搜索、在本地、在本地网络或 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] Internet 上搜索。
::: moniker-end
::: moniker range=">=vs-2019"
可以使用 连接的服务中的 解决方案资源管理器 节点访问 **Microsoft WCF Web Service Reference Provider**，这样，就可以管理 Windows Communication Foundation (WCF) 数据服务引用。
::: moniker-end

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-a-wcf-service-reference"></a>添加 WCF 服务引用

### <a name="to-add-a-reference-to-an-external-service"></a>添加对外部服务的引用

::: moniker range="vs-2017"

1. 在 **解决方案资源管理器** 中，右键单击要添加服务的项目的名称，然后单击 **添加服务引用。**

   此时将出现“添加服务引用”对话框。

1. 在 **"地址**"框中，输入服务的 URL，然后单击"转到"搜索该服务。 如果服务实现用户名和密码安全性，系统可能会提示输入用户名和密码。

    > [!NOTE]
    > 应仅从受信任源引用服务。 从不受信任的源添加引用可能会危及安全性。

     还可以从"地址"列表中选择 URL，该 URL 存储以前找到有效服务元数据的 15 个 URL。 

     执行搜索时，将显示进度栏。 可以通过单击"停止"随时停止 **搜索**。

1. 在 **"服务** "列表中，展开想要使用的服务的节点，然后选择一个实体集。

1. 在“命名空间”框中，输入要用于参考的命名空间。

1. 单击“确定”将参考添加到项目中。

     将生成 (代理) 客户端，并且将描述该服务的元数据添加到 *app.config文件。*
::: moniker-end
::: moniker range=">=vs-2019"
1. 在 **解决方案资源管理器** 中，双击或点击 **连接的服务节点。**

   " **配置服务"** 选项卡随即打开。

1. 选择 **"Microsoft WCF Web Service Reference Provider"。**

   "**配置WCF Web Service Reference** 对话框出现。

   ![WCF Web 服务提供程序对话框的屏幕截图](media/vs-2019/configure-wcf-web-service-reference-dialog.png)


1. 在 **"URI"** 框中，输入服务的 URL，然后单击"转到"搜索该服务。 如果服务实现用户名和密码安全性，系统可能会提示输入用户名和密码。

    > [!NOTE]
    > 应仅从受信任源引用服务。 从不受信任的源添加引用可能会危及安全性。

     还可以从 **URI** 列表中选择 URL，该 URL 存储之前找到有效服务元数据的 15 个 URL。

     执行搜索时，将显示进度栏。 可以通过单击"停止"随时停止 **搜索**。

1. 在 **"服务** "列表中，展开想要使用的服务的节点，然后选择一个实体集。

1. 在“命名空间”框中，输入要用于参考的命名空间。

1. 单击 **"** 完成"以添加对项目的引用。

     将生成 (代理) 客户端，并且将描述该服务的元数据添加到 *app.config文件。*

::: moniker-end

### <a name="to-add-a-reference-to-a-service-in-the-current-solution"></a>在当前解决方案中添加对服务的引用

::: moniker range="vs-2017"

1. 在 **解决方案资源管理器** 中，右键单击要添加服务的项目的名称，然后单击 **添加服务引用。**

    此时将出现“添加服务引用”对话框。

1. 单击"**发现"。**

    当前解决方案 (和 WCF [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]) 的所有服务都添加到"服务 **"** 列表中。

1. 在 **"服务** "列表中，展开想要使用的服务的节点，然后选择一个实体集。

1. 在“命名空间”框中，输入要用于参考的命名空间。

1. 单击“确定”将参考添加到项目中。

    服务客户端 (代理) ，描述服务的元数据将添加到 *app.config文件。*
::: moniker-end
::: moniker range=">=vs-2019"
1. 在 **解决方案资源管理器** 中，双击或点击 **连接的服务节点。** 

   " **配置服务"** 选项卡随即打开。

1. 选择 **"Microsoft WCF Web Service Reference Provider"。**

   "**配置WCF Web Service Reference** 对话框出现。

1. 单击"**发现"。**

    当前解决方案 (和 WCF [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]) 的所有服务都添加到"服务 **"** 列表中。

1. 在 **"服务** "列表中，展开想要使用的服务的节点，然后选择一个实体集。

1. 在“命名空间”框中，输入要用于参考的命名空间。

1. 单击 **"** 完成"以添加对项目的引用。

    服务客户端 (代理) ，描述服务的元数据将添加到 *app.config文件。*

::: moniker-end

## <a name="update-a-service-reference"></a>更新服务引用

的实体数据模型 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 有时会更改。 发生这种情况时，必须更新服务引用。

### <a name="to-update-a-service-reference"></a>更新服务引用

- 在 **解决方案资源管理器** 中，右键单击服务引用，然后单击"**更新服务引用"。**

     当引用从原始位置更新时，将显示一个进度对话框，并且重新生成服务客户端以反映元数据中的任何更改。

## <a name="remove-a-service-reference"></a>删除服务引用

如果不再使用服务引用，可以从解决方案中删除它。

### <a name="to-remove-a-service-reference"></a>删除服务引用

- 在 **解决方案资源管理器** 中，右键单击服务引用，然后单击"删除 **"。**

     服务客户端将从解决方案中删除，描述服务的元数据将从 *app.config中删除。*

    > [!NOTE]
    > 必须手动删除引用服务引用的任何代码。

## <a name="see-also"></a>另请参阅

- [WindowsVisual Studio 中的 Communication Foundation Services 和 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
