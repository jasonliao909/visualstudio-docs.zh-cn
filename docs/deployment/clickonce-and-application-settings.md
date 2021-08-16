---
title: ClickOnce和应用程序设置 |Microsoft Docs
description: 了解应用程序设置文件在应用程序ClickOnce工作，以及ClickOnce升级到下一版本时如何迁移设置。
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
ms.openlocfilehash: 6449a74a8649fa97ac4ff55cf57ea855892ba50baa9debacd064a39ffb70059d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121404005"
---
# <a name="clickonce-and-application-settings"></a>ClickOnce 和应用程序设置
使用 Windows 窗体的应用程序设置，可以轻松在客户端上创建、存储和维护自定义应用程序和用户首选项。 以下文档介绍了应用程序设置文件在 ClickOnce 中如何工作，以及ClickOnce升级到下一版本时如何迁移设置。

 以下信息仅适用于默认应用程序设置提供程序 类 <xref:System.Configuration.LocalFileSettingsProvider> 。 如果提供自定义提供程序，该提供程序将确定它如何存储其数据，以及如何在版本之间升级其设置。 有关应用程序设置提供程序详细信息，请参阅 [应用程序设置体系结构](/dotnet/framework/winforms/advanced/application-settings-architecture)。

## <a name="application-settings-files"></a>应用程序设置文件
 应用程序设置使用两个文件 *\<app> ：.exe.config* 和 *user.config，* 其中 *app* 是 Windows Forms 应用程序的名称。 *user.config* 应用程序首次存储用户范围的设置时，在客户端上创建一个。 *\<app>.exe.config，* 如果为设置定义默认值，则部署前将存在此参数。 Visual Studio发布命令时，**将自动包含此文件**。 如果使用 ClickOnce 或Mage.exe创建MageUI.exe应用程序，则必须确保在填充应用程序清单时，此文件包含在应用程序的其他文件中。

 在使用 ClickOnce 部署的 Windows Forms 应用程序中，应用程序的 *\<app>.exe.config* 文件存储在应用程序目录中，而 *user.config* 文件存储在用户的 Documents 和 **设置 文件夹中**。 在 ClickOnce 应用程序中 *\<app> ，.exe.config* 位于 ClickOnce 应用程序缓存内的应用程序目录中，user.config位于该应用程序的 ClickOnce 数据目录中。 

 无论如何部署应用程序，应用程序设置都可确保对.exe.config进行安全的 *\<app>* 读取访问，以及对应用程序的安全读/*写user.config。*

 在ClickOnce应用程序中，应用程序设置使用的配置文件的大小受应用程序缓存ClickOnce大小。 有关详细信息，请参阅缓存[ClickOnce概述](../deployment/clickonce-cache-overview.md)。

## <a name="version-upgrades"></a>版本升级
 正如应用程序的每个版本ClickOnce与所有其他版本隔离一样，ClickOnce应用程序的应用程序设置也与其他版本的设置隔离。 当用户升级到应用程序的更高版本时，应用程序设置会将最新的 (编号最高的) 版本的设置与更新版本提供的设置进行比较，并将设置合并到一组新的设置文件中。

 下表介绍了应用程序设置如何决定要复制的设置。

|更改类型|升级操作|
|--------------------|--------------------|
|添加到 *\<app>.exe.config*|新设置将合并到当前版本的 *\<app>.exe.config*|
|已从 *\<app> 中删除.exe.config*|旧设置将从当前版本的版本 *\<app> 中删除.exe.config*|
|设置的默认已更改;本地设置仍设置为原始 *默认设置user.config*|设置将合并到当前版本的 *user.config，使用* 新的默认值作为值|
|设置的默认已更改;将 设置为非 *默认值user.config*|设置将合并到当前版本的 *user.config，并* 保留非默认值|

如果已创建自己的应用程序设置包装类并想要自定义更新逻辑，可以重写 <xref:System.Configuration.ApplicationSettingsBase.Upgrade%2A> 方法。

## <a name="clickonce-and-roaming-settings"></a>ClickOnce和漫游设置
 ClickOnce漫游设置不起作用，这允许设置文件在网络中跨计算机跟随你。 如果需要漫游设置，则需要实现通过网络存储设置的应用程序设置提供程序，或开发自己的自定义设置类以在远程计算机上存储设置。 有关设置提供程序中详细信息，请参阅 [应用程序设置体系结构](/dotnet/framework/winforms/advanced/application-settings-architecture)。

## <a name="see-also"></a>请参阅
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)
- [应用程序设置概述](/dotnet/framework/winforms/advanced/application-settings-overview)
- [ClickOnce 缓存概述](../deployment/clickonce-cache-overview.md)
- [在 ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)