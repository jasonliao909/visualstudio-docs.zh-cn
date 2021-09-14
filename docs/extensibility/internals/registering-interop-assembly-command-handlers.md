---
title: 注册互操作程序集命令处理程序|Microsoft Docs
description: 了解使用互操作程序集实现命令的所有 VSPackage 使用的基本命令协定。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, command handlers
- command handling with interop assemblies, registering
ms.assetid: 303cd399-e29d-4ea1-8abe-5e0b59c12a0c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 8d45e2f547d907e6bd1e75d51b08852f40b6c7a9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664324"
---
# <a name="registering-interop-assembly-command-handlers"></a>注册互操作程序集命令处理程序
VSPackage 必须注册到 ，以便集成开发环境 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (IDE) 正确路由其命令。

 可以通过手动编辑或通过使用注册机构 (.rgs) 注册表。 有关更多信息，请参见 [Creating Registrar Scripts](/cpp/atl/creating-registrar-scripts)。

 MPF (包) 通过 类提供 <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> 此功能。

- [命令表格式引用](/previous-versions/bb164647(v=vs.100)) 资源位于非托管附属 UI dll 中。

## <a name="command-handler-registration-of-a-vspackage"></a>VSPackage 的命令处理程序注册
 充当基于 UI 命令的用户界面 (的 VSPackage) 需要一个以 VSPackage 命名的注册表项 `GUID` 。 此注册表项指定 VSPackage 的 UI 资源文件和该文件中的菜单资源的位置。 注册表项本身位于 HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\Menus 下，其中 是 的版本， \\ *\<Version>* *\<Version>* [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 例如 9.0。

> [!NOTE]
> 初始化 shell 时，HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio的根路径可以使用备用 \\ *\<Version>* [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 根重写。 有关根路径详细信息，请参阅[Installing VSPackages with Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md)。

### <a name="the-ctmenu-resource-registry-entry"></a>CTMENU 资源注册表项
 注册表项的结构为：

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\<Version>\
  Menus\
    <GUID> = <Resource Information>
```

 \<*GUID*> 是 `GUID` {XXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX} 形式的 VSPackage 的 。

 *\<Resource Information>* 由以逗号分隔的三个元素组成。 这些元素的顺序为：

 \<*Path to Resource DLL*>, \<*Menu Resource ID*>, \<*Menu Version*>

 下表描述了 的字段 \<*Resource Information*> 。

| 元素 | 说明 |
|---------------------------| - |
| \<*Path to Resource DLL*> | 这是包含菜单资源的资源 DLL 的完整路径，或留空，表示 VSPackage 的资源 DLL 将按照在 VSPackage 本身注册到) 的 Packages 子项中指定的 (使用。<br /><br /> 希望将此字段留空。 |
| \<*Menu Resource ID*> | 这是资源的资源 ID，其中包含从 `CTMENU` [.vsct](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md) 文件编译的 VSPackage 的所有 UI 元素。 |
| \<*Menu Version*> | 此数字用作资源 `CTMENU` 的版本。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 使用此值确定是否需要重新将资源的内容及其所有资源的 `CTMENU` 缓存 `CTMENU` 重新进行。 通过执行 devenv setup 命令触发重新触发。<br /><br /> 此值最初应设置为 1，在资源中每次更改后以及重新集合发生 `CTMENU` 之前递增。 |

### <a name="example"></a>示例
 下面是几个资源条目的示例：

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\9.0Exp\
  Menus\
    {019971D6-4685-11D2-B48A-0000F87572EB} = ,1, 10
    {1b027a40-8f43-11d0-8d11-00a0c91bc942} = , 10211, 3
```

## <a name="see-also"></a>另请参阅
- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [使用互操作程序集的命令和菜单](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)