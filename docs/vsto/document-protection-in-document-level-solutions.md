---
title: 文档级解决方案中的文档保护
description: 了解如何在文档级项目中使用 Microsoft Office Word 和 Microsoft Office Excel 的保护功能。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602296"
---
# <a name="document-protection-in-document-level-solutions"></a>文档级解决方案中的文档保护
  可以在文档级项目中使用 Microsoft Office Word 和 Microsoft Office Excel 的保护功能。 这些功能阻止未经授权的用户对文档的受保护部分进行更改。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 使用 Excel，可以在设计器中打开工作簿时启用和关闭保护。 使用 Word，只能在设计器外部启用保护。 运行时，可以编程方式启用或禁用 Word 和 Excel。

 在设计器中打开的文档上启用文档保护时，所有控件将从"工具箱"中删除或变为不可用，并且无法将任何内容从"数据源"窗口拖动到文档。

## <a name="serverdocument-and-protected-documents"></a>ServerDocument 和受保护的文档
 如果文档受保护，则不能从文档外部访问数据缓存。 不能使用 类检索或操作在受保护文档中缓存的数据，也不能使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类的其他 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 方法。

## <a name="word-document-protection-in-the-designer"></a>设计器中的 Word 文档保护
 如果在 Word 文档或模板打开时向它添加保护Visual Studio，则不能开始在设计器中强制实施保护。 文档在打开时位于设计模式Visual Studio，并且必须位于运行模式下，然后才能开始强制实施保护。

 但是，如果创建使用已启用保护的现有 Word 文档的项目，则文档在设计器中打开时受到保护。 无法编辑文档的受保护部分，但仍可以在代码编辑器中编写代码以自动执行文档。 如果在打开文档时启用了保护，则也不能生成Visual Studio。

 可以在设计器中打开文档时关闭保护，以便编辑文档并生成项目。 在调试时，不能在设计器中关闭对副本的保护;在调试期间打开的文档是独立于设计器中打开的文档 (输出副本存储在 Visual Basic 的 *\bin* 目录中，而 *\bin\debug* 目录存储于 C# ) 。

 可以通过关闭 Visual Studio 中的项目、打开项目目录中的文档副本并启用保护，对在设计器中打开的文档副本启用保护。

## <a name="enforce-word-document-protection-on-build"></a>在生成时强制实施 Word 文档保护
 Visual Studio在生成过程中开始对 Word 文档和模板强制实施保护，以便当打开文档进行调试时启用保护。 文档使用空密码进行保护。

 在生成期间启用保护，以便如果文档事件存在可能导致异常或更改应用程序行为的代码，可以正确 <xref:Microsoft.Office.Tools.Word.Document.Startup> 调试此代码。 如果在打开文档后启用保护，将无法调试或测试初始化代码。

## <a name="setting-the-password"></a>设置密码
 Visual Studio自动启用保护，但默认情况下不提供密码。 如果希望文档保护具有密码，则必须在部署解决方案之前添加它。 添加密码可让授权用户从文档中删除保护;如果没有密码，则无法轻松删除保护。 有关设置密码的详细信息，请参阅特定应用程序Office帮助。

## <a name="see-also"></a>另请参阅
- [如何：以编程方式保护文档和文档的某些部分](../vsto/how-to-programmatically-protect-documents-and-parts-of-documents.md)
- [Office开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [信息权限管理和托管代码扩展概述](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [对文档Office密码保护](../vsto/password-protection-on-office-documents.md)
- [如何：允许代码在具有受限权限的文档后面运行](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)
- [设计和创建Office解决方案](../vsto/designing-and-creating-office-solutions.md)
