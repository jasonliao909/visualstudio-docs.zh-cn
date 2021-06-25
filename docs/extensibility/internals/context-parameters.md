---
title: 上下文参数|Microsoft Docs
description: 了解 IDE Visual Studio集成开发 (中的) 参数，这些参数定义添加或实现向导时项目的状态。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- wizards, context parameters
- context parameters
ms.assetid: 1a062dcb-8a8f-40dd-bea9-3d10f9448966
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 536e5abf92884c5c19399e73b4e1773e66919657
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898222"
---
# <a name="context-parameters"></a>上下文参数
在集成开发 (IDE) 中，可以将向导添加到"新建项目"、"添加新项"或 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] "添加 **子项目**"对话框。  添加的向导在"文件"菜单 **上可用**，或右键单击 "文件"**解决方案资源管理器。** IDE 将上下文参数传递给向导的实现。 上下文参数定义 IDE 调用向导时项目的状态。

 IDE 通过设置 IDE 对项目的 方法的调用中的 标志 <xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A> 来启动向导。 设置后，项目必须使用注册的向导名称或 GUID 以及 IDE 传递给它的其他上下文参数，使方法 `IVsExtensibility::RunWizardFile` 执行。

## <a name="context-parameters-for-new-project"></a>新项目的上下文参数

| 参数 | 描述 |
|-------------------------| - |
| `WizardType` | 注册的向导 <xref:EnvDTE.Constants.vsWizardNewProject> () 或指示向导类型的 GUID。 在 实现中，向导的 GUID 为 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] {0F90E1D0-4999-11D1-B6D1-00A0C90F2744}。 |
| `ProjectName` | 作为唯一项目名称 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的字符串。 |
| `LocalDirectory` | 工作项目文件的本地位置。 |
| `InstallationDirectory` | 的目录路径是 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 安装。 |
| `FExclusive` | 指示项目应关闭打开的解决方案的布尔标志。 |
| `SolutionName` | 不带目录部分或 *.sln* 扩展名的解决方案文件的名称。 *.suo* 文件名也是使用 创建的 `SolutionName` 。 如果此参数不是空字符串，则向导在使用 <xref:EnvDTE._Solution.Create%2A> 添加项目之前使用 <xref:EnvDTE._Solution.AddFromTemplate%2A> 。 如果此名称为空字符串，请使用 <xref:EnvDTE._Solution.AddFromTemplate%2A> 而不调用 <xref:EnvDTE._Solution.Create%2A> 。 |
| `Silent` | 一个布尔值，指示向导是否应该以无提示方式运行，就像单击"完成" () 。 `TRUE` |

## <a name="context-parameters-for-add-new-item"></a>添加新项的上下文参数

| 参数 | 描述 |
|-------------------------| - |
| `WizardType` | 注册的向导 <xref:EnvDTE.Constants.vsWizardAddItem> () 或指示向导类型的 GUID。 在实现中，向导的 GUID 为 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] {0F90E1D1-4999-11D1-B6D1-00A0C90F2744}。 |
| `ProjectName` | 作为唯一项目名称 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的字符串。 |
| `ProjectItems` | 包含工作项目文件的本地位置。 |
| `ItemName` | 要添加的项的名称。 此名称是默认文件名或用户从"添加项"对话框中 **输入的文件名** 。 该名称基于在 *.vsdir* 文件中设置的标志。 该名称可以是 null 值。 |
| `InstallationDirectory` | 的目录路径是 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 安装。 |
| `Silent` | 一个布尔值，指示向导是否应该以无提示方式运行，就像单击"完成" () 。 `TRUE` |

## <a name="context-parameters-for-add-sub-project"></a>添加子项目的上下文参数

| 参数 | 描述 |
|-------------------------| - |
| `WizardType` | 注册的向导 <xref:EnvDTE.Constants.vsWizardAddSubProject> () 或指示向导类型的 GUID。 在实现中，向导的 GUID 为 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] {0F90E1D2-4999-11D1-B6D1-00A0C90F2744}。 |
| `ProjectName` | 作为唯一项目名称 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的字符串。 |
| `ProjectItems` | 指向 `ProjectItems` 向导操作的集合的指针。 此指针根据项目层次结构选择传递给向导。 用户通常选择要将项放入的文件夹，然后调用项目的"添加项 **"** 对话框。 |
| `LocalDirectory` | 工作项目文件的本地位置。 |
| `ItemName` | 要添加的项的名称。 此名称是默认文件名或用户从"添加项"对话框中 **输入的文件名** 。 该名称基于在 *.vsdir* 文件中设置的标志。 该名称可以是 null 值。 |
| `InstallationDirectory` | 安装的目录 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 路径。 |
| `Silent` | 一个布尔值，指示向导是否应该以无提示方式运行，就像单击"完成" () 。 `TRUE` |

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2>
- 自定义参数
- [向导](../../extensibility/internals/wizards.md)
- [向导 (.vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
- [用于启动向导的上下文参数](/previous-versions/tz690efs(v=vs.140))