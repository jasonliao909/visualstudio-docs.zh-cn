---
title: ClickOnce缓存概述|Microsoft Docs
description: 了解应用程序ClickOnce缓存，其中包括存储这些应用程序ClickOnce的客户端计算机上的隐藏目录。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122051672"
---
# <a name="clickonce-cache-overview"></a>ClickOnce 缓存概述
所有 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序（无论是在本地安装还是联机托管）都存储在应用程序缓存 中的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 客户端计算机 *上*。 缓存是当前用户的 Documents 和 设置 文件夹的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] Local 设置 目录下的隐藏目录系列。 此缓存保存应用程序的所有文件，包括程序集、配置文件、应用程序和用户设置以及数据目录。 缓存还负责将应用程序的数据目录迁移到最新版本。 有关数据迁移详细信息，请参阅访问应用程序中的本地和[ClickOnce数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)。

 通过提供应用程序存储的单一位置， 将接管从用户 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 管理应用程序的物理安装的任务。 缓存还有助于隔离应用程序，因为所有应用程序的程序集和数据文件及其不同版本彼此独立。 例如，在升级应用程序时，该版本及其数据资源在缓存中随 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 自己的目录一起提供。

## <a name="cache-storage-quota"></a>缓存存储配额
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 联机托管的应用程序所占用的空间量受限于限制缓存大小的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配额。 缓存大小适用于用户的所有联机应用程序;单个部分受信任的联机应用程序只能占用配额空间的一半。 已安装的应用程序不受限于缓存大小，也不计入缓存限制。 对于 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 所有应用程序，缓存仅保留当前版本和以前安装的版本。

 默认情况下，客户端计算机为联机应用程序提供 250 MB [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 的存储。 数据文件不计入此限制。 系统管理员可以通过更改注册表项HKEY_CURRENT_USER\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment\OnlineAppQuotaInKB来扩大 **或** 减少特定客户端计算机上的此配额，这是表示缓存大小的 DWORD 值（以 KB 为单位）。 例如，为了将缓存大小减小到 50 MB，需要将此值更改为 51200。

## <a name="see-also"></a>请参阅
- [在 ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)