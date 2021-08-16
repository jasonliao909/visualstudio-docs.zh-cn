---
title: 使用自动化模型|Microsoft Docs
description: 了解如何在 VSPackage 连接到自动化模型后获取其属性和方法。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], automation model
ms.assetid: 0c7f7889-fbfb-4b19-804f-b742138baecd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6412e27386ac0744ecaae607d83c7297900f464cd9ff843983019331ca6f17db
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121375619"
---
# <a name="using-the-automation-model"></a>使用自动化模型
将 VSPackage 连接到自动化后，可以通过在 对象上调用 方法来获取属性和方法，并传递表示要检索 <xref:EnvDTE.DTEClass.GetObject%2A> <xref:EnvDTE._DTE> 的对象的字符串。

## <a name="obtaining-project-objects"></a>获取Project对象
 下面是两个代码示例，其中显示了自动化使用者如何获取项目自动化对象。 若要了解如何获取 DTE 对象，请参阅 [如何：获取对 DTE 和 DTE2 对象的引用](/previous-versions/68shb4dw(v=vs.140))。

```vb
Sub DoAutomation()
    Dim MyProjects As Projects
    MyProjects = DTE.GetObject("AcmeProject")
End Sub
```

```cpp
void DoAutomation(void)
{
  CComQIPtr<Projects> pMyPkg; // Use an IDispatch-derived object type.
    pMyPkg = pDTE->GetObject("AcmeProjects");

   // The '=' performs a Query Interface.
   // Assumes pDTE is already available as a global.
   // Use pMyPkg to access your projects object's properties and methods.
}

```

 此时，可以使用属于特定 VSPackage 的标准项目对象向下移动层次结构模型。

 下面的代码示例演示如何获取自定义项目类型的属性的自定义对象：

```vb
Dim MyPrj As Project
Dim MyPrjItem As ProjectItem
Dim objMyObject as MyExtendedObject

MyPrj = MyProjects.Item(1) 'use the Projects collection to get a project
objMyObject = MyPrj.Object 'You call .Object to get to special Project
                           'implementation
objMyObject.MySpecialMethodOrProperty
```

 以下代码列出了"工具"菜单上"环境常规" [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 选项中所有 **属性** 的名称：

```vb
dim objDTE
dim objEnv
set objDTE = CreateObject("VisualStudio.DTE")
set objEnv = objDTE.Properties("Environment", "General")
for each obj in ObjEnv
MsgBox obj.Name
Next

```

## <a name="see-also"></a>另请参阅
- <xref:EnvDTE.DTEClass.GetObject%2A>