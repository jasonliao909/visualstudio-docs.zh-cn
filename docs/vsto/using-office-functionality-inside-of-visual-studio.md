---
title: 在 Office 内使用Visual Studio
description: 了解如何在文档级项目中托管文档和关联的应用程序Visual Studio以便可以直接处理文档。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- security [Office development in Visual Studio], document protection
- Office applications [Office development in Visual Studio]
- Office functionality inside Visual Studio
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: ee597766c9444b837ff0abe29146b0373264906e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122046225"
---
# <a name="use-office-functionality-inside-of-visual-studio"></a>在 Office 内使用Visual Studio
  创建文档级项目时，文档和关联的应用程序托管在 Visual Studio以便可以直接设计和处理文档。 当应用程序Microsoft Office打开时Visual Studio，它通常可以正常工作。 但是，应用程序的一些功能不同或不可访问。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="document-protection"></a>文档保护
 Microsoft OfficeWord 和 Microsoft Office Excel 提供了可在项目中使用的文档保护功能。 但是，如果在打开文档时启用了文档保护Visual Studio，则可能会阻止进行一些设计更改。 有关详细信息，请参阅文档 [级解决方案 中的文档保护](../vsto/document-protection-in-document-level-solutions.md)。

## <a name="information-rights-management"></a>信息权限管理
 有关 Rights Management (IRM) 的信息，请参阅 Microsoft Office Word 和 Microsoft Office Excel。 IRM 可帮助防止未经授权的人员查看或更改敏感信息。 但是，IRM 还可以阻止代码运行。 有关详细信息，请参阅信息 [权限管理和托管代码扩展概述](../vsto/information-rights-management-and-managed-code-extensions-overview.md)。

## <a name="password-protection"></a>密码保护
 Microsoft Office可以设置Microsoft Office Excel文档和工作簿，以便不知道密码的人无法打开它们。 密码保护在 Word 和 Excel处理方式不同，可能会影响开发过程。 有关详细信息，请参阅文档 上的[Office保护](../vsto/password-protection-on-office-documents.md)。

## <a name="see-also"></a>请参阅
- [文档级解决方案中的文档保护](../vsto/document-protection-in-document-level-solutions.md)
- [信息权限管理和托管代码扩展概述](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [对文档Office密码保护](../vsto/password-protection-on-office-documents.md)
- [如何：在不Office的情况下打开解决方案](../vsto/how-to-open-office-solutions-without-running-code.md)
