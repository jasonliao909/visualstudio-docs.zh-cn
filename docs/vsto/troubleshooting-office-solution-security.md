---
title: 解决方案Office故障排除
description: 了解解决使用安全解决方案时可能会遇到的Microsoft Office提示。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: troubleshooting
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- security [Office development in Visual Studio], troubleshooting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 156494c507065d1c14fed9affe5a5ef2f592093e39625bd50fcbb505b6be2d6d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121330891"
---
# <a name="troubleshoot-office-solution-security"></a>解决方案Office故障排除
  本主题包含一些提示，用于解决使用安全解决方案时可能会遇到的Office问题。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="trusted-solutions-cannot-be-installed-from-restricted-sites"></a>无法从受限站点安装受信任的解决方案
 如果网站在受限站点区域中列出，则用户无法从 web 位置Internet Explorer解决方案。 即使使用受信任的证书对解决方案进行签名，也是如此。

 部署清单的 URL 可以分为五个区域之一：

- 我的电脑

- Internet

- 本地 Intranet

- 受信任的站点

- 受限制的站点

  如果部署清单的位置已分配给受限制的站点区域， [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 则 不安装解决方案。 如果位置已知且可信任，则用户可以从受限站点区域中删除该位置并安装解决方案。 若要了解如何管理区域，请参阅[配置ClickOnce发布者。](/previous-versions/dotnet/articles/ms996418(v=msdn.10))

## <a name="solutions-cannot-be-installed-from-network-file-shares-or-web-locations-when-internet-explorer-enhanced-security-configuration-or-internet-explorer-7-is-installed"></a>安装增强的安全配置或 Internet Explorer 7 时，无法从Internet Explorer或 Web 位置安装解决方案
 Internet Explorer Windows Server 2003 及更高版本以及 Internet Explorer 7 及更高版本中增强的安全配置 (IEESC) ，显著限制了用户浏览 Internet 的能力。 当用户尝试从网络文件共享或 Web 位置安装 Office 解决方案时，可能会收到以下错误消息："此应用程序中的自定义功能将不起作用，因为用于为 *SolutionName* 的部署清单签名的证书不可信。 请与管理员联系，寻求进一步的帮助。"

 使用 IEESC Internet Explorer 7 及更高版本时，如果部署清单的 URL 在 Internet 区域中分类，则清单必须具有来自受信任的发布者的证书，否则无法安装解决方案。 如果没有 IEESC，默认行为是提示最终用户做出信任决策。

 若要管理 IEESC 和 Internet Explorer 7 及更高版本的效果，请标识你信任的网站和通用命名约定 (UNC) 路径，并将其添加到受信任的安全区域之一 (本地 Intranet 或受信任的站点) 。若要了解如何管理区域，请参阅配置ClickOnce[发布者。](/previous-versions/dotnet/articles/ms996418(v=msdn.10))

## <a name="see-also"></a>另请参阅
- [安全Office解决方案](../vsto/securing-office-solutions.md)
- [Visual Studio 故障排除](/troubleshoot/visualstudio/welcome-visual-studio/)
