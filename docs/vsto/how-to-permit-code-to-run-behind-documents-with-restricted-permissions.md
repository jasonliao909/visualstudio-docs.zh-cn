---
title: 允许代码在具有受限权限的文档后面运行
description: 了解如何通过使用 Visual Studio 中的开发工具，允许代码在具有受限权限的文档Office运行。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Information Rights Management [Office development in Visual Studio]
- permissions [Office development in Visual Studio]
- IRM [Office development in Visual Studio]
- code [Office development in Visual Studio], running behind restricted documents
- documents [Office development in Visual Studio], restricted permissions
- Office documents [Office development in Visual Studio, restricted permissions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 366c8716995f0f5e88707d738957fc4ec0476a50
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602275"
---
# <a name="how-to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>如何：允许代码在具有受限权限的文档后面运行
  可以使用 Rights Management (的"Rights Management (IRM) "功能Microsoft Office限制对文档或工作簿的权限。 默认情况下，不允许运行受限 Microsoft Office Word 文档Microsoft Office Excel工作簿后面的代码。 可以更改默认值，以便托管代码扩展可以访问对象模型，解决方案将正常工作。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 你必须是文档或工作簿的作者，或者必须具有"完全控制"访问权限才能更改权限设置。

## <a name="to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>允许代码在具有受限权限的文档后面运行

1. 在 Word 或 Excel 中打开文档或Excel。

2. 单击"**文件"** 选项卡，指向 **"准备"，** 指向"**限制权限**"，然后单击"受限 **访问"。**

   > [!NOTE]
   > 首次使用时，系统会提示你安装Windows Rights Management客户端。 安装客户端后，可能需要重复这些步骤。

3. 在"**权限"** 对话框中，选择 **"限制对此文档的权限"，** 然后单击"**更多选项"。**

4. 在 **"用户的其他权限"下，** 选择 **"以编程方式访问内容"。**

   Word 或 Excel将允许以编程方式访问对象模型。

## <a name="see-also"></a>另请参阅
- [信息权限管理和托管代码扩展概述](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [文档级解决方案中的文档保护](../vsto/document-protection-in-document-level-solutions.md)
- [对文档Office密码保护](../vsto/password-protection-on-office-documents.md)
- [设计和创建Office解决方案](../vsto/designing-and-creating-office-solutions.md)
- [安全Office解决方案](../vsto/securing-office-solutions.md)
- [部署Office解决方案](../vsto/deploying-an-office-solution.md)
