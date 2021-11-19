---
title: 启用 ClickOnce 安全设置 | Microsoft Docs
description: 了解发布向导如何自动启用 ClickOnce 应用程序的代码访问安全性，以便发布应用程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- security [Visual Studio], ClickOnce applications
- ClickOnce deployment, security settings
- security settings, ClickOnce deployment
ms.assetid: 73cd3e9d-cd72-4ad2-8cae-94d6bb6b01e0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: b534d18deeb63cad6cb0df967915e4fde968c688
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602519"
---
# <a name="how-to-enable-clickonce-security-settings"></a>如何：启用 ClickOnce 安全设置
若要发布应用程序，必须启用 ClickOnce 应用程序的代码访问安全性。 使用发布向导发布应用程序时，会自动执行此操作。

 在某些情况下，启用代码访问安全性会影响生成或调试应用程序时的性能；在这些情况下，你可能希望暂时禁用安全设置。

 可以在“项目设计器”的“安全”页上启用或禁用 ClickOnce 安全设置。

### <a name="to-enable-clickonce-security-settings"></a>启用 ClickOnce 安全设置

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击“安全”选项卡。 

3. 选中“启用 ClickOnce 安全设置”  复选框。

     现在可以在“安全”页上为你的应用程序自定义安全设置。

    > [!NOTE]
    > 每次用“发布”向导发布应用程序时，都将自动选中此复选框。

### <a name="to-disable-clickonce-security-settings"></a>禁用 ClickOnce 安全设置

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击“安全”选项卡。 

3. 清除“启用 ClickOnce 安全设置”复选框。

     应用程序将以完全信任安全设置运行；“安全”页上的所有设置都将被忽略。

    > [!NOTE]
    > 每次用“发布”向导发布应用程序时，都将选中此复选框；你必须在每次成功发布后再次将其清除。

## <a name="see-also"></a>另请参阅
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)
