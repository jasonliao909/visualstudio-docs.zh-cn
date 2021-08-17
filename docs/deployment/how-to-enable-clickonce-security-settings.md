---
title: 启用 ClickOnce Security 设置 |Microsoft Docs
description: 了解发布向导如何自动为应用程序ClickOnce启用代码访问安全性。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122080619"
---
# <a name="how-to-enable-clickonce-security-settings"></a>如何：启用 ClickOnce 安全设置
必须启用ClickOnce应用程序的代码访问安全性才能发布应用程序。 使用发布向导发布应用程序时，会自动完成此操作。

 在某些情况下，启用代码访问安全性可能会影响生成或调试应用程序时的性能;在这些情况下，你可能希望暂时禁用安全设置。

 ClickOnce设计器 的"安全性"页上启用或禁用Project **安全设置**。 

### <a name="to-enable-clickonce-security-settings"></a>启用ClickOnce安全设置

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击“安全”选项卡。 

3. 选中“启用 ClickOnce 安全设置”  复选框。

     现在可以在"安全性"页上自定义应用程序的安全设置。

    > [!NOTE]
    > 每次使用发布向导发布应用程序时，都会自动选中 **此** 复选框。

### <a name="to-disable-clickonce-security-settings"></a>禁用ClickOnce安全设置

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击“安全”选项卡。 

3. 清除"**启用ClickOnce安全性设置** 复选框。

     应用程序将在完全信任的安全设置下运行;将忽略" **安全性"** 页上的任何设置。

    > [!NOTE]
    > 每次使用发布向导发布应用程序时，都会选中此复选框;每次发布成功后，必须再次清除它。

## <a name="see-also"></a>请参阅
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)
