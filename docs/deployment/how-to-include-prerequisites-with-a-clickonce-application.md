---
title: '包括应用 (ClickOnce的先决条件) '
description: 了解如何获取安装程序包，了解为开发计算机分发ClickOnce应用程序的先决条件。
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
ms.openlocfilehash: dae657a35a2fffba23a353f20d2f36a9296fb3c1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122146376"
---
# <a name="how-to-include-prerequisites-with-a-clickonce-application"></a>如何：将必备组件与 ClickOnce 应用程序包括在一起
你必须先将必备软件的安装程序包下载到开发计算机上，然后才能使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序分发这些软件。 发布应用程序并选择“从与我的应用程序相同的位置下载系统必备组件”时，如果安装程序包不在“包”文件夹中，则将发生错误。

> [!NOTE]
> 若要为开发人员添加安装程序.NET Framework，请参阅[.NET Framework开发人员部署指南](/dotnet/framework/deployment/deployment-guide-for-developers)。

## <a name="to-add-an-installer-package-by-using-packagexml"></a><a name="Package"></a> 使用 Package.xml 添加安装程序包

1. 在文件资源管理器中，打开“包”文件夹。

    默认情况下，路径为 `%ProgramFiles(x86)%\Microsoft SDKs\ClickOnce Bootstrapper\Packages\` 。

>[!NOTE]
> 从 2019 Visual Studio 2019 Update 7 版本引导程序包开始，还会在 *<VS Install Path> 路径 \MSBuild\Microsoft\VisualStudio\BootstrapperPackages* 下发现。

2. 为要添加的系统必备组件打开文件夹，然后为已安装的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 版本打开语言文件夹（例如，“en”用于英语）。

3. 在记事本中，打开“Package.xml”文件。

4. 找到 **包含 的 Name** 元素 `http://go.microsoft.com/fwlink` ，并复制 URL。 包括“LinkID”部分。

   > [!NOTE]
   > 如果没有 **Name** 元素包含 ，请打开Product.xml根文件夹中的 `http://go.microsoft.com/fwlink` fwlink 文件并找到 **fwlink** 字符串。 

   > [!IMPORTANT]
   > 某些系统必备组件具有多个安装程序包（例如，用于 32 位或 64 位系统）。 如果多个“名称”元素包含“fwlink”，则必须对每个元素重复剩余步骤。

5. 将该 URL 粘贴到浏览器的地址栏中，然后在系统提示运行或保存时，选择“保存”。

    此步骤将安装程序文件下载到你的计算机中。

6. 将此文件复制到系统必备组件的根文件夹中。

    例如，对于 .NET Framework 4.7.2 先决条件，将文件复制到 *\Packages\DotNetFX472* 文件夹。

    现在你可以将安装程序包与你的应用程序一起分发。

## <a name="see-also"></a>请参阅
- [如何：使用应用程序安装ClickOnce先决条件](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)
