---
title: 使用ClickOnce部署多目标应用
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
可以使用 ClickOnce 部署技术部署面向多个版本的 .NET Framework 应用程序。 这要求生成和更新应用程序和部署清单。

> [!NOTE]
> 在将应用程序更改为面向多个版本的 .NET Framework 之前，应确保应用程序使用多个版本的 .NET Framework。 版本公共语言运行时在 .NET Framework 4 与 .NET Framework 2.0、.NET Framework 3.0 和 .NET Framework 3.5 之间有所不同。

 此过程需要以下步骤：

1. 生成应用程序和部署清单。

2. 更改部署清单以列出多个.NET Framework版本。

3. 更改app.config *文件* 以列出运行时.NET Framework兼容。

4. 更改应用程序清单，将依赖程序集标记为.NET Framework程序集。

5. 对应用程序清单进行签名。

6. 更新部署清单并签名。

### <a name="to-generate-the-application-and-deployment-manifests"></a>生成应用程序和部署清单

- 使用设计器的发布向导或Project页发布应用程序并生成应用程序和部署清单文件。 有关详细信息，请参阅[如何：](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)使用发布ClickOnce发布向导或发布页发布应用程序，Project[设计器](../ide/reference/publish-page-project-designer.md)。

### <a name="to-change-the-deployment-manifest-to-list-the-multiple-net-framework-versions"></a>更改部署清单以列出多个.NET Framework版本

1. 在发布目录中，使用"发布"目录中的"XML 编辑器"打开Visual Studio。 部署清单具有 *.application* 文件扩展名。

2. 将 和 元素之间的 XML 代码 `<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">` `</compatibleFrameworks>` 替换为 XML，该 XML 列出了.NET Framework应用程序支持的版本。

     下表显示了一些可用的.NET Framework版本以及可添加到部署清单的相应 XML。

    |.NET Framework 版本|XML|
    |----------------------------|---------|
    |4 客户端|\<framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.30319" />|
    |4 完整|\<framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.30319" />|
    |3.5 客户端|\<framework targetVersion="3.5" profile="Client" supportedRuntime="2.0.50727" />|
    |3.5 完整|\<framework targetVersion="3.5" profile="Full" supportedRuntime="2.0.50727" />|
    |3.0|\<framework targetVersion="3.0" supportedRuntime="2.0.50727" />|

### <a name="to-change-the-appconfig-file-to-list-the-compatible-net-framework-runtime-versions"></a>更改app.config文件以列出.NET Framework版本

1. 在 解决方案资源管理器中，app.config中的XML 编辑器打开 Visual Studio。

2. 将 (或) 和 元素之间的 XML 代码替换为 `<startup>` `</startup>` XML，该 XML .NET Framework应用程序支持的应用程序运行时。

     下表显示了一些可用的.NET Framework版本以及可添加到部署清单的相应 XML。

    |.NET Framework运行时版本|XML|
    |------------------------------------|---------|
    |4 客户端|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0,Profile=Client" />|
    |4 完整|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0" />|
    |3.5 完整|\<supportedRuntime version="v2.0.50727"/>|
    |3.5 客户端|\<supportedRuntime version="v2.0.50727" sku="Client"/>|

### <a name="to-change-the-application-manifest-to-mark-dependent-assemblies-as-net-framework-assemblies"></a>更改应用程序清单以将依赖程序集标记为.NET Framework程序集

1. 在发布目录中，使用"发布"目录中的"XML 编辑器"打开Visual Studio。 部署清单具有 *.manifest* 文件扩展名。

2. 将 `group="framework"` 添加到 sentinel 程序集的依赖项 XML `System.Core` (、、 和 `WindowsBase` `Sentinel.v3.5Client` `System.Data.Entity`) 。 例如，XML 应如下所示：

   ```xml
   <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" group="framework">
   ```

3. 更新 `<assemblyIdentity>` Microsoft.Windows 的 元素的版本号。CommonLanguageRuntime 到最低公共分母.NET Framework的版本号。 例如，如果应用程序面向 .NET Framework 3.5 和 .NET Framework 4，请使用 2.0.50727.0 版本号，XML 应如下所示：

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
- [ClickOnce部署清单](../deployment/clickonce-deployment-manifest.md)
- [配置文件架构](/dotnet/framework/configure-apps/file-schema/index)
