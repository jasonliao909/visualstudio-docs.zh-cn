---
title: 开发Office解决方案
description: 了解如何使用 Office 开发人员工具设计Visual Studio。 此外，了解如何开始在 UI (实现代码和) 。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, about developing solutions
- solutions [Office development in Visual Studio], developing
- Office solutions [Office development in Visual Studio], developing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: f9bc17fddd98132d95a994483afb3e3d3a6e6801
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122148267"
---
# <a name="develop-office-solutions"></a>开发Office解决方案
  使用 Visual Studio 中的 Office 开发人员工具设计项目并设置项目文件后，便可以开始集中精力实现代码和自定义用户界面 (UI)。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="office-solutions-programming-model"></a>Office解决方案编程模型
 Office 对象模型公开各种可以编程的对象。 每当使用托管代码进行 Office 解决方案编程，都将编写使用 Office 主互操作程序集中的类型的代码。 在使用 Visual Studio 中的 Office 项目模板创建的解决方案中，还编写直接针对项目中生成的类的代码。 有关详细信息，请参阅在解决方案[中Office代码](../vsto/writing-code-in-office-solutions.md)。

## <a name="program-different-types-of-office-solutions"></a>为不同类型的解决方案Office程序
 你正在创建的解决方案的类型确定你可以在项目中使用的功能。 例如，在设计时通过从 Visual Studio 中的 *“工具箱”* 拖放项，可以向文档级自定义项添加 Windows 窗体控件和扩展的 Office 控件（名为 **主机控件** ）。 但是，如果你正在开发一个 VSTO 外接程序，通过编写代码，可以在运行时仅将这些种类的控件添加到文档。

 有关特定于不同类型解决方案的功能的详细信息，请参阅以下主题：

- [程序VSTO外接程序](../vsto/programming-vsto-add-ins.md)。

- [对文档级自定义进行编程](../vsto/programming-document-level-customizations.md)。

- [Office UI 自定义 。](../vsto/office-ui-customization.md)

  有关帮助你规划项目解决方案Office过程的背景信息，请参阅设计和创建Office[解决方案](../vsto/designing-and-creating-office-solutions.md)。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[在解决方案中Office代码](../vsto/writing-code-in-office-solutions.md)|描述在 Office 解决方案中编写代码的各个方面。|
|[程序VSTO外接程序](../vsto/programming-vsto-add-ins.md)|提供对 VSTO 外接程序的编程模型和相关编程任务的概述。|
|[计划文档级自定义项](../vsto/programming-document-level-customizations.md)|提供对文档级自定义项的编程模型和相关编程任务的概述。|
|[OfficeUI 自定义](../vsto/office-ui-customization.md)|介绍可通过使用 VSTO 外接程序和文档级自定义项来自定义 Office 应用程序 UI 的不同方式。|
|[解决方案Office数据](../vsto/data-in-office-solutions.md)|介绍可以使用 Office 解决方案中的数据的不同方法，例如将数据绑定到控件和缓存文档级自定义项中的数据。|
|[自动保存如何影响Office解决方案](./how-autosave-impacts-office-solutions.md)|描述启用自动保存时Office解决方案所需的调整。|
|[解决方案Office疑难解答](../vsto/troubleshooting-office-solutions.md)|提供用于解决在创建 Office 解决方案时可能遇到的常见问题的提示。|
|[线程处理支持Office](../vsto/threading-support-in-office.md)|提供在 Office 解决方案中使用多个线程的概述。|
|[项目Office辅助功能](../vsto/accessibility-in-office-projects.md)|描述 Office 解决方案中可用的辅助功能。|

## <a name="see-also"></a>请参阅
- [如何：创建和修改自定义文档属性](../vsto/how-to-create-and-modify-custom-document-properties.md)
- [如何：读取和写入文档属性](../vsto/how-to-read-from-and-write-to-document-properties.md)
- [如何：面向Office多语言用户界面](../vsto/how-to-target-the-office-multilingual-user-interface.md)
- [演练：为 VSTO 创建第一个Excel](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md)
- [演练：为用户创建第一个文档级自定义Excel](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)
- [演练：为VSTO创建第一个Outlook](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md)
- [演练：为VSTO创建第一个PowerPoint](../vsto/walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)
- [演练：为VSTO创建第一个Project](../vsto/walkthrough-creating-your-first-vsto-add-in-for-project.md)
- [演练：为 Word VSTO第一个外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-word.md)
- [演练：为 Word 创建第一个文档级自定义项](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)
