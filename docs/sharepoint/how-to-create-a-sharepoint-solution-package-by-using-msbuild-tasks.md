---
title: 使用SharePoint任务创建MSBuild包
description: 了解如何在开发计算机上使用命令行SharePoint (.wsp) 生成、清理和验证 MSBuild 解决方案包。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 781281c6abce5031166b00d9cdde0b175619f79b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671934"
---
# <a name="how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks"></a>如何：使用SharePoint创建解决方案MSBuild包
  可以使用开发计算机上用于SharePoint的命令行 (*.wsp*) 生成、MSBuild和验证包。 还可使用这些命令在生成计算机上使用Team Foundation Server自动执行生成过程。

## <a name="build-a-sharepoint-package"></a>生成SharePoint包

#### <a name="to-build-a-sharepoint-package"></a>生成 SharePoint 包

1. 在 **"Windows"菜单** 上，选择"**所有程序**  >  **附件"**  >  **命令提示符**。

2. 更改为项目所在的SharePoint目录。

3. 输入以下命令，为项目创建包。 将 *ProjectFileName* 替换为项目的名称。

    ```cmd
    msbuild /t:Package ProjectFileName
    ```

     例如，可以运行以下命令之一来打包名为 ListDefinition1 SharePoint项目。

    ```cmd
    msbuild /t:Package ListDefinition1.vbproj
    msbuild /t:Package ListDefinition1.csproj
    ```

## <a name="clean-a-sharepoint-package"></a>清理SharePoint包

#### <a name="to-clean-a-sharepoint-package"></a>清理 SharePoint 包

1. 打开命令提示符窗口。

2. 更改为项目所在的SharePoint目录。

3. 输入以下命令以清除项目的包。 将 *ProjectFileName* 替换为项目的名称。

    ```cmd
    msbuild /t:CleanPackage ProjectFileName
    ```

     例如，可以运行以下命令之一来清理名为 ListDefinition1 SharePoint项目。

    ```cmd
    msbuild /t:CleanPackage ListDefinition1.vbproj
    msbuild /t:CleanPackage ListDefinition1.csproj
    ```

## <a name="validate-a-sharepoint-package"></a>验证SharePoint包

#### <a name="to-validate-a-sharepoint-package"></a>验证SharePoint包

1. 打开命令提示符窗口。

2. 更改为项目所在的SharePoint目录。

3. 输入以下命令以验证项目的包。 将 *ProjectFileName* 替换为项目的名称。

    ```cmd
    msbuild /t:ValidatePackage ProjectFileName
    ```

     例如，可以运行以下命令之一来验证名为 ListDefinition1 SharePoint项目。

    ```cmd
    msbuild /t:ValidatePackage ListDefinition1.vbproj
    msbuild /t:ValidatePackage ListDefinition1.csproj
    ```

## <a name="set-properties-in-a-sharepoint-package"></a>设置包SharePoint属性

#### <a name="to-set-a-property-in-a-sharepoint-package"></a>在应用程序包中SharePoint属性

1. 打开命令提示符窗口。

2. 更改为项目所在的SharePoint目录。

3. 输入以下命令，在项目的包中设置属性。 将 *PropertyName* 替换为要设置的属性。

    ```cmd
    msbuild /property:PropertyName=Value
    ```

     例如，可以运行以下命令来设置警告级别。

    ```cmd
    msbuild /property:WarningLevel = 2
    ```

## <a name="see-also"></a>另请参阅
- [创建SharePoint功能](../sharepoint/creating-sharepoint-features.md)
- [如何：自定义SharePoint功能](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [如何：添加和删除项以SharePoint功能](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
