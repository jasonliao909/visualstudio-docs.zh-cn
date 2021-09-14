---
title: 如何：在 SharePoint 功能中添加和移除项 |Microsoft Docs
description: 使用 Visual Studio 中的功能设计器将 SharePoint 项目项手动添加到 SharePoint 功能。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.FeatureDesigner
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: c69cd284a6268d132b90242b8c2a461b51718874
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600617"
---
# <a name="how-to-add-and-remove-items-to-sharepoint-features"></a>如何：在 SharePoint 功能中添加和移除项
  创建 SharePoint 解决方案时，Visual Studio 会将默认 SharePoint 项目项添加到功能。 在部署之前，您可以添加和删除 SharePoint 项目项以修改 SharePoint 功能。

## <a name="add-sharepoint-project-items-to-a-feature"></a>向功能添加 SharePoint 项目项

#### <a name="to-add-sharepoint-project-items-with-the-feature-designer"></a>用功能设计器添加 SharePoint 项目项

1. 打开 "功能设计器"。

    有关详细信息，请参阅[如何：自定义 SharePoint 功能](../sharepoint/how-to-customize-a-sharepoint-feature.md)中的说明进行操作。

2. 通过执行以下一个或多个步骤，将 **"解决方案** " 列表中的项中的一个或多个项添加到 **功能列表中的项** ：

   - 双击要添加的每一项。

   - 选择要添加的项目，然后选择 " **添加** " 按钮 (> ") "。

   - 选择 " **全部添加** " 按钮 (>>) 。

     SharePoint Project 项显示在功能列表中的 **项** 上。

## <a name="remove-sharepoint-project-items-from-a-feature"></a>从功能中删除 SharePoint 项目项

#### <a name="to-remove-sharepoint-items-with-the-feature-designer"></a>用功能设计器删除 SharePoint 项

1. 选择 **功能列表项** 中的一个或多个项。

2. 选择 " **删除** " 按钮 (<) 一次删除一个项目，或选择 " **全部删除** " 按钮 (<<) "以删除所有项目。

     SharePoint Project 项显示在解决方案列表中的 **项** 上。

## <a name="see-also"></a>另请参阅
- [创建 SharePoint 功能](../sharepoint/creating-sharepoint-features.md)
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
