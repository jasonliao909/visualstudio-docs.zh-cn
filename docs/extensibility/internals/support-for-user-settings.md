---
title: 支持用户设置 |Microsoft Docs
description: 了解如何使用 Visual Studio SDK 中的设置 API 启用设置类别的持久性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Custom Settings Points
- user settings [Visual Studio SDK], registering persistence support
- persistence, registering settings
ms.assetid: ad9beac3-4f8d-4093-ad0e-6fb00444a709
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 85a4e2fa7b09309d8927555e26302bcb4183e0d932cdaaf59188f4f48d69ffa2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414371"
---
# <a name="support-for-user-settings"></a>支持用户设置
VSPackage **可以** 定义一个或多个设置类别，这些类别是当用户在"工具"菜单上选择导入/导出 设置命令时保留 **的状态变量** 组。 若要启用此持久性，请使用 中的设置 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] API。

 称为自定义点和 GUID 的设置项定义 VSPackage 的设置类别。 VSPackage 可以支持多个设置类别，每个类别由自定义点设置定义。

- 基于互操作程序集的设置实现 (使用接口) 应该通过编辑注册表或注册器脚本 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings> (.rgs 文件来创建自定义 设置 Point) 。 有关更多信息，请参见 [Creating Registrar Scripts](/cpp/atl/creating-registrar-scripts)。

- 使用托管包框架 (MPF) 的代码应该通过为每个自定义 设置 点将 附加到 VSPackage 来创建自定义 设置 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 点。

     如果单个 VSPackage 支持多个自定义设置点，则每个自定义 设置 Point 由单独的类实现，每个自定义点由 类的唯一实例 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 注册。 因此，实现 类的设置可以支持多个设置类别。

## <a name="custom-settings-point-registry-entry-details"></a>自定义设置点注册表项详细信息
 自定义 设置 Points 是在以下位置的注册表项中创建的：HKLM\Software\Microsoft\VisualStudio \UserSettings，其中 是 VSPackage 支持的自定义 设置 Point 的名称，是 的版本，例如 \\ *\<Version>* \\ `<CSPName>` `<CSPName>` *\<Version>* [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 8.0。

> [!NOTE]
> 初始化 IDE HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio集成开发环境时，可以使用备用根 (替代) \\ *\<Version>* [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 路径。 有关详细信息，请参阅 [命令行开关](../../extensibility/command-line-switches-visual-studio-sdk.md)。

 注册表项的结构如下图所示：

 HKLM\Software\Microsoft\VisualStudio \\ *\<Version>* \UserSettings\

 `<CSPName`>= '#12345'

 包 = '{XXXXXX XXXX XXXX XXXX XXXXXXXXX}'

 Category = '{YYYYYY YYYYY YYYYY YYYYY}'

 ResourcePackage = '{ZZZZZZ ZZ ZZ ZZ ZZ ZZZZZZZ}'

 AlternateParent = CategoryName

| 名称 | 类型 | 数据 | 说明 |
|-----------------|--------| - | - |
| （默认值） | REG_SZ | 自定义点设置的名称 | 密钥的名称（>）是自定义点设置 `<CSPName` 名称。<br /><br /> 对于基于 MPF 的实现，键的名称通过将构造函数的 和 `categoryName` `objectName` 参数合并到 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 获取 `categoryName_objectName` 。<br /><br /> 键可以为空，也可以包含附属 DLL 中本地化字符串的引用 ID。 此值从构造函数的 `objectNameResourceID` 参数 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 获取。 |
| 包裹 | REG_SZ | GUID | 实现自定义分发点的 VSPackage 设置 GUID。<br /><br /> 基于使用 类的 MPF 的实现使用包含 VSPackage 的 和反射的构造函数参数 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> `objectType` <xref:System.Type> 来获取此值。 |
| 类别 | REG_SZ | GUID | 标识设置类别的 GUID。<br /><br /> 对于基于互操作程序集的实现，此值可以是任意选择的 GUID，IDE 会传递给 和 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ExportSettings%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ImportSettings%2A> 方法。 这两种方法的所有实现都应验证其 GUID 参数。<br /><br /> 对于基于 MPF 的实现，此 GUID 由实现设置机制的 类 <xref:System.Type> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的 获取。 |
| ResourcePackage | REG_SZ | GUID | 可选。<br /><br /> 如果实现 VSPackage 不提供本地化字符串，则指向包含本地化字符串的附属 DLL 的路径。<br /><br /> MPF 使用反射来获取正确的资源 VSPackage，因此 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 类不会设置此参数。 |
| AlternateParent | REG_SZ | "工具选项"页下包含此自定义点设置的名称。 | 可选。<br /><br /> 只有在设置实现支持使用 中的持久性机制（而不是自动化模型中用于保存状态的机制）的工具选项页时，才必须 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 设置此值。<br /><br /> 在这些情况下，AlternateParent 键中的值是用于标识特定 `topic` `topic.sub-topic` **"工具""选项** "页的字符串部分。 例如，对于 **"工具""选项"** 页 `"TextEditor.Basic"` ，AlternateParent 的值为 `"TextEditor"` 。<br /><br /> 当 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 生成自定义设置点时，它与类别名称相同。 |
