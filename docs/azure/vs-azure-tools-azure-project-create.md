---
title: 创建 Azure 云服务项目
description: 了解如何使用 Visual Studio 创建 Azure 云服务项目
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 03/19/2019
ms.author: ghogen
ms.openlocfilehash: 0e7030349f47990f9ee12f8d51856bf8dcb5f0b18bf4c8a2bd32001d5b12cc82
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121406679"
---
# <a name="create-an-azure-cloud-service-project-with-visual-studio"></a>使用 Visual Studio 创建 Azure 云服务项目

Visual Studio提供了一个项目模板，可用于创建[Azure](/azure/cloud-services/cloud-services-choose-me)云服务，这是一个简单的通用 Azure 服务。 创建项目后，可通过 Visual Studio 调试、配置云服务，并将其部署到 Azure。

## <a name="steps-to-create-an-azure-cloud-service-project-in-visual-studio"></a>在 Visual Studio 中创建 Azure 云服务项目的步骤
本节介绍如何在 Visual Studio 中创建具有一个或多个 Web 角色的 Azure 云服务项目。

::: moniker range="vs-2017"
1. 以管理员的身份打开 Visual Studio。

1. 在主菜单上，选择"**文件""** > **新建** > Project"。

1. 从 Visual C# 或 Visual Basic 项目模板节点中选择“云”，并从模板列表中选择“Azure 云服务”。

    ![新建 Azure 云服务](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. 指定要用于开发项目的 .NET Framework 版本。

1. 输入项目的名称和位置以及解决方案的名称。

1. 选择“确定”。
::: moniker-end
::: moniker range=">=vs-2019"
1. 在“启动”窗口中，选择“创建新项目”。

1. 在搜索框中，键入“云”，然后选择“Azure 云服务”。

   ![新建 Azure 云服务](./media/vs-azure-tools-azure-project-create/vs-2019/new-project-cloud-service.png)

1. 为项目提供名称，然后选择“创建”。

   ![为项目提供名称](./media/vs-azure-tools-azure-project-create/vs-2019/new-project-cloud-service-2.png)
::: moniker-end

1. 在“新建 Microsoft Azure 云服务”对话框中，选择要添加的角色，然后选择右箭头按钮以将其添加到解决方案。

    ![选择新的 Azure 云服务角色](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. 要重命名已添加的角色，请在“新建 Microsoft Azure 云服务”对话框中将鼠标悬停在该角色上，然后从上下文菜单中选择“重命名”。 还可在添加角色后在解决方案（**解决方案资源管理器** 中）内对其进行重命名。

    ![重命名 Azure 云服务角色](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

Visual Studio Azure 项目与解决方案中的角色项目具有关联。 该项目还包括服务定义文件和服务配置文件：

- **服务定义文件** - 定义了应用程序的运行时设置，包括所需角色、终结点和虚拟机大小。
- **服务配置文件** - 配置了角色有多少实例在运行以及为角色定义的设置的值。

有关这些文件详细信息，请参阅使用 Visual Studio 为 Azure 云服务[配置角色](vs-azure-tools-configure-roles-for-cloud-service.md)。

## <a name="next-steps"></a>后续步骤
- [使用 Visual Studio 管理 Azure 云服务项目中的角色](./vs-azure-tools-cloud-service-project-managing-roles.md)
