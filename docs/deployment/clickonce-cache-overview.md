---
title: ClickOnce 缓存概述 | Microsoft Docs
description: 了解 ClickOnce 应用程序缓存，其中包括存储 ClickOnce 应用程序的客户端计算机上的隐藏目录。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce deployemtn
- ClickOnce applications, cache
- ClickOnce deployment, cache
ms.assetid: e379921e-9ef1-4326-bbf3-53ba67925526
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: c88c3e641869e9f58111fee28742d0ebeaafd9ab
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671822"
---
# <a name="clickonce-cache-overview"></a>ClickOnce 缓存概述
所有 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序，无论是本地安装还是在线托管，都存储在客户端计算机上的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序缓存中。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 缓存是当前用户的“文档和设置”文件夹的“本地设置”目录下的一系列隐藏目录。 此缓存保存应用程序的所有文件，包括程序集、配置文件、应用程序和用户设置以及数据目录。 缓存还负责将应用程序的数据目录迁移到最新版本。 有关数据迁移的详细信息，请参阅在 [ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)。

 通过为应用程序存储提供单个位置，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 从用户那里接管了管理应用程序物理安装的任务。 缓存还可保留所有应用程序的程序集和数据文件及其彼此区别的不同版本，从而帮助隔离应用程序。 例如，在升级 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，该版本及其数据资源会在缓存中随其自己的目录一起提供。

## <a name="cache-storage-quota"></a>缓存存储配额
 在线托管的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序可占用的空间量受到配额限制，该配额限制了 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 缓存的大小。 缓存大小适用于用户的所有联机应用程序；一个部分受信任的联机应用程序仅可占用一半配额空间。 已安装的应用程序不受缓存大小限制，并且不计入缓存限制。 对于所有 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序，缓存仅保留当前版本和以前安装的版本。

 默认情况下，客户端计算机为联机 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序提供 250 MB 的存储空间。 数据文件不计入此限制。 系统管理员可通过更改注册表项 HKEY_CURRENT_USER\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment\OnlineAppQuotaInKB 来增加或减小特定客户端计算机上的此配额，该注册表项是一个 DWORD 值，以千字节表示缓存大小。 例如，为了将缓存大小减少到 50 MB，可将此值更改为 51200。

## <a name="see-also"></a>另请参阅
- [在 ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)