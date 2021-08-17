---
title: 创建本地化的引导程序包 |Microsoft Docs
description: 了解如何通过为每个区域设置创建两个文件，在 ClickOnce 中创建引导程序包的本地化版本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- localized bootstrapper packages
- dependencies, creating localized bootstrapper packages
- prerequisites, creating localized bootstrapper packages
ms.assetid: 66a1bc7e-6540-4164-963d-557196a69d8a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 95b1d4e68f6508751d79fab2970d79cb74577e55
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122090000"
---
# <a name="how-to-create-a-localized-bootstrapper-package"></a>如何：创建本地化的引导程序包
创建引导程序包后，您可以通过为每个区域设置创建两个文件来创建每个区域设置的本地化版本的引导程序包：软件许可条款文件 (例如 *eula*) 和包清单 (*package.xml*) 。

 默认情况下，Visual Studio 2010 只包括 .NET Framework 4、.NET Framework 4 Client Profile、F# Runtime 2.0 和 F# Runtime 4.0 的本地化引导程序包。 你可以通过完成三步操作来为其他引导程序创建本地化包。

1. 在 \Program 文件中创建一个名为的文件夹， *(x86) \microsoft sdk \ ClickOnce Bootstrapper\Packages \\ \<BootstrapperPackageName>* 的区域名称。

2. 创建包含引导程序包的软件许可条款的文件并将其放入新的文件夹中。

3. 创建名为 *package.xml* 的包清单，更新字符串和区域性，然后将该文件放入新文件夹。 如果已创建了目标语言中 Visual Studio 的引导程序，则可以复制 Visual Studio *package.xml* 文件，并在此步骤中修改它。

> [!NOTE]
> 如果使用安装项目来部署应用程序，则可以通过更改“本地化”属性来本地化应用程序。

 [!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-a-localized-bootstrapper-package"></a>创建本地化的引导程序包

1. 创建以区域设置名称命名的文件夹。

     在32位计算机上，在 *\Program Files\Microsoft sdk \ \\ \<BootstrapperPackageName> \\ ClickOnce Bootstrapper\Packages* 文件夹中创建文件夹。

     在64位计算机上， *(x86) \microsoft sdk \ \\ \<BootstrapperPackageName> \\ ClickOnce Bootstrapper\Packages* 文件夹中的 \Program 文件中创建文件夹。

     下表显示可以用来匹配区域设置的文件夹名称。

    |Locale|文件夹名称|
    |------------|-----------------|
    |中文(简体)|zh-Hans|
    |中文(繁体)|zh-Hant|
    |捷克语|cs|
    |德语|de|
    |英语|en|
    |西班牙语|es|
    |法语|fr|
    |意大利语|it|
    |朝鲜语|ko|
    |日语|ja|
    |波兰语|pl|
    |葡萄牙语(巴西)|pt-BR|
    |俄语|ru|
    |土耳其语|tr|

2. 创建包含引导程序包的软件许可条款的文件并将其放入新的文件夹中。

3. 创建名为 package.xml 的包清单并将其放入新的文件夹中。 有关详细信息，请参阅 [如何：创建包清单](../deployment/how-to-create-a-package-manifest.md)。

4. 更新包清单的 `<Strings>` 部分，使字符串以正确的区域设置语言表示。

5. 更改 `<String Name="Culture">` 值以匹配文件夹名称。

6. 保存 *package.xml* 文件。

### <a name="to-create-a-bootstrapper-package-for-net-framework-35-service-pack-1-localized-in-french"></a>为用法语本地化的 .NET Framework 3.5 Service Pack 1 创建引导程序包

1. 创建名为 fr 的文件夹。 该文件夹名称必须与区域设置名称匹配。

     在32位计算机上，在 *\Program Files\Microsoft sdk \ ClickOnce Bootstrapper\Packages\DotNetFX35SP1 \\* 文件夹中创建文件夹。

     在64位计算机上， *(x86) \microsoft sdk \ ClickOnce Bootstrapper\Packages\DotNetFX35SP1 \\* 文件夹中的 \Program 文件中创建文件夹。

2. 将软件许可条款的本地化版本置于 *fr* 文件夹中。

3. 将 *(x86) \microsoft sdk \ ClickOnce Bootstrapper\Packages\DotNetFX35SP1\en\package.xml* 文件中的 \Program 文件复制到 *fr* 文件夹，然后在 XML 设计器中打开该文件。

4. 更新包清单的 `<Strings>` 部分，以便用法语表示错误字符串。

5. 将 `<String Name="Culture">` 值更改为 *fr*。

6. 保存 *package.xml* 文件。

>[!NOTE]
> 从 Visual Studio 2019 Update 7 版本的引导程序包开始，还会在路径 *<VS Install Path> \ MSBuild \Microsoft\VisualStudio\BootstrapperPackages* 下发现。

## <a name="see-also"></a>请参阅
- [创建引导程序包](../deployment/creating-bootstrapper-packages.md)
- [应用程序部署必备](../deployment/application-deployment-prerequisites.md)
- [如何：创建程序包清单](../deployment/how-to-create-a-package-manifest.md)