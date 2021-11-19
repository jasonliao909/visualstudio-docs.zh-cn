---
title: 使用 ClickOnce 部署多目标应用
description: 了解如何使用 ClickOnce 部署技术部署面向多个版本的 .NET Framework 的应用程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, multiple .NET Framework versions
- ClickOnce deployment, multiple .NET Framework versions
- deploying applications [ClickOnce], multiple .NET Framework versions
ms.assetid: e0a8c330-21bc-4eb2-b936-fd0f3c3221f1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- dotnet
ms.openlocfilehash: 0e0e1c010ee1dcf1cc53f37610e518b817a31871
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664135"
---
# <a name="how-to-use-clickonce-to-deploy-applications-that-can-run-on-multiple-versions-of-the-net-framework"></a>如何：使用 ClickOnce 部署可在多个版本的 .NET Framework 上运行的应用程序
你可以使用 ClickOnce 部署技术部署面向多个版本的 .NET Framework 的应用程序。 这就需要生成和更新应用程序和部署清单。

> [!NOTE]
> 在将应用程序更改为面向多个版本的 .NET Framework 之前，应确保应用程序与多个版本的 .NET Framework 一起运行。 版本公共语言运行时在 .NET Framework 4 与 .NET Framework 2.0、.NET Framework 3.0 和 .NET Framework 3.5 之间有所不同。

 此过程需要执行以下步骤：

1. 生成应用程序和部署清单。

2. 更改部署清单以列出多个.NET Framework 版本。

3. 更改 app.config 文件以列出可兼容的 .NET Framework 运行时版本。

4. 更改应用程序清单，将依赖程序集标记为 .NET Framework 程序集。

5. 对应用程序清单进行签名。

6. 更新部署清单并签名。

### <a name="to-generate-the-application-and-deployment-manifests"></a>生成应用程序和部署清单

- 使用发布向导或项目设计器的“发布”页面发布应用程序并生成应用程序和部署清单文件。 有关详细信息，请参阅[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)或[“项目设计器”的“发布”页](../ide/reference/publish-page-project-designer.md)。

### <a name="to-change-the-deployment-manifest-to-list-the-multiple-net-framework-versions"></a>更改部署清单以列出多个.NET Framework 版本

1. 在发布目录中，通过在 Visual Studio 中使用 XML 编辑器，打开部署清单。 部署清单的文件扩展名为“.application”。

2. 将 `<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">` 和 `</compatibleFrameworks>` 元素之间的 XML 代码替换为 XML，其中列出了应用程序支持的 .NET Framework 版本。

     下表显示了一些可用的.NET Framework 版本以及可添加到部署清单的相应 XML。

    |.NET Framework 版本|XML|
    |----------------------------|---------|
    |4 客户端|\<framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.30319" />|
    |4 完整|\<framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.30319" />|
    |3.5 客户端|\<framework targetVersion="3.5" profile="Client" supportedRuntime="2.0.50727" />|
    |3.5 完整|\<framework targetVersion="3.5" profile="Full" supportedRuntime="2.0.50727" />|
    |3.0|\<framework targetVersion="3.0" supportedRuntime="2.0.50727" />|

### <a name="to-change-the-appconfig-file-to-list-the-compatible-net-framework-runtime-versions"></a>更改 app.config 文件以列出可兼容的 .NET Framework 运行时版本

1. 在解决方案资源管理器中，通过在 Visual Studio 中使用 XML 编辑器，打开 app.config文件。

2. 将 `<startup>` 和 `</startup>` 元素之间的 XML 代码替换为 XML（或为此代码添加 XML），其中列出了应用程序支持的 .NET Framework 版本。

     下表显示了一些可用的.NET Framework 版本以及可添加到部署清单的相应 XML。

    |.NET Framework 运行时版本|XML|
    |------------------------------------|---------|
    |4 客户端|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0,Profile=Client" />|
    |4 完整|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0" />|
    |3.5 完整|\<supportedRuntime version="v2.0.50727"/>|
    |3.5 客户端|\<supportedRuntime version="v2.0.50727" sku="Client"/>|

### <a name="to-change-the-application-manifest-to-mark-dependent-assemblies-as-net-framework-assemblies"></a>更改应用程序清单，将依赖程序集标记为 .NET Framework 程序集

1. 在发布目录中，通过在 Visual Studio 中使用 XML 编辑器，打开应用程序清单。 部署清单的文件扩展名为“.manifest”。

2. 将 `group="framework"` 添加到 Sentinel 程序集的依赖项 XML（`System.Core`、`WindowsBase`、`Sentinel.v3.5Client` 和 `System.Data.Entity`）。 例如，XML 应如下所示：

   ```xml
   <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" group="framework">
   ```

3. 将 Microsoft.Windows.CommonLanguageRuntime 的 `<assemblyIdentity>` 元素版本号更新为作为最小公分母的 .NET Framework 的版本号。 例如，如果应用程序面向 .NET Framework 3.5 和 .NET Framework 4，请使用版本号 2.0.50727.0，XML 应如下所示：

   ```xml
   <dependency>
     <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">
       <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="2.0.50727.0" />
     </dependentAssembly>
   </dependency>
   ```

### <a name="to-update-and-re-sign-the-application-and-deployment-manifests"></a>更新应用程序和部署清单并重新签名

- 更新应用程序和部署清单并重新签名。 有关详细信息，请参阅[如何：对应用程序和部署清单重新签名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)。

## <a name="see-also"></a>另请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [\<compatibleFrameworks> 元素](../deployment/compatibleframeworks-element-clickonce-deployment.md)
- [\<dependency> 元素](../deployment/dependency-element-clickonce-application.md)
- [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)
- [配置文件架构](/dotnet/framework/configure-apps/file-schema/index)
