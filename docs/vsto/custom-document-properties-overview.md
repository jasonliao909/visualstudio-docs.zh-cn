---
title: 自定义文档属性概述
description: 了解在生成文档级项目时，Visual Studio向项目中的文档添加两个自定义属性。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], custom properties
- custom document properties
- document-level customizations [Office development in Visual Studio], custom properties
- Office documents [Office development in Visual Studio], custom properties
- _AssemblyLocation property
- _AssemblyName property
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: a7b8b30304ed840843818a4d576fdfdb49bc36b54e72f77f441e1d9864e876c0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121424432"
---
# <a name="custom-document-properties-overview"></a>自定义文档属性概述

生成文档级项目时，Visual Studio向项目中的文档添加两个自定义属性 \_ ：AssemblyLocation 和 \_ AssemblyName。 当用户打开文档时，Microsoft Office检查这些自定义文档属性。 如果文档中存在它们，应用程序将加载 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ，这将启动自定义。 有关详细信息，请参阅 Office[中的 Visual Studio](../vsto/architecture-of-office-solutions-in-visual-studio.md)体系结构。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="_assemblyname"></a>\_AssemblyName

此属性包含在 的解决方案加载程序组件Office接口的 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] CLSID。 CLSID 值为 4E3C66D5-58D4-491E-A7D4-64AF99AF6E8B。 切勿更改此值。

## <a name="_assemblylocation"></a>\_AssemblyLocation

此属性包含一个字符串，该字符串提供有关自定义项的部署清单的详细信息。 有关清单的更多信息，请参阅应用程序解决方案 中的应用程序和[Office清单](../vsto/application-and-deployment-manifests-in-office-solutions.md)。

 \_AssemblyLocation 属性值可以具有不同的格式，具体取决于解决方案的部署方式：

- 如果发布解决方案以从网站、UNC 路径或 CD 或 USB 驱动器安装，则 _AssemblyLocation 属性的格式为 *DeploymentManifestPath* | *SolutionID*。 以下字符串是一个示例：

     file://deployserver/MyShare/ExcelWorkbook1.vsto|74744e4b-e4d6-41eb-84f7-ad20346fe2d9

- 如果从 Visual Studio 运行或调试解决方案，则 _AssemblyLocation 属性的格式为 *DeploymentManifestName* | *SolutionID*|vstolocal。 以下字符串是一个示例：

     ExcelWorkbook1.vsto|74744e4b-e4d6-41eb-84f7-ad20346fe2d9|vstolocal

  *SolutionID* 是一个 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] GUID，用于标识解决方案。 生成项目时，会自动生成 *SolutionID。* **vstolocal** 术语向 指示应从文档相同的文件夹中 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 加载程序集。

## <a name="see-also"></a>另请参阅

- [Office 解决方案体系结构Visual Studio](../vsto/architecture-of-office-solutions-in-visual-studio.md)
- [文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)
- [解决方案中的应用程序和Office清单](../vsto/application-and-deployment-manifests-in-office-solutions.md)
- [如何：使用 Office 发布 ClickOnce](/previous-versions/bb386095(v=vs.110))
- [如何：创建和修改自定义文档属性](../vsto/how-to-create-and-modify-custom-document-properties.md)