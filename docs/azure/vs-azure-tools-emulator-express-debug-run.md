---
title: 使用 Emulator Express 在本地运行/调试 Azure 云服务
ms.custom: SEO-VS-2020
description: 使用 Emulator Express 在本地计算机上运行和调试云服务
author: mikejo5000
manager: jmartens
ms.technology: vs-azure
ms.topic: how-to
ms.workload: azure-vs
ms.date: 03/06/2017
ms.author: mikejo
ms.openlocfilehash: be382d80aea5a8f44001dc453741a1685fb644bc
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602141"
---
# <a name="using-emulator-express-to-run-and-debug-an-azure-cloud-service-on-a-local-machine"></a>使用 Emulator Express 在本地计算机上运行和调试 Azure 云服务
通过使用 Emulator Express，可以测试和调试云服务，而不需要以管理员身份运行 Visual Studio。 可以将项目设置指定为根据云服务的要求使用 Emulator Express 或完整版模拟器。 有关完整模拟器的详细信息，请参阅 [Run an Azure Application in the Compute Emulator](/azure/storage/common/storage-use-emulator)（在计算模拟器中运行 Azure 应用程序）。

## <a name="using-emulator-express-in-visual-studio"></a>在 Visual Studio 中使用 Emulator Express
在 Azure SDK 2.3 或更高版本中创建 Azure 项目时会自动使用 Emulator Express。 对于使用早期版本的 Azure SDK 创建的现有项目，请按照以下步骤来选择 Emulator Express：

1. 在 Visual Studio 中创建或打开 Azure 云服务项目。

1. 在“解决方案资源管理器”中右键单击项目，并从上下文菜单中选择“属性”。

1. 在项目属性页中，选择“Web”选项卡。

    ![Azure 云服务项目的的属性](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. 在“本地开发服务器”下，选择“使用 IIS Express”选项。

1. 在“模拟器”下，选择“使用 Emulator Express”。

1. 若要启动 Emulator Express，请在命令提示符处运行以下命令：

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a>Emulator Express 限制
以下问题是 Emulator Express 的已知限制：

- Emulator Express 与 IIS Web 服务器不兼容。
- 云服务可以包含多个角色，但每个角色只能有一个实例。
- 无法访问 1000 以下的端口号。 如果所用的某个身份验证提供程序通常使用低于 1000 的端口，则可能需要将此值更改为 1000 以上的端口号。
- 适用于 Azure 计算模拟器的任何限制也适用于 Emulator Express。 例如，每个部署的角色实例数不能超过 50 个。 有关 Azure 计算模拟器的详细信息，请参阅[在计算模拟器中运行 Azure 应用程序](vs-azure-tools-performance-profiling-cloud-services.md)。

## <a name="next-steps"></a>后续步骤
[调试 Azure 云服务](vs-azure-tools-debugging-cloud-services-overview.md)
