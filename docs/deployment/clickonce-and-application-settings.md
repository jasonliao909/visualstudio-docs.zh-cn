---
title: ClickOnce 和应用程序设置 |Microsoft Docs
description: 了解应用程序设置文件如何在 ClickOnce 应用程序中工作，以及当用户升级到下一个版本时 ClickOnce 如何迁移设置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, application settings
ms.assetid: 891caba6-faef-4a3c-8f71-60e6fadb60eb
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 2e321f905e4bad8139705b8f9bcb6139c5d10a9c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671828"
---
# <a name="clickonce-and-application-settings"></a>ClickOnce 和应用程序设置
借助 Windows 窗体的应用程序设置，可轻松地在客户端创建、存储和维护自定义应用程序和用户首选项。 下列文档描述了应用程序设置文件如何在 ClickOnce 应用程序中工作，以及当用户升级到下一个版本时 ClickOnce 如何迁移设置。

 以下信息仅适用于默认应用程序设置提供程序，即 <xref:System.Configuration.LocalFileSettingsProvider> 类。 如果提供自定义提供程序，该提供程序将确定它如何存储其数据，以及如何在版本之间升级其设置。 有关应用程序设置提供程序的详细信息，请参阅[应用程序设置体系结构](/dotnet/framework/winforms/advanced/application-settings-architecture)。

## <a name="application-settings-files"></a>应用程序设置文件
 应用程序设置使用两个文件：\<app>.exe.config 和 user.config，其中“应用”是 Windows Forms 应用程序的名称。 user.config 是在应用程序第一次存储用户范围设置时在客户端上创建的。 相比之下，如果为设置定义默认值，\<app>.exe.config 将在部署之前存在。 使用 Visual Studio 的“发布”命令时，Visual Studio 将自动包含此文件。 如果使用 Mage.exe 或 MageUI.exe 创建 ClickOnce 应用程序，则必须确保在填充应用程序清单时，此文件包含在应用程序的其他文件中。

 在未使用 ClickOnce 部署的 Windows 窗体应用程序中，应用程序的 \<app>.exe.config 文件存储在应用程序目录中，而 user.config 文件存储在用户的“文档和设置”文件夹中。 在 ClickOnce 应用程序中，\<app>.exe.config 位于 ClickOnce 应用程序缓存内的应用程序目录中，而 user.config 位于该应用程序的 ClickOnce 数据目录中。

 无论如何部署应用程序，应用程序设置都可确保对 \<app>.exe.config 的安全读取访问，以及对 user.config 的安全读/写访问。

 在 ClickOnce 应用程序中，应用程序设置使用的配置文件的大小受到 ClickOnce 缓存大小的限制。 有关详细信息，请参阅 [ClickOnce 缓存概述](../deployment/clickonce-cache-overview.md)。

## <a name="version-upgrades"></a>版本升级
 正如 ClickOnce 应用程序的每个版本都独立于所有其他版本，ClickOnce 应用程序的应用程序设置也都独立于其他版本的设置。 当用户升级到应用程序的更高版本时，应用程序设置会将最新（编号最高）的版本的设置与随更新版本提供的设置进行比较，并将设置合并到一组新的设置文件中。

 下表介绍了应用程序设置如何决定要复制的设置。

|更改类型|升级操作|
|--------------------|--------------------|
|添加到 \<app>.exe.config 的设置|新设置合并到当前版本的 \<app>.exe.config|
|从 \<app>.exe.config 移除的设置|旧设置已从当前版本的 \<app>.exe.config 中移除|
|设置的默认值已更改；user.config 中的本地设置仍设置为原始默认值|设置合并到当前版本的 user.config，其中使用新的默认值作为值|
|设置的默认值已更改；在 user.config 中将设置设为非默认值|设置合并到当前版本的 user.config，其中保留非默认值|

如果已创建自己的应用程序设置包装类并想要自定义更新逻辑，可以重写 <xref:System.Configuration.ApplicationSettingsBase.Upgrade%2A> 方法。

## <a name="clickonce-and-roaming-settings"></a>ClickOnce 和漫游设置
 ClickOnce 不支持漫游设置，漫游设置允许设置文件跨网络计算机追随你。 如果需要漫游设置，则需要执行通过网络存储设置的应用程序设置提供程序，或开发自己的自定义设置类以在远程计算机上存储设置。 有关设置提供程序的详细信息，请参阅[应用程序设置体系结构](/dotnet/framework/winforms/advanced/application-settings-architecture)。

## <a name="see-also"></a>另请参阅
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)
- [应用程序设置概述](/dotnet/framework/winforms/advanced/application-settings-overview)
- [ClickOnce 缓存概述](../deployment/clickonce-cache-overview.md)
- [在 ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)