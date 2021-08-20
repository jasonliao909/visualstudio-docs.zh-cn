---
title: 使用设计器禁用ClickOnce应用的 URL 激活
description: 了解如何使用 ClickOnce 为 ClickOnce Visual Studio 应用程序禁用自动启动，以便用户必须从 "开始"菜单。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- disallowURLActivation
- URL activation, ClickOnce applications
- ClickOnce deployment, URL activation
ms.assetid: a337a582-e67c-409a-b52e-607cd1a8fc57
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: b86b9ecd4ada8396f603af2555de11efd7d3c51e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122160655"
---
# <a name="how-to-disable-url-activation-of-clickonce-applications-by-using-the-designer"></a>如何：使用设计器禁用 ClickOnce 应用程序的 URL 激活
通常， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序在从 Web 服务器安装后立即自动启动。 出于安全原因，可以决定禁用此行为，并告知用户从"开始"菜单 **启动** 应用程序。 以下过程描述了如何禁用 URL 激活。

 此方法仅适用于从 Web 服务器安装到用户计算机上的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。 它不能用于仅联机应用程序，这些应用程序只能使用其 URL 启动。 有关仅联机应用程序与已安装应用程序之间差异详细信息，请参阅选择ClickOnce[部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)。

 此过程使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 也可使用 来完成此任务 [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] 。 有关详细信息，请参阅[如何：禁用](../deployment/how-to-disable-url-activation-of-clickonce-applications.md)应用程序应用程序的 URL ClickOnce激活。

## <a name="procedure"></a>过程

#### <a name="to-disable-url-activation-for-your-application"></a>禁用应用程序的 URL 激活的步骤

1. 右键单击项目中的项目 **解决方案资源管理器，然后单击**"属性 **"。**

2. 在" **属性"** 页上，单击" **发布"** 选项卡。

3. 单击“选项”。

4. 单击 **"清单"。**

5. 选中标记为"阻止通过 URL **激活应用程序"的复选框**。

6. 部署应用程序。

## <a name="see-also"></a>请参阅
- [发布ClickOnce应用程序](../deployment/publishing-clickonce-applications.md)