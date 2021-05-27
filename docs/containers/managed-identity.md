---
title: 如何结合使用托管标识与 Bridge to Kubernetes
ms.technology: vs-azure
ms.date: 04/28/2021
ms.topic: conceptual
description: 了解如何结合使用 AKS 群集中的 Azure Active Directory (Azure AD) 托管标识与 Bridge to Kubernetes
monikerRange: '>=vs-2019'
manager: jmartens
author: ghogen
ms.author: ghogen
ms.openlocfilehash: e4847b25531b48c8200a2620ca3e975f9677c881
ms.sourcegitcommit: 60b7a6159045a44293043a519c8ea6d915bf2c31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2021
ms.locfileid: "108335098"
---
# <a name="use-managed-identity-with-bridge-to-kubernetes"></a>结合使用托管标识与 Bridge to Kubernetes

如果 AKS 群集使用[托管标识](/azure/active-directory/managed-identities-azure-resources/overview)安全功能来保护对机密和资源的访问，那么 Bridge to Kubernetes 需要一些特殊配置来确保它可以与这些功能配合使用。 需要将 Azure Active Directory (AD) 令牌下载到本地计算机，以确保本地执行和调试受到妥善保护，这需要在 Bridge to Kubernetes 中进行一些特殊配置。 本文介绍了如何配置 Bridge to Kubernetes 以与使用托管标识的服务配合使用。

## <a name="how-to-configure-your-service-to-use-managed-identity"></a>如何将服务配置为使用托管标识

若要启用支持托管标识的本地计算机，请在 KubernetesLocalConfig.yaml 文件的 `enableFeatures` 部分中添加 `ManagedIdentity`。 如果还没有 `enableFeatures` 部分，请添加它。

```yaml
enableFeatures:
    ManagedIdentity
```

> [!WARNING]
> 请务必仅在处理开发群集（而不是生产群集）时对 Bridge to Kubernetes 使用托管标识，因为 Azure AD 令牌会被提取到本地计算机，这将带来潜在的安全风险。

如果没有 KubernetesLocalConfig.yaml 文件，可以创建一个；请参阅[操作说明：配置 Bridge to Kubernetes](configure-bridge-to-kubernetes.md)。

## <a name="how-to-fetch-the-azure-active-directory-tokens"></a>如何提取 Azure Active Directory 令牌

在提取令牌时，必须确保在代码中依赖于 <xref:Azure.Identity.DefaultAzureCredential> 或 <xref:Azure.Identity.ManagedIdentityCredential>。

下面的 C# 代码展示了如何在使用 `ManagedIdentityCredential` 时提取存储帐户凭据：

```csharp
var credential = new ManagedIdentityCredential(miClientId);
Console.WriteLine("Created credential");
var containerClient = new BlobContainerClient(new Uri($"https://{accountName}.blob.windows.net/{containerName}"), credential);
Console.WriteLine("Created blob client");
```

下面的代码展示了如何在使用 DefaultAzureCredential 时提取存储帐户凭据：

```csharp
var credential = new DefaultAzureCredential();
Console.WriteLine("Created credential");
var containerClient = new BlobContainerClient(new Uri($"https://{accountName}.blob.windows.net/{containerName}"), credential);
Console.WriteLine("Created blob client");
```

若要了解如何使用托管标识访问其他 Azure 资源，请参阅[后续步骤](#next-steps)部分。

## <a name="receive-azure-alerts-when-tokens-are-downloaded"></a>当令牌被下载时接收 Azure 警报

每当你在服务上使用 Bridge to Kubernetes 时，Azure AD 令牌就会被下载到本地计算机。 可以启用 Azure 警报，以在这种情况发生时收到通知。 有关信息，请参阅[启用 Azure Defender](/azure/security-center/enable-azure-defender)。 请注意，30 天试用期后是要收费的。

## <a name="next-steps"></a>后续步骤

至此，你已经将 Bridge to Kubernetes 配置为用于使用托管标识的 AKS 群集，接下来可以照常调试了。 请参阅 [bridge-to-kubernetes.md#connect-to-your-cluster-and-debug-a-service]。

通过学习以下教程，详细了解如何使用托管标识来访问 Azure 资源：

- [教程：使用 Linux VM 系统分配的托管标识访问 Azure 存储](/azure/active-directory/managed-identities-azure-resources/tutorial-linux-vm-access-storage)
- [教程：使用 Linux VM 系统分配的托管标识访问 Azure Data Lake Store](/azure/active-directory/managed-identities-azure-resources/tutorial-linux-vm-access-datalake)
- [教程：使用 Linux VM 系统分配的托管标识访问 Azure Key Vault](/azure/active-directory/managed-identities-azure-resources/tutorial-linux-vm-access-nonaad)

此部分还有其他一些教程，介绍了如何使用托管标识来访问其他 Azure 资源。

## <a name="see-also"></a>另请参阅

[Azure Active Directory](/azure/active-directory/managed-identities-azure-resources/)
