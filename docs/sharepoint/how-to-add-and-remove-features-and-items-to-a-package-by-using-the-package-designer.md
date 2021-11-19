---
title: 包设计器：在包中添加与删除功能和项
titleSuffix: ''
description: 查看如何使用 Visual Studio 中的包设计器在 SharePoint 包中添加与删除功能和项。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.PackageDesignerDesign
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 946b3fca7e99bf2aaf1395d63f13626f5e5e5859
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600618"
---
# <a name="how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer"></a>如何：使用包设计器在包中添加与删除功能和项
  创建 SharePoint 解决方案时，Visual Studio 会将默认 SharePoint 功能添加到解决方案中的包。 在最终部署之前，可以添加和删除 SharePoint 项目项和功能，以修改 SharePoint 包。

 或者，你可以使用“打包资源管理器”添加和删除 SharePoint 项目项。 还可以查看和更改放置到包 (.wsp) 的 SharePoint 项目项和功能的层次结构。 有关详细信息，请参阅[如何：使用打包资源管理器在包中添加和删除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)。

## <a name="add-features-to-a-sharepoint-package"></a>向 SharePoint 包添加功能
 你可以使用包设计器将功能添加到 SharePoint 包。

#### <a name="to-add-sharepoint-features-with-the-package-designer"></a>使用包设计器添加 SharePoint 功能

1. 打开“包设计器”。

    有关详细信息，请参阅[如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)。

2. 通过执行以下一个或多个步骤来添加一个或多个 SharePoint 功能：

   1. 双击“解决方案项”列表中要添加的每个项。

   2. 选择要添加的项，然后选择“添加”按钮 (>)。

   3. 选择“全部添加”按钮 (>>)，一次添加所有项。

      例如，可以双击“解决方案项”列表中的某个项，将其添加到“包项”列表。

      SharePoint 项目项和功能会显示在“包项”列表中。

## <a name="remove-features-from-a-sharepoint-package"></a>从 SharePoint 包中删除功能
 可以使用包设计器删除 SharePoint 包中的功能。

#### <a name="to-remove-sharepoint-features-with-the-package-designer"></a>使用包设计器删除 SharePoint 功能

1. 在“包项”列表中，选择要删除的项，然后选择“删除”(<) 按钮，或选择“全部删除”按钮(<<) 删除所有项。

     SharePoint 项显示在“解决方案项”列表中。

## <a name="see-also"></a>另请参阅
- [创建 SharePoint 解决方案包](../sharepoint/creating-sharepoint-solution-packages.md)
- [如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [如何：创建包](/previous-versions/ee231585(v=vs.110))