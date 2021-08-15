---
title: 本地化菜单命令|Microsoft Docs
description: 了解如何通过为 VSPackage 创建本地化的 .vsct 文件和本地化的 .resx 文件，为菜单和工具栏命令提供本地化文本。
ms.custom: SEO-VS-2020
ms.date: 10/08/2019
ms.topic: how-to
helpviewer_keywords:
- localize
- localization
- vsct
- menu commands
- localize visual studio
- localize vsct
ms.assetid: b04ee0f6-82ea-47e6-853a-72382267d6da
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 12a8801e9629de97bed6e35dbdcc3bc8d14a1653f0692aca3a46f4deddd91430
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401084"
---
# <a name="localize-menu-commands"></a>本地化菜单命令

可以通过为 VSPackage 创建本地化 *的 .vsct* 文件和本地化 *的 .resx* 文件，然后更新项目文件以合并更改，为菜单和工具栏命令提供本地化文本。

若要了解如何本地化安装体验，请参阅 [本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)。

## <a name="localize-command-names"></a>本地化命令名称

在 VSPackages 中，菜单命令和工具栏按钮在 *.vsct 文件中* 定义。

1. 在 **解决方案资源管理器** 中，将 *.vsct* 文件的名称从 *filename.vsct* 更改为 *filename.en-US.vsct*。

2. 为每种本地化语言创建 *filename.en-US.vsct* 的副本。

    将每个副本 *文件名命名。{Locale}.vsct*，其中 *{Locale}* 是特定的区域性名称。 有关区域性名称值的列表，请参阅 Microsoft[分配区域设置 ID。](/windows/uwp/publish/supported-languages)

    这些 *文件名。Locale.vsct* 文件将包含包的本地化菜单文本。

3. 打开每个 *文件名。用于本地化文本的 Locale.vsct* 文件。

   1. 根据 [特定语言修改 ButtonText](../extensibility/buttontext-element.md) 元素值。

   2. 如果要提供本地化的图标，请修改 [位图](../extensibility/bitmap-element.md) 值以指向目标文件。

      以下示例显示用于打开"家庭树资源管理器"工具窗口的命令的英语和西班牙语按钮文本。

      [*FamilyTree.en-US.vsct*]

   ```xml
   <Button guid="guidLocalizedPackageCmdSet" id="cmdidFamilyTree" priority="0x0100" type="Button">
     <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>
     <Icon guid="guidImages" id="bmpPic2" />
     <Strings>
       <CommandName>cmdidFamilyTree</CommandName>
       <ButtonText>Family Tree Explorer</ButtonText>
     </Strings>
   </Button>
   ```

    [*FamilyTree.es-ES.vsct*]

   ```xml
   <Button guid="guidLocalizedPackageCmdSet" id="cmdidFamilyTree" priority="0x0100" type="Button">
     <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>
     <Icon guid="guidImages" id="bmpPic2" />
     <Strings>
       <CommandName>cmdidFamilyTree</CommandName>
       <ButtonText>Explorar el arbol genealogico</ButtonText>
     </Strings>
   </Button>
   ```

## <a name="localize-other-text-resources"></a>本地化其他文本资源

除命令名称外的文本资源在 *.resx* (资源) 定义。

1. 将 *VSPackage.resx* 重命名为 *VSPackage.en-US.resx*。

2. 为每种本地化语言创建 *VSPackage.en-US.resx* 文件的副本。

     将每个副本 *命名 VSPackage。{Locale}.resx*，其中 *{Locale}* 是特定的区域性名称。

3. 将 *Resources.resx* 重命名为 *Resources.en-US.resx*。

4. 为每种本地化语言创建 *Resources.en-US.resx* 文件的副本。

     命名每个副本 *资源。{Locale}.resx*，其中 *{Locale}* 是特定的区域性名称。

5. 打开每个 *.resx* 文件，根据特定语言和区域性修改字符串值。 以下示例显示了工具窗口的标题栏的本地化资源定义。

     [*Resources.en-US.resx*]

    ```xml
    <data name="ToolWindowTitle" xml:space="preserve">
      <value>Family Tree Explorer</value>
    </data>
    ```

     [*Resources.es-ES.resx*]

    ```xml
    <data name="ToolWindowTitle" xml:space="preserve">
      <value>Explorador del arbol genealogico</value>
    </data>
    ```

## <a name="incorporate-localized-resources-into-the-project"></a>将本地化资源合并到项目中

必须修改 *assemblyinfo.cs* 文件和项目文件以合并本地化的资源。

1. 从 "**属性"** 解决方案资源管理器 **，在** 编辑器中打开 *assemblyinfo.cs* 或 *assemblyinfo.vb。*

2. 添加以下条目。

    ```csharp
    [assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]
    ```

     这会将"美国英语"设置为默认语言。

3. 卸载项目。

4. 在编辑器中打开项目文件。

5. 在根 `Project` 元素中，添加 `PropertyGroup` 具有 `UICulture` 与默认语言匹配的元素的元素。

    ```xml
    <PropertyGroup>
      <UICulture>en-US</UICulture>
    </PropertyGroup>
    ```

     这会将"美国英语"设置为 WPF 控件Windows Presentation Foundation (UI) 区域性。

6. 找到 `ItemGroup` 包含 元素 `EmbeddedResource` 的元素。

7. 在 `EmbeddedResource` 调用 *VSPackage.en-US.resx* 的 元素中，将 元素替换为设置为 `ManifestResourceName` `LogicalName` `VSPackage.en-US.Resources` 的元素，如下所示：

    ```xml
    <EmbeddedResource Include="VSPackage.en-US.resx">
      <MergeWithCTO>true</MergeWithCTO>
      <LogicalName>VSPackage.en-US.Resources</LogicalName>
    </EmbeddedResource>
    ```

8. 对于每个本地化语言，复制 的 元素，将副本的 Include 属性和 LogicalName 元素设置为 `EmbeddedResource` `VsPackage.en-US` 目标区域设置。  

9. 对于每个本地化 `VSCTCompile` 元素，添加指向 的元素 `ResourceName` `Menus.ctmenu` ，如以下示例所示：

    ```xml
    <ItemGroup>
      <VSCTCompile Include="LocalizedPackage.es-ES.vsct">
        <ResourceName>Menus.ctmenu</ResourceName>
      </VSCTCompile>
    </ItemGroup>
    ```

10. 保存项目文件并重新加载项目。

11. 生成项目。

     这会为每个语言创建主程序集和资源程序集。 有关本地化部署过程的信息，请参阅 [本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)

## <a name="see-also"></a>另请参阅

- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
- [全球化和本地化应用程序](../ide/globalizing-and-localizing-applications.md)
