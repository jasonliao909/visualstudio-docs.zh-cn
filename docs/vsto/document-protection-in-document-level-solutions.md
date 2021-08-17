---
title: 文档级解决方案中的文档保护
description: 了解如何使用文档级项目中 Microsoft Office Word 和 Microsoft Office Excel 的保护功能。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- restricted permissions [Office development in Visual Studio]
- permissions [Office development in Visual Studio]
- workbooks [Office development in Visual Studio], restricted permissions
- Office documents [Office development in Visual Studio], restricted permissions
- documents [Office development in Visual Studio], restricted permissions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: cc11241057a32d24746eb9eabbc6a7b6526c9eaa
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122026468"
---
# <a name="document-protection-in-document-level-solutions"></a>文档级解决方案中的文档保护
  您可以使用文档级项目中 Microsoft Office Word 和 Microsoft Office Excel 的保护功能。 这些功能会阻止未经授权的用户更改文档的受保护部分。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 使用 Excel，可以在设计器中打开工作簿时打开和关闭保护。 使用 Word，只能在设计器外部打开保护。 在运行时，可以通过编程方式为 Word 和 Excel 启用或禁用保护。

 在设计器中打开的文档上启用文档保护时，将从 " **工具箱** " 中删除所有控件或使其不可用，您不能将任何内容从 " **数据源** " 窗口拖动到文档中。

## <a name="serverdocument-and-protected-documents"></a>ServerDocument 和受保护文档
 如果文档受到保护，则无法从文档外部访问数据缓存。 不能使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类来检索或操作缓存在受保护文档中的数据，也不能使用类的其他方法 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 。

## <a name="word-document-protection-in-the-designer"></a>设计器中的 Word 文档保护
 如果在 Visual Studio 中打开 Word 文档或模板时向其中添加保护，则无法在设计器中开始强制执行保护。 文档在 Visual Studio 中打开时处于设计模式，并且它必须处于运行模式，然后才能开始强制保护。

 但是，如果您创建一个项目，该项目使用启用了保护的现有 Word 文档，则该文档将在设计器中打开时受到保护。 您无法编辑文档的受保护部分，但您仍可以在代码编辑器中编写代码以自动执行文档。 如果在 Visual Studio 中打开文档时启用了保护，也无法生成项目。

 在设计器中打开文档时，可以关闭保护，以便可以编辑文档和生成项目。 在调试时，无法在设计器中关闭对副本的保护;在调试过程中打开的文档是与设计器中打开的副本不同的副本 (输出副本存储在用于 Visual Basic 的 *\bin* 目录中，后者 ) 的 *\bin\debug* 目录。

 您可以通过在 Visual Studio 中关闭项目，打开项目目录中的文档副本，然后打开保护，在设计器中打开的文档的副本上启用保护。

## <a name="enforce-word-document-protection-on-build"></a>在生成时强制执行 Word 文档保护
 Visual Studio 在生成过程中开始对 Word 文档和模板进行保护，以便在打开文档进行调试时启用保护。 文档使用空密码进行保护。

 在生成过程中启用保护，因此，如果文档事件中有 <xref:Microsoft.Office.Tools.Word.Document.Startup> 可能导致异常或更改应用程序行为的代码，则可以正确调试此代码。 如果在打开文档后启用保护，则无法调试或测试初始化代码。

## <a name="setting-the-password"></a>设置密码
 Visual Studio 会自动启用保护，但默认情况下不提供密码。 如果希望文档保护具有密码，则必须在部署解决方案之前添加密码。 通过添加密码，你可以允许授权用户从文档中删除保护;如果没有密码，则无法轻松删除保护。 有关设置密码的详细信息，请参阅特定 Office 应用程序中的帮助。

## <a name="see-also"></a>请参阅
- [如何：以编程方式保护文档和文档的某些部分](../vsto/how-to-programmatically-protect-documents-and-parts-of-documents.md)
- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [信息权限管理和托管代码扩展概述](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [Office 文档的密码保护](../vsto/password-protection-on-office-documents.md)
- [如何：允许代码在具有受限权限的文档的后台运行](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
