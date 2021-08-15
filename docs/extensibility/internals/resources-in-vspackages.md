---
title: VSPackages 中的资源|Microsoft Docs
description: 了解可在 VSPackage 中嵌入哪些类型的本地化资源。 还可以在本机附属 UI DLL 或托管附属 DLL 中嵌入资源。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, resources in
- resources, managed VSPackages
- VSPackages, managed resources
ms.assetid: cc8c17a6-b190-4856-b001-0c1104f104b2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 069ceef0275ce802a9f6bc717baee48a82a5df30e08dba1122f75ea429c2cac8
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121337807"
---
# <a name="resources-in-vspackages"></a>VSPackage 中的资源
可以在本机附属 UI DLL、托管附属 DLL 或托管 VSPackage 本身中嵌入本地化资源。

 某些资源不能嵌入 VSPackage 中。 可以嵌入以下托管类型：

- 字符串

- 包加载密钥 (也是字符串) 

- 工具窗口图标

- 编译的命令表输出 (CTO) 文件

- CTO 位图

- 命令行帮助

- 关于对话框数据

  托管包中的资源按资源 ID 选择。 CTO 文件例外，该文件必须命名为 CTMENU。 CTO 文件必须作为 显示在资源表中 `byte[]` 。 所有其他资源项按类型标识。

  可以使用 属性 <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> 向 指示 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 托管资源可用。

  :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdkresources/cs/vssdkresourcespackage.cs" id="Snippet1":::
  :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdkresources/vb/vssdkresourcespackage.vb" id="Snippet1":::

  按此方式设置 指示在搜索资源时（例如，通过使用 ）应忽略非 <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 托管附属 <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackageString%2A> DLL。 如果 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 遇到两个或多个资源具有相同的资源 ID，则它使用找到的第一个资源。

## <a name="example"></a>示例
 以下示例是工具窗口图标的托管表示形式。

```
<data name="1001"
type="System.Resources.ResXFileRef,System.Windows.Forms">
     <value>
     MyToolWinIcon.bmp;
     System.Drawing.Bitmap,
     System.Drawing,
     Version=1.0.0.0,
     Culture=neutral,
     PublicKeyToken=b03f5f7f11d50a3a
     </value>
</data>
```

 下面的示例演示如何嵌入 CTO 字节数组，该数组必须命名为 CTMENU。

```
<data name="CTMENU"
type="System.Resources.ResXFileRef,System.Windows.Forms">
     <value>
     MyPackage.cto;
     System.Byte[],
     mscorlib,
     Version=1.0.0.0,
     Culture=neutral,
     PublicKeyToken=b03f5f7f11d50a3a
     </value>
</data>
```

## <a name="implementation-notes"></a>实现说明
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 尽可能延迟 VSPackage 的加载。 在 VSPackage 中嵌入 CTO 文件的后果是，在安装期间（即生成合并的命令表时），必须在内存中加载所有此类 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage。 无需在 VSPackage 中运行代码即可检查元数据，从 VSPackage 中提取资源。 VSPackage 目前未初始化，因此性能损失最小。

 在安装后从 VSPackage 请求资源时，该包很可能已加载和初始化，因此 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 性能损失最小。

## <a name="see-also"></a>另请参阅
- [管理 VSPackages](../../extensibility/managing-vspackages.md)
- [MFC 应用程序中的本地化资源：附属 DLL](/cpp/build/localized-resources-in-mfc-applications-satellite-dlls)
