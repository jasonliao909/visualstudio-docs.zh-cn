---
title: 如何：添加和移除附加程序集 |Microsoft Docs
description: 了解如何添加和删除 SharePoint 解决方案包中的其他程序集。 同时，添加或删除安全控件和类资源。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.CustomAssembly
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
ms.openlocfilehash: aa1017ec2dd27ddb46281a6f8c047641f4117b9f39818ed091f5174d91e79240
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121228709"
---
# <a name="how-to-add-and-remove-additional-assemblies"></a>如何：添加和移除附加程序集
  如果 SharePoint 包依赖于其他程序集以获取功能或数据，则可以将程序集添加到解决方案包 ( .wsp) 。 这样，SharePoint 服务器就可以确保使用包安装自定义程序集。

 你还可以添加和更改与程序集关联的安全控件和类资源文件。

## <a name="add-additional-assemblies-safe-controls-and-class-resources"></a>添加其他程序集、安全控件和类资源
 你可以将其他程序集添加到 SharePoint 解决方案包。 沙盒解决方案中的其他程序集将部署到全局程序集缓存中，但沙盒解决方案中 SharePoint 项目项会添加到内容数据库。 你还可以向这些附加程序集添加安全控件和类资源。 有关安全控件的详细信息，请参阅在[SharePoint Foundation 中部署 Web 部件](/previous-versions/office/developer/sharepoint-2010/cc768621(v=office.14))中[Project 项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)，或 "创建 SafeControl 条目"。

#### <a name="to-add-an-existing-assembly"></a>添加现有程序集

1. 打开 **包设计器**。 有关详细信息，请参阅[如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)。

2. 选择“高级”选项卡。

3. 选择 " **添加** " 按钮，然后从列表中选择 " **添加现有程序集** "。

     此时将显示 " **添加现有程序集** " 对话框。

4. 选择省略号 (![ASP.NET Mobile 设计器 "椭圆形](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")") ，然后选择要添加的程序集。 出于可移植性的目的，我们建议使用相对路径到选定的程序集。

5. 对于 **部署目标**，请选择 " **GlobalAssemblyCache** " 选项按钮以将程序集部署到全局程序集缓存，或选择 " **WebApplication** " 选项按钮，将程序集部署到运行 SharePoint 的服务器上的 WebApplication 文件夹中。

#### <a name="to-add-an-assembly-from-project-output"></a>从项目输出中添加程序集

1. 打开 **包设计器**。

     有关详细信息，请参阅[如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)。

2. 选择“高级”选项卡。

3. 选择 "**添加**" 按钮，然后从列表中选择 "**从 Project 输出添加程序集**"。

     此时将显示 "**从 Project 输出添加程序集**" 对话框。

4. 在 "**源 Project** " 列表中，选择要添加的源项目。

5. 对于 **部署目标**，请选择 " **GlobalAssemblyCache** " 选项按钮以将程序集部署到全局程序集缓存，或选择 " **WebApplication** " 选项按钮，将程序集部署到运行 SharePoint 的服务器上的 WebApplication 文件夹中。

#### <a name="to-add-a-safe-control"></a>添加安全控件

1. 打开 " **编辑现有程序集** " 对话框。 若要实现此目的，请打开包设计器，选择 " **高级** " 选项卡，选择一个程序集，然后选择 " **编辑** " 按钮。

2. 在 **保险箱控件**"窗格中，选择"**单击此处添加新项**"按钮。

3. 在 " **程序集名称** " 列中，输入程序集的名称。

4. 在 " **命名空间** " 列中，输入安全控件的命名空间的名称。

5. 在 " **类型名称** " 列中，输入类型的名称。

#### <a name="to-add-a-class-resource"></a>添加类资源

1. 打开 " **编辑现有程序集** " 对话框。 若要实现此目的，请打开包设计器，选择 " **高级** " 选项卡，选择一个程序集，然后选择 " **编辑** " 按钮。

2. 在 " **类资源** " 窗格中，选择 " **单击此处添加新项** " 按钮。

3. 在 "**文件名**" 列中，选择省略号 (![ASP.NET 移动设计器](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")"" 椭圆形 ") ，然后选择要添加的类资源。

## <a name="delete-custom-assemblies"></a>删除自定义程序集
 可以从 SharePoint 包删除程序集，也可以从现有程序集中删除安全控件和类资源。

#### <a name="to-delete-an-existing-assembly"></a>删除现有程序集

1. 打开 **包设计器**。 有关详细信息，请参阅[如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)。

2. 选择“高级”选项卡。

3. 在 " **其他程序集** " 窗格中，选择要删除的自定义程序集。

4. 选择 **“删除”** 按钮。

#### <a name="to-delete-a-safe-control-for-an-assembly"></a>删除程序集的安全控件

1. 打开 " **编辑现有程序集** " 对话框。 若要实现此目的，请打开包设计器，选择 " **高级** " 选项卡，选择一个程序集，然后选择 " **编辑** " 按钮。

2. 选择要删除的安全控件。

3. 选择 "删除" 键。

#### <a name="to-delete-a-class-resource-for-an-assembly"></a>删除程序集的类资源

1. 打开 " **编辑现有程序集** " 对话框。 若要实现此目的，请打开包设计器，选择 " **高级** " 选项卡，选择一个程序集，然后选择 " **编辑** " 按钮。

2. 选择要删除的类资源。

3. 选择 "删除" 键。

## <a name="see-also"></a>请参阅
- [创建 SharePoint 功能](../sharepoint/creating-sharepoint-features.md)
- [如何：自定义 SharePoint 功能](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [如何：在 SharePoint 功能中添加和移除项](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
