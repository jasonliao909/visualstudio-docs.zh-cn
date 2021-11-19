---
title: 部署中先决条件的支持 URL ClickOnce URL
description: 了解应用程序ClickOnce先决条件的部署测试ClickOnce部署如何处理缺少的先决条件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, prerequisites
- ClickOnce deployment, URLs
ms.assetid: 590742c3-a286-4160-aa75-7a441bb2207b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 048d379aa3194eb7e6fca46019e6c5a2ddbd60c5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665865"
---
# <a name="how-to-specify-a-support-url-for-individual-prerequisites-in-a-clickonce-deployment"></a>如何：为 ClickOnce 部署中的各个系统必备项指定一个支持 URL
部署可以测试许多必备组件，这些先决条件必须在客户端计算机 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 上提供，应用程序 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 才能运行。 这些依赖项包括所需的最低版本 .NET Framework、操作系统的版本，以及必须预装在全局程序集缓存 (GAC) 。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]但是，无法自行安装任何这些先决条件;如果找不到必备组件，则只会停止安装并显示一个对话框，说明安装失败的原因。

 有两种方法用于安装必备组件。 可以使用引导程序应用程序安装它们。 或者，可以指定单个先决条件的支持 URL，如果找不到先决条件，该 URL 将在对话框中向用户显示。 该 URL 引用的页面可以包含指向安装所需先决条件的说明的链接。 如果应用程序未指定单个先决条件的支持 URL，则显示整个应用程序的部署清单中指定的支持 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] URL（如果已定义）。

 虽然 、Mage.exe和MageUI.exe都可用于生成部署，但这些工具都直接不支持为单个先决条件 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]  [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 指定支持 URL。 本文档介绍如何修改部署的应用程序清单和部署清单，以包含这些支持 URL。

### <a name="specify-a-support-url-for-an-individual-prerequisite"></a>为单个先决条件指定支持 URL

1. 在文本编辑器 (*.manifest*) [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 打开应用程序清单。

2. 对于操作系统先决条件，将 `supportUrl` 属性添加到 `dependentOS` 元素：

   ```xml
    <dependency>
       <dependentOS supportUrl="http://www.adatum.com/MyApplication/wrongOSFound.htm">
         <osVersionInfo>
           <os majorVersion="5" minorVersion="1" buildNumber="2600" servicePackMajor="0" servicePackMinor="0" />
         </osVersionInfo>
       </dependentOS>
     </dependency>
   ```

3. 对于特定版本的公共语言运行时的先决条件，将 属性添加到指定公共语言 `supportUrl` `dependentAssembly` 运行时依赖项的条目：

   ```xml
     <dependency>
       <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" supportUrl=" http://www.adatum.com/MyApplication/wrongClrVersionFound.htm">
         <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="4.0.30319.0" />
       </dependentAssembly>
     </dependency>
   ```

4. 对于必须预装在全局程序集缓存中的程序集的先决条件，请为指定所需程序集 `supportUrl` `dependentAssembly` 的元素设置 ：

   ```xml
     <dependency>
       <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" supportUrl=" http://www.adatum.com/MyApplication/missingSampleGACAssembly.htm">
         <assemblyIdentity name="SampleGACAssembly" version="5.0.0.0" publicKeyToken="04529dfb5da245c5" processorArchitecture="msil" language="neutral" />
       </dependentAssembly>
     </dependency>
   ```

5. 可选。 对于面向 .NET Framework 4 的应用程序，在 (*中打开应用程序的 .application*) [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 清单。

6. 对于.NET Framework 4 先决条件，将 `supportUrl` 属性添加到 `compatibleFrameworks` 元素：

   ```xml
   <compatibleFrameworks  xmlns="urn:schemas-microsoft-com:clickonce.v2" supportUrl="http://adatum.com/MyApplication/CompatibleFrameworks.htm">
     <framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.30319" />
     <framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.30319" />
   </compatibleFrameworks>
   ```

7. 手动更改应用程序清单后，必须使用数字证书对应用程序清单重新签名，然后更新部署清单并重新签名。 使用 *Mage.exe* 或 *MageUI.exe* SDK 工具来完成此任务，因为使用 重新生成这些文件会清除 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 手动更改。 有关使用 Mage.exe 清单进行重新签名的详细信息，请参阅[如何：为应用程序和部署清单重新签名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)。

## <a name="net-framework-security"></a>.NET Framework 安全性
 如果将应用程序标记为在部分信任下运行，则支持 URL 不会显示在对话框中。

## <a name="see-also"></a>另请参阅
- [Mage.exe（清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [\<compatibleFrameworks> 元素](../deployment/compatibleframeworks-element-clickonce-deployment.md)
- [ClickOnce 和 Authenticode](../deployment/clickonce-and-authenticode.md)
- [应用程序部署必备](../deployment/application-deployment-prerequisites.md)