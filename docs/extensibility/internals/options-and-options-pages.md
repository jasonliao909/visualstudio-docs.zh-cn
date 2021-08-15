---
title: "\"选项\"和\"选项\"页|Microsoft Docs"
description: 了解对选项页的支持，通过这些选项页可以更改确定 VSPackage 状态的选项的值。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], managed package framework support
- managed package framework, Tools Options pages support
- support, Tools Options pages
- Tools Options pages [Visual Studio SDK], layouts
- Tools Options pages [Visual Studio SDK], attributes
ms.assetid: e6c0e636-5ec3-450e-b395-fc4bb9d75918
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 8e861539470579cc10f2dc41859237393b89fdf943b30ec0033cf2f033f862e6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121359242"
---
# <a name="options-and-options-pages"></a>选项和选项页
单击 **"** 工具" **菜单上的** "选项"将打开 **"选项** "对话框。 此对话框中的选项统称为选项页。 导航窗格中的树控件包括选项类别，每个类别都有选项页。 选择页面时，其选项将显示在右窗格中。 这些页面允许更改用于确定 VSPackage 状态的选项的值。

## <a name="support-for-options-pages"></a>对选项页的支持
 类 <xref:Microsoft.VisualStudio.Shell.Package> 支持创建选项页和选项类别。 类 <xref:Microsoft.VisualStudio.Shell.DialogPage> 实现选项页。

 的默认实现 <xref:Microsoft.VisualStudio.Shell.DialogPage> 向通用属性网格中的用户提供其公共属性。 可以通过重写页面上的各种方法自定义此行为，以创建自定义选项页，该页具有自己的用户界面 (UI) 。 有关详细信息，请参阅创建 [选项页](../../extensibility/creating-an-options-page.md)。

 类 <xref:Microsoft.VisualStudio.Shell.DialogPage> 实现 <xref:Microsoft.VisualStudio.Shell.IProfileManager> ，它为选项页和用户设置提供持久性。 如果 和 方法的默认实现可以将 属性转换为字符串，并且该属性可以从字符串转换，则该属性更改将持久化到 <xref:Microsoft.VisualStudio.Shell.IProfileManager.LoadSettingsFromStorage%2A> <xref:Microsoft.VisualStudio.Shell.IProfileManager.SaveSettingsToStorage%2A> 注册表的用户部分。

## <a name="options-page-registry-path"></a>"选项"页注册表路径
 默认情况下，通过组合 、单词 DialogPage 和选项页类的类型名称来确定由选项页管理的属性的 <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A> 注册表路径。 例如，选项页类的定义如下。

 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs" id="Snippet1":::
 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb" id="Snippet1":::

 如果为 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp，则属性名称和值对是属性的子 <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A> HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp\DialogPage\Company.OptionsPage.OptionsPageGeneral。

 选项页本身的注册表路径通过组合 、单词 <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> ToolsOptionsPages 以及选项页类别和名称来确定。 例如，如果"自定义选项"页的类别为"我的选项页HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp，则选项页具有注册表项 <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\ToolsOptionsPages\My Option Pages\Custom"。

## <a name="toolsoptions-page-attributes-and-layout"></a>"工具/选项"页属性和布局
 属性 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 确定自定义选项页在"选项"对话框的导航树中按 **类别** 分组。 属性 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 将选项页与提供 接口的 VSPackage 关联。 考虑以下代码片断：

:::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs" id="Snippet2":::
:::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb" id="Snippet2":::

 这声明 MyPackage 提供两个选项页：OptionsPageGeneral 和 OptionsPageCustom。 在" **选项"** 对话框中，这两个选项页分别在" **我的** 选项页"类别中显示为" **常规** "和" **自定义**"。

## <a name="option-attributes-and-layout"></a>选项属性和布局
 页面提供的 (用户界面) 确定自定义选项页中选项的外观。 泛型选项页中选项的布局、标记和说明由以下属性确定：

- <xref:System.ComponentModel.CategoryAttribute> 确定选项的类别。

- <xref:System.ComponentModel.DisplayNameAttribute> 确定选项的显示名称。

- <xref:System.ComponentModel.DescriptionAttribute> 确定选项的说明。

  > [!NOTE]
  > 等效属性（SRCategory、LocDisplayName 和 SRDescription）使用字符串资源进行本地化，在托管项目示例 [中定义](/azure/devops/integrate/index)。

  考虑以下代码片断：

  :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/optionspagecustom.cs" id="Snippet3":::
  :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/optionspagegeneral.vb" id="Snippet3":::

  OptionInteger 选项在选项页上显示为 **"我的选项** "类别中的 **"整数选项** "。 如果选择了该选项，说明框中将显示说明" **我的** 整数"选项 。

## <a name="accessing-options-pages-from-another-vspackage"></a>从另一个 VSPackage 访问选项页
 托管和管理选项页的 VSPackage 可以使用自动化模型以编程方式从另一个 VSPackage 访问。 例如，在下面的代码中，VSPackage 注册为承载选项页。

 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs" id="Snippet4":::
 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb" id="Snippet4":::

 以下代码片段从 MyOptionPage 获取 OptionInteger 的值：

 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs" id="Snippet5":::
 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb" id="Snippet5":::

 当 属性注册选项页时，如果该特性的 参数为 ，则页面在 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> AutomationProperties 键 `SupportsAutomation` 下注册 `true` 。 自动化检查此注册表项以查找关联的 VSPackage，然后自动化通过托管选项页（本例中为"我的网格页"）访问 属性。

 自动化属性的注册表路径通过组合 、单词 <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> AutomationProperties 以及选项页类别和名称来确定。 例如，如果选项页具有"我的类别"类别、"我的网格页名称"和"HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp"，则自动化属性具有注册表项 <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\AutomationProperties\My Category\My Grid Page。

> [!NOTE]
> 规范名称"我的 Category.My 网格页"是此键的 Name 子项的值。
