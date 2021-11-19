---
title: 设置安全区域（ClickOnce 应用）
description: 了解如何设置 ClickOnce 应用程序的代码访问安全权限，从项目设计器中的基本权限集开始。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, security settings
- code access security, ClickOnce applications
- security zones, ClickOnce applications
ms.assetid: d3dac454-518a-44d7-a76e-ccb7b9c3a150
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 23ec1cae88ff1545118c92c3829f0d62962dc858
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665875"
---
# <a name="how-to-set-a-security-zone-for-a-clickonce-application"></a>如何：为 ClickOnce 应用程序设置安全区域
为 ClickOnce 应用程序设置代码访问安全权限时，需要在“项目设计器”  的“安全” 页上从基本权限集开始。

 在大多数情况下，还可以选择包含受限权限集的“Internet”  区域，或选择包含较大权限集的“本地 Intranet”  区域。 如果应用程序需要自定义权限，则可以通过选择“自定义”  安全区域实现该操作。 有关设置自定义权限的详细信息，请参阅 [如何：设置 ClickOnce 应用程序的自定义权限](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)。

### <a name="to-set-a-security-zone"></a>设置安全区域

1. 在“解决方案资源管理器” 中选择一个项目，然后在“项目”  菜单上单击“属性” 。

2. 单击“安全”选项卡。 

3. 选中“启用 ClickOnce 安全设置”  复选框。

4. 选择“这是部分可信的应用程序”  选项按钮。

     “ClickOnce 安全权限”  部分中的控件已启用。

5. 在“将要从中安装应用程序的区域”  下拉列表中，选择一个安全区域。

## <a name="see-also"></a>另请参阅
- [如何：设置 ClickOnce 应用程序的自定义权限](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)
