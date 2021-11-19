---
title: '指定详细日志文件 (ClickOnce部署) '
description: 了解如何为要维护的活动日志指定详细ClickOnce，以安装、初始化、更新和卸载 ClickOnce部署。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- logs, ClickOnce deployment
- ClickOnce deployment, logging
ms.assetid: 0807a28d-2e40-4a51-ab10-308d808ded6b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 6b7760aa8f7916d14b7d3f5ee03978f1e2d2193a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671812"
---
# <a name="how-to-specify-verbose-log-files-for-clickonce-deployments"></a>如何：指定 ClickOnce 部署的详细日志文件
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 维护所有部署的活动日志文件。 这些日志记录有关安装、初始化、更新和卸载部署 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 的详细信息。 若要增加写入这些日志文件的详细信息，请使用注册表编辑器 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] *(regedit.exe)* 指定详细级别。

> [!CAUTION]
> 如果不正确地使用注册表编辑器，可能会导致严重问题，这些问题可能需要重新安装操作系统。 请慎用注册表编辑器，风险自负。

 以下过程介绍如何为当前用户指定 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 日志文件详细级别。 若要降低详细级别，请删除此注册表值。

### <a name="to-specify-verbose-log-files"></a>指定详细日志文件

1. 打开 *Regedit.exe*。

2. 导航到 节点 **HKEY_CURRENT_USER\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment。**

3. 如有必要，请创建名为 的新字符串值 `LogVerbosityLevel` 。

4. 将 `LogVerbosityLevel` 值设置为 `1` 。

## <a name="see-also"></a>另请参阅
- [ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md)