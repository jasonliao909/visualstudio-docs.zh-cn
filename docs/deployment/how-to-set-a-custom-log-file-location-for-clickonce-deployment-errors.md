---
title: " (ClickOnce 部署错误，请设置自定义日志文件位置) "
description: 了解 ClickOnce 为所有部署维护的激活日志文件，这些文件记录用于安装和初始化 ClickOnce 部署的错误。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
- ClickOnce deployment, error logging
ms.assetid: 77424414-7f0e-4b99-94bb-ea130de92d09
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 94786783ebc4ccf849af122b7c334f9543f72435
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122073820"
---
# <a name="how-to-set-a-custom-log-file-location-for-clickonce-deployment-errors"></a>如何：为 ClickOnce 部署错误设置一个自定义日志文件位置
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 维护所有部署的激活日志文件。 这些日志记录与安装和初始化部署有关的任何错误 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 默认情况下，将 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 为每个部署激活创建一个日志文件。 它将这些日志文件存储在临时 Internet Files 文件夹中。 发生激活失败时，会向用户显示部署的日志文件，并且用户在结果错误对话框中单击 " **详细信息** "。

 您可以使用注册表编辑器 (**regedit.exe**) 来设置自定义日志文件路径，从而更改特定客户端的此行为。 在这种情况下，会 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 将所有部署的激活成功和失败记录到一个文件中。

> [!CAUTION]
> 如果注册表编辑器使用不当，则可能会产生严重问题，导致重新安装操作系统。 请慎用注册表编辑器，风险自负。

> [!NOTE]
> 偶尔需要截断或删除日志文件，以防其增长过大。

 以下过程描述如何为单个客户端设置自定义日志文件位置。

### <a name="to-set-a-custom-log-file-location"></a>设置自定义日志文件位置

1. 打开 **Regedit.exe**。

2. 导航到节点 `HKCU\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment` 。

3. 将字符串值设置 `LogFilePath` 为首选自定义日志位置的完整路径和文件名。

     此位置必须在用户具有写入权限的目录中。 例如，在 Windows Vista 上，创建以下文件夹结构并将 `LogFilePath` 其设置为 *C:\Users \\ \<username> \Documents\Logs\ ClickOnce \installation.log*。

## <a name="see-also"></a>请参阅
- [ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md)