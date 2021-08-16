---
title: 授予对文档的信任
description: 了解文档级项目的安全性要求如何与应用程序级项目相同，例如使用证书对清单进行签名或单击信任提示。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- security [Office development in Visual Studio], trust
- inclusion lists [Office development in Visual Studio], about inclusion lists
- trust [Office development in Visual Studio], 2007 Office system
- granting trust [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 0825b66bfa21df321232546a022f088f152281f1e34285ad04fedbbfcc6e10d1
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121352027"
---
# <a name="grant-trust-to-documents"></a>授予对文档的信任
  文档级项目与应用程序级项目具有相同的安全要求：使用证书对清单进行签名，或单击信任提示。 此外，文档或工作簿必须位于指定为受信任位置的目录中。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="trusted-locations"></a>受信任位置
 2010 Office 和 Office 中的应用程序具有信任中心，用户可以在信任中心配置安全和隐私设置，例如 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 受信任的位置。 对于 Office 解决方案，将本地计算机视为受信任的位置。 但是，由于具有较高风险，因此某些特定目录（如系统、用户和 Internet Explorer 的临时文件夹）也无法信任。

 有关信任中心的信息，请参阅[2010](/previous-versions/office/office-2010/cc178946(v=office.14))Office 中的安全性和策略和设置。 若要详细了解如何创建、管理、删除和配置受信任的文件夹，请参阅[在 2007 Office](/previous-versions/office/office-2007-resource-kit/cc178948(v=office.12))系统中配置受信任的位置和受信任的发布者设置，以及创建、删除或更改文件的受信任[位置](https://support.office.com/article/Create-remove-or-change-a-trusted-location-for-your-files-f5151879-25ea-4998-80a5-4208b3540a62)。

## <a name="security-considerations-for-office-solutions"></a>解决方案的安全Office注意事项
 在考虑将哪些文件夹添加到受信任的位置时，存在几个安全问题：

- 将本地文件夹视为较安全并且隐式受信任。 必须将远程位置（例如，文件共享）指定为受信任的位置。

- 当将某个目录添加到受信任的位置时，此操作将不仅向 Office 解决方案，还向 VBA 和 ActiveX 代码授予完全信任。 因此，不应将根目录我的文档文件夹指定为受信任文件夹。

- 尽管通过使用受信任的位置使文档本身受到信任，但仍需要其他权限来信任该自定义项。 通过使用使用证书对清单进行签名、单击信任提示或将 Office安装到 Program Files 目录，可以授予对自定义 *项* 的完全信任。

- 可以在与程序集相同或不同的目录中存储文档级解决方案的文档或工作薄。 例如，文档可以位于 SharePoint 服务器，而程序集可以位于网络文件共享中。 有关详细信息，请参阅如何：使用 SharePoint 将文档级 Office[解决方案发布到 ClickOnce。](/previous-versions/bb608595(v=vs.110))

## <a name="see-also"></a>另请参阅
- [向解决方案Office信任](../vsto/granting-trust-to-office-solutions.md)
- [解决方案Office故障排除](../vsto/troubleshooting-office-solution-security.md)
- [安全Office解决方案](../vsto/securing-office-solutions.md)