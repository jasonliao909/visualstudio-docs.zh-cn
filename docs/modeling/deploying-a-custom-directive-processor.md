---
title: 部署自定义指令处理器
description: 了解可用于在计算机或任何计算机上部署Visual Studio指令处理器的方法。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- text templates, custom directive processors
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 4dcc9f12a65ad163acd07724da534039c772b385446f00b30dab627d441a42fc
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121316859"
---
# <a name="deploying-a-custom-directive-processor"></a>部署自定义指令处理器

若要在任何计算机的 Visual Studio 中使用自定义指令处理器，必须通过本主题中所述的方法之一进行注册。

可用的方法包括：

- [Visual Studio扩展。](../extensibility/shipping-visual-studio-extensions.md) 通过这种方法，可以在自己或他人的计算机上安装和卸载指令处理器。 通常，可能会在同一 VSIX 中包含其他功能。

- [VSPackage](../extensibility/internals/vspackages.md)。 如果要定义一个包含指令处理器和其他功能的 VSPackage，有一种方便的方法可以注册指令处理器。

- 设置注册表项。 如果采用此方法，则会为指令处理器添加一个注册表项。

只有在要转换文本模板的 Visual Studio 或 MSBuild 时，才需要使用这些方法之一。 如果在自己的应用程序中使用自定义宿主，则由自定义宿主负责查找每条指令的指令处理器。

## <a name="deploying-a-directive-processor-in-a-vsix"></a>在 VSIX 中部署指令处理器

可以将自定义指令处理器添加到[VSIX Visual Studio扩展 (扩展) 。 ](../extensibility/starting-to-develop-visual-studio-extensions.md)

 需要确保 .vsix 文件包含以下两项：

- 包含自定义指令处理器类的程序集 (.dll)。

- 注册指令处理器的 .pkgdef 文件。 文件的根名称必须与程序集相同。 例如，文件可以命名为 CDP.dll 和 CDP.pkgdef。

若要检查或更改 .vsix 文件的内容，请将其文件扩展名更改为 .zip，然后将其打开。 编辑内容之后，将文件扩展名改回为 .vsix。

有几种方法可以创建 .vsix 文件。 以下过程将介绍其中一种方法。

#### <a name="to-develop-a-custom-directive-processor-in-a-vsix-project"></a>在 VSIX 项目中开发自定义指令处理器

1. 创建新的 **VSIX Project** 项目。

2. 在 **source.extension.vsixmanifest** 中，设置内容类型和支持的版本。

    1. 在 VSIX 清单编辑器中的"资产 **"** 选项卡上，选择 **"新建"** 并设置新项的属性：

         **内容类型**  = **VSPackage**

         **源Project** = \<*the current project*>

    2. 单击 **"所选** 版本"，并检查希望指令处理器可用于的安装类型。

3. 添加 .pkgdef 文件，并设置其属性，以便使其包含在 VSIX 中。

    1. 创建文本文件，并命名 \<*assemblyName*> .pkgdef。

         \<*assemblyName*> 通常与项目的名称相同。

    2. 在解决方案资源管理器中，选中该文件并将其属性设置如下：

         **生成操作** = **内容**

         **复制到输出目录**  = **始终复制**

         **在 VSIX 中包括**  = **True**

    3. 设置 VSIX 的名称并确保该 ID 是唯一的。

4. 向 .pkgdef 文件添加以下文本。

    ```
    [$RootKey$\TextTemplating]
    [$RootKey$\TextTemplating\DirectiveProcessors]
    [$RootKey$\TextTemplating\DirectiveProcessors\ CustomDirectiveProcessorName]
    @="Custom Directive Processor description"
    "Class"="NamespaceName.ClassName"
    "CodeBase"="$PackageFolder$\AssemblyName.dll"
    ```

     用您自己提供的名称替换以下名称：`CustomDirectiveProcessorName`、`NamespaceName`、`ClassName`、`AssemblyName`。

5. 将下列引用添加到该项目中：

    - **Microsoft.VisualStudio.TextTemplating。 \*0**

    - **Microsoft.VisualStudio.TextTemplating.Interfaces。 \*0**

    - **Microsoft.VisualStudio.TextTemplating.VSHost。 \*0**

6. 将自定义指令处理器类添加到项目。

     这是一个公共类，它应实现 <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> 或 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>。

#### <a name="to-install-the-custom-directive-processor"></a>安装自定义指令处理器

1. 在Windows资源管理器中，打开生成目录 (bin\Debug 或 bin\Release) 。

2. 如果要在另一台计算机上安装指令处理器，请将 .vsix 文件复制到该计算机。

3. 双击 .vsix 文件。 将显示Visual Studio扩展安装程序。

