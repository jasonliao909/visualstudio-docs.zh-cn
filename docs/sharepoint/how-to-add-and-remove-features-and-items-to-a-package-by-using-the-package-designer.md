---
title: 包设计器：添加&删除要打包的功能和项
titleSuffix: ''
description: 查看如何使用包设计器在 SharePoint 包包中添加和删除功能和Visual Studio。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122026962"
---
# <a name="how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer"></a>如何：使用包设计器向包添加和删除功能和项
  创建解决方案SharePoint，Visual Studio将默认SharePoint功能添加到解决方案中的包。 在最终部署之前，可以添加和删除SharePoint项和功能，以修改SharePoint包。

 或者，可以使用打包资源管理器添加和删除SharePoint项。 还可以查看和更改项目项的层次结构SharePoint以及放入包 (.wsp) 的功能。 有关详细信息，请参阅如何：使用打包资源管理器 向包 [添加和删除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)。

## <a name="add-features-to-a-sharepoint-package"></a>将功能添加到 SharePoint 包
 可以使用包设计器将功能添加到SharePoint包。

#### <a name="to-add-sharepoint-features-with-the-package-designer"></a>使用SharePoint设计器添加自定义功能

1. 打开包 **设计器**。

    有关详细信息，请参阅[如何：自定义SharePoint包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)。

2. 通过执行一SharePoint一个或多个以下步骤，添加一个或多个自定义功能：

   1. 双击"解决方案"列表中 **要添加的** "项"中的每个项。

   2. 选择要添加的项，然后选择"添加 **"** 按钮 (>) 。

   3. 选择" **全部添加** "按钮 (>>) 一次添加所有项。

      例如，可以双击"解决方案"列表中的"项"中的 **某个项，** 将其添加到"包 **"列表中的"项"。**

      "SharePoint Project项和功能"显示在"包 **"列表中的"项"** 中。

## <a name="remove-features-from-a-sharepoint-package"></a>从包中删除SharePoint功能
 可以使用包设计器将功能删除到SharePoint包。

#### <a name="to-remove-sharepoint-features-with-the-package-designer"></a>使用SharePoint设计器删除所有功能

1. 在"**包"** 列表中的"项"中，选择要删除的项，然后选择"删除 (<) "按钮，或选择"删除所有 (<<) 按钮以删除所有项。

     "SharePoint项"显示在"解决方案 **"列表中的"项"** 中。

## <a name="see-also"></a>请参阅
- [创建SharePoint解决方案包](../sharepoint/creating-sharepoint-solution-packages.md)
- [如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [如何：创建包](/previous-versions/ee231585(v=vs.110))