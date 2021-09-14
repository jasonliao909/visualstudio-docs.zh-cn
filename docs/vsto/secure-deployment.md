---
title: 保护部署
description: 了解如何通过使用证书对解决方案进行签名，或者使用信任提示密钥来提供信任ClickOnce依据。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- deploying applications [Office development in Visual Studio], security
- Office development in Visual Studio, security
- Office applications [Office development in Visual Studio], security
- ClickOnce deployment [Office development in Visual Studio], security
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: df241aa2a2f67b18d11653ba016b39b561866bec
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602222"
---
# <a name="secure-deployment"></a>保护部署
  创建 Office解决方案时，开发计算机会自动更新，以允许项目中的代码运行。 但是，在部署解决方案时，必须通过使用证书或信任提示密钥对解决方案进行签名来提供信任决策 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 所基于的证据。 有关详细信息，请参阅[向解决方案授予Office信任](../vsto/granting-trust-to-office-solutions.md)。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 对于文档级自定义，如果将文档部署到网络位置，则还必须将文档的位置添加到 Office 应用程序的信任中心中的受信任位置列表。 若要详细了解如何在最终用户计算机上设置文档权限，请参阅 [向文档授予信任](../vsto/granting-trust-to-documents.md)。

## <a name="prevent-office-solutions-from-running-code"></a>阻止Office解决方案运行代码
 管理员可以使用注册表来阻止所有Office解决方案在计算机上运行。 打开Office代码扩展的解决方案时，Visual Studio Tools for Office运行时将检查计算机上是否存在具有以下注册表项之一下的名称 `Disabled` 条目：

- **HKEY_CURRENT_USER\Software\Microsoft\VSTO**

- **HKEY_LOCAL_MACHINE\Software\Microsoft\VSTO**

  若要防止Office运行代码，请在这两个注册表项下创建一个条目，并指定 以下数据类型和 `Disabled` 值之一 `Disabled` ：

- 设置为REG_SZ 0"REG_EXPAND_SZ字符串的字符串或字符串 (零) 。

- 设置为REG_DWORD 0 或零值 (值) 。

  若要Office运行代码，请同时将两个条目设置为 0 (零) 或删除 `Disabled` 注册表项。

## <a name="see-also"></a>另请参阅
- [部署Office解决方案](../vsto/deploying-an-office-solution.md)
- [准备计算机以运行或托管Office解决方案](/previous-versions/bb772092(v=vs.110))
- [安全Office解决方案](../vsto/securing-office-solutions.md)