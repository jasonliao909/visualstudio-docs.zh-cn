---
title: 设置命名的身份验证凭据 | Microsoft Docs
description: 了解如何提供 Visual Studio 可用于验证对 Azure 的请求的凭据，以便从 Visual Studio 将应用程序发布到 Azure 或者监视现有云服务。
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/11/2017
ms.author: ghogen
ms.openlocfilehash: e7d8acc861e1460cc569ce6e1bd75ce01bd6e4b4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122031817"
---
# <a name="set-up-named-authentication-credentials"></a>设置命名的身份验证凭据

若要将应用程序发布到 Azure 或监视现有云服务，Visual Studio 需要凭据以对向 Azure 发出的请求进行身份验证，即你的 Azure 订阅 ID 和带至少 2048 位密钥的有效 X.509 v3 证书。 可通过以下某个方法提供这些凭据：

- 在 Visual Studio 中，选择“视图 > 服务器资源管理器”，右键单击 Azure 节点，选择“连接到 Microsoft Azure 订阅”，然后登录。
- 创建一个订阅文件 (`.publishsettings`)，其中包含证书公钥。 如本文所述，该订阅文件可以包含多个订阅的凭据。

注意：这些凭据与用于对 Azure 存储服务的请求进行身份验证的凭据不同。

## <a name="create-a-subscription-file"></a>创建订阅文件

在“服务器资源管理器”中，右键单击 Azure 节点，并选择“管理和筛选订阅”。 然后选择“证书”选项卡，然后执行以下任一操作：

- 选择“导入”，打开“导入 Microsoft Azure 订阅”对话框。 选择“下载订阅文件”链接，然后在浏览器中将下载的文件保存到临时位置。 返回对话框，浏览到下载位置，然后将其导入，以便在身份验证中使用。
- 选择一个有效订阅，并选择“编辑”，随即打开一个对话框，可在其中编辑在身份验证中使用的现有订阅。
- 选择“新建”，打开“新建订阅”对话框，并提供所需的详细信息。 若要将证书上传到对话框中注明的云服务中，登录到 Azure 门户，导航到云服务，选择“设置 > 管理证书”，选择“上传”，然后指定 `.cer` 文件路径。

如果要自行创建证书，可以参阅[创建并上传 Azure 管理证书](/azure/cloud-services/cloud-services-certs-create)中的说明，然后将证书手动上传到 [Azure 门户](https://portal.azure.com/)。

## <a name="next-steps"></a>后续步骤

- [Web 应用一般概述](/azure/app-service/)
- [将你的应用部署到 Azure App Service](/azure/app-service/app-service-deploy-local-git)
- [使用 Visual Studio 部署 Web 作业](/azure/app-service/websites-dotnet-deploy-webjobs)
- [创建和部署云服务](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
