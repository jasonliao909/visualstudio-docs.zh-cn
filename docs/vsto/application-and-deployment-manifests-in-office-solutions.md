---
title: 解决方案中的应用程序和Office清单
description: 了解应用程序清单如何是一个 XML 文件，该文件提供应用程序解决方案Office查找和更新其程序集的信息。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- manifests [Office development in Visual Studio]
- deployment manifests [Office development in Visual Studio]
- application manifests [Office development in Visual Studio]
- assemblies [Office development in Visual Studio], updating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 17ff7893ddf4961f6271d4e6ebf285faeb771c528f52d7b5ff14c1147cd81097
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121299040"
---
# <a name="application-and-deployment-manifests-in-office-solutions"></a>解决方案中的应用程序和Office清单
  应用程序清单是一个 XML 文件，该文件提供由 Office 解决方案使用的信息来定位和更新其程序集。 应用程序清单可结合部署清单一起使用，部署清单是一个存储在服务器上的 XML 文件，提供定位最新版本的应用程序清单和程序集所需的信息。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="manifest-structure-for-office-solutions"></a>解决方案清单Office结构
 对于通过使用 Visual Studio 中的 Office 开发工具创建的 Microsoft Office 解决方案，所有清单都基于标准的 ClickOnce 架构。 在部署 Office 解决方案时，文档级和 VSTO 外接程序项目的应用程序清单都位于 ClickOnce 缓存。 部署清单不可复制到客户端计算机。

 有关项目的应用程序清单和部署清单Office，请参阅 Office[解决方案](../vsto/application-manifests-for-office-solutions.md)的应用程序清单和 Office[的部署清单](../vsto/deployment-manifests-for-office-solutions.md)。

## <a name="create-application-and-deployment-manifests"></a>创建应用程序和部署清单
 应用程序清单可作为生成过程的一部分自动创建。 每次生成文档级项目时，部署清单的位置就会作为自定义文档属性嵌入到该文档。 对于 VSTO 外接程序，部署清单的位置存储在注册表中。

 有关发布向导 **详细信息，** 请参阅使用 Office [部署ClickOnce。](../vsto/deploying-an-office-solution-by-using-clickonce.md)

 有关清单如何与解决方案Office，请参阅[部署Office解决方案](../vsto/deploying-an-office-solution.md)。

## <a name="see-also"></a>另请参阅

- [文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [设计和创建Office解决方案](../vsto/designing-and-creating-office-solutions.md)
- [解决方案的应用程序Office清单](../vsto/application-manifests-for-office-solutions.md)
- [解决方案部署Office清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)
- [ClickOnce部署清单](../deployment/clickonce-deployment-manifest.md)