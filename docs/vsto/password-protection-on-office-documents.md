---
title: 对文档Office密码保护
description: 了解如何在文档和工作簿Microsoft Word设置Excel密码，以便未经授权的用户无法打开它们。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- permissions [Office development in Visual Studio]
- workbooks [Office development in Visual Studio], restricted permissions
- passwords [Office development in Visual Studio], document protections
- documents [Office development in Visual Studio], restricted permissions
- Office documents [Office development in Visual Studio, restricted permissions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 80e89d5907fca8d4896ba0349bf26b527c11b1cd
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122099602"
---
# <a name="password-protection-on-office-documents"></a>对文档Office密码保护
  可以在 Word 文档和工作簿上Microsoft Office密码Microsoft Office Excel，以便不知道密码的人无法打开这些工作簿。 此选项在打开 时 **称为密码**。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 可以使用已启用"打开时密码"的现有文档和工作簿 **创建文档级** 项目。 对于启用了"打开Visual Studio"的 Word 和Excel文档，此 **行为** 有所不同。

 有关在打开时 **启用密码的信息，** 请参阅 Word 或 Excel。

## <a name="behavior-of-excel-and-word"></a>Excel和 Word 的行为
 每次在启用了"打开Excel密码Visual Studio **打开** 工作簿时，Excel提示输入密码。 生成解决方案时，系统会再次提示输入密码，因为文档在生成期间打开。

 首次在启用了"打开时Visual Studio打开 Word 文档时，Word 会提示输入密码。  成功输入密码后，" **打开时** 的密码"将从文档中删除，打开文档不再需要密码。 如果希望解决方案中的文档在打开之前需要密码，则必须在最终生成后和部署解决方案之前启用"打开密码"。

## <a name="see-also"></a>请参阅
- [文档级解决方案中的文档保护](../vsto/document-protection-in-document-level-solutions.md)
- [信息权限管理和托管代码扩展概述](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [如何：允许代码在具有受限权限的文档后面运行](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)
- [设计和创建Office解决方案](../vsto/designing-and-creating-office-solutions.md)
