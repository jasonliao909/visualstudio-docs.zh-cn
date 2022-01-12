---
title: 包括必备组件（ClickOnce 应用）
description: 了解如何为开发计算机的 ClickOnce 应用程序获取要分发的必备组件安装程序包。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: c66bf0a5-8c93-4e68-a224-3b29ac36fe4d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: e0ad4c47a2bab3c10e67c21ba4c78af83590663e
ms.sourcegitcommit: dcecc0ed37b5e976b5dc83c5128ba5ecc8bc04b1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2022
ms.locfileid: "135750718"
---
# <a name="how-to-include-prerequisites-with-a-clickonce-application"></a>如何：将必备组件与 ClickOnce 应用程序包括在一起
你必须先将必备软件的安装程序包下载到开发计算机上，然后才能使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序分发这些软件。 发布应用程序并选择“从与我的应用程序相同的位置下载系统必备组件”时，如果安装程序包不在“包”文件夹中，则将发生错误。

> [!NOTE]
> 若要添加 .NET Framework 的安装程序包，请参阅 [.NET Framework 部署指南（针对开发人员）](/dotnet/framework/deployment/deployment-guide-for-developers)。

## <a name="to-add-an-installer-package-by-using-packagexml"></a><a name="Package"></a> 使用 Package.xml 添加安装程序包

1. 在文件资源管理器中，打开“包”文件夹。

    默认情况下，路径为 `%ProgramFiles(x86)%\Microsoft SDKs\ClickOnce Bootstrapper\Packages\`。

>[!NOTE]
> 从 Visual Studio 2019 Update 7 版本的引导程序包开始，还会在路径下发现 `<VS Install Path>\MSBuild\Microsoft\VisualStudio\BootstrapperPackages` 。

2. 为要添加的系统必备组件打开文件夹，然后为已安装的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 版本打开语言文件夹（例如，“en”用于英语）。

3. 在记事本中，打开“Package.xml”文件。

4. 找到包含 `http://go.microsoft.com/fwlink` 的“名称”元素，并复制该 URL。 包括“LinkID”部分。

   > [!NOTE]
   > 如果“名称”元素不包含“`http://go.microsoft.com/fwlink`”，则打开位于系统必备组件的根文件夹中的“Product.xml”文件并查找“fwlink”字符串  。

   > [!IMPORTANT]
   > 某些系统必备组件具有多个安装程序包（例如，用于 32 位或 64 位系统）。 如果多个“名称”元素包含“fwlink”，则必须对每个元素重复剩余步骤。

5. 将该 URL 粘贴到浏览器的地址栏中，然后在系统提示运行或保存时，选择“保存”。

    此步骤将安装程序文件下载到你的计算机中。

6. 将此文件复制到系统必备组件的根文件夹中。

    例如，对于 .NET Framework 4.7.2 必备组件，将文件复制到 \Packages\DotNetFX472 文件夹。

    现在你可以将安装程序包与你的应用程序一起分发。

## <a name="see-also"></a>另请参阅
- [如何：与 ClickOnce 应用程序一起安装系统必备组件](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)
