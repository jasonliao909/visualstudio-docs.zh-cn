---
title: 为 Office 解决方案设置配置信息
description: 了解如何使用配置文件来配置特定于 Microsoft Office 解决方案的设置。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], configuration files
- configuration files [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 1fd59fb61cf1d84c35bbcbbe406030318b8f57c6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122032701"
---
# <a name="how-to-set-up-configuration-information-for-an-office-solution"></a>如何：为 Office 解决方案设置配置信息
  您可以使用配置文件来配置特定于您的 Office 解决方案的设置。 可以指定设置，例如程序集绑定策略、远程处理对象、调试和跟踪设置。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-a-configuration-file-to-your-office-project"></a>将配置文件添加到 Office 项目中

1. 在 **“项目”** 菜单上，单击 **“添加新项”**。

2. 在 " **类别** " 窗格中，单击 " **常规**"。

3. 在 " **模板** " 窗格中，选择 " **应用程序配置文件**"。

4. 在 "**名称**" 框中，键入与程序集相同的名称以及扩展名 *.config*。例如，名为 *ExcelWorkbook1.dll* 的 Excel 项目程序集的配置文件将命名为 " *ExcelWorkbook1.dll.config*"。

5. 单击“添加”。

6. 根据应用程序配置文件架构创建配置文件。 有关详细信息，请参阅[.NET Framework 的配置文件架构](/dotnet/framework/configure-apps/file-schema/index)。

   将配置文件与 Office 项目一起使用时没有特别的注意事项。

## <a name="see-also"></a>请参阅
- [.NET Framework 的配置文件架构](/dotnet/framework/configure-apps/file-schema/index)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