4. 重启 Visual Studio。 现在，可以运行包含引用自定义指令处理器的指令的文本模板。 每个指令的形式如下：

     `<#@ CustomDirective Processor="CustomDirectiveProcessorName" parameter1="value1" ... #>`

#### <a name="to-uninstall-or-temporarily-disable-the-custom-directive-processor"></a>卸载或临时禁用自定义指令处理器

1. 在 **"Visual Studio"菜单中**，单击"**扩展管理器"。**

2. 选择包含指令处理器的 VSIX，然后单击"卸载 **"或**"禁用 **"。**

### <a name="troubleshooting-a-directive-processor-in-a-vsix"></a>VSIX 中指令处理器的疑难解答
 如果指令处理器不能正常运行，可以尝试以下建议：

- 在自定义指令中指定的处理器名必须与在 .pkgdef 文件中指定的 `CustomDirectiveProcessorName` 一致。

- `IsDirectiveSupported` 方法在传递 `true` 的名称时必须返回 `CustomDirective`。

- 如果在扩展管理器中看不到扩展，但系统不允许安装该扩展，请从 **%localappdata%\Microsoft\VisualStudio \\ \* .0\Extensions \\** 中删除扩展。

- 打开 .vsix 文件并检查其内容。 若要打开该文件，请将文件扩展名更改为 .zip。 确认该文件包含 .dll、.pkgdef 和 extension.vsixmanifest 文件。 extension.vsixmanifest 文件的 SupportedProducts 节点应包含相应的列表，“内容”节点下还应包含 VsPackage 节点：

     `<Content>`

     `<VsPackage>CustomDirectiveProcessor.dll</VsPackage>`

     `</Content>`

## <a name="deploying-a-directive-processor-in-a-vspackage"></a>在 VSPackage 中部署指令处理器
 如果指令处理器作为 VSPackage 的一部分安装在 GAC 中，则可以由系统生成 .pkgdef 文件。

 为包类添加以下特性：

```csharp
[ProvideDirectiveProcessor(typeof(DirectiveProcessorClass), "DirectiveProcessorName", "Directive processor description.")]
```

> [!NOTE]
> 将此特性置于包类，而不是指令处理器类。

 生成项目时，将生成 .pkgdef 文件。 安装 VSPackage 时，.pkgdef 文件将注册指令处理器。

 确认 .pkgdef 文件显示在生成文件夹中，该文件夹通常是 bin\Debug 或 bin\Release。 如果未显示该文件，请在文本编辑器中打开 .csproj 文件，删除以下节点：`<GeneratePkgDefFile>false</GeneratePkgDefFile>`。

 有关更多信息，请参见 [VSPackages](../extensibility/internals/vspackages.md)。

## <a name="setting-a-registry-key"></a>设置注册表项
 这种自定义指令处理器的安装方法是最不方便的一种方法。 这种方法不能方便地启用和禁用指令处理器，也不能方便地向其他用户分发指令处理器。

> [!CAUTION]
> 错误编辑注册表会严重损坏您的系统。 更改注册表之前，请务必备份计算机中的所有重要数据。

#### <a name="to-register-a-directive-processor-by-setting-a-registry-key"></a>通过设置注册表项注册指令处理器

1. 运行 `regedit`。

2. 在 regedit 中，定位到

    **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\ \* .0\TextTemplating\DirectiveProcessors**

    如果要在实验版本的 Visual Studio 中安装指令处理器，请将"Exp"插入"11.0"之后。

3. 添加与指令处理器类同名的注册表项。

   - 在注册表树中，右键单击 **"DirectiveProcessors"** 节点，指向"**新建**"，然后单击"密钥 **"。**

4. 在新建节点中，根据下表为 Class 和 CodeBase 或 Assembly 添加字符串值。

   1. 右键单击创建的节点，指向"**新建"，** 然后单击"字符串 **值"。**

   2. 编辑值的名称。

   3. 双击该名称，然后编辑数据。

   如果自定义指令处理器不在 GAC 中，则注册表子项应如下表所示：

|名称|类型|数据|
|-|-|-|
|（默认值）|REG_SZ|(未设置值)|
|类|REG_SZ|**\<Namespace Name>.\<Class Name>**|
|CodeBase|REG_SZ|**\<Your Path>\\<程序集名称\>**|

 如果程序集在 GAC 中，则注册表子项应如下表所示：

|名称|类型|数据|
|-|-|-|
|（默认值）|REG_SZ|(未设置值)|
|类|REG_SZ|\<**Your Fully Qualified Class Name**>|
|程序集|REG_SZ|\<**Your Assembly Name in the GAC**>|

## <a name="see-also"></a>另请参阅

- [创建自定义 T4 文本模板指令处理器](../modeling/creating-custom-t4-text-template-directive-processors.md)
