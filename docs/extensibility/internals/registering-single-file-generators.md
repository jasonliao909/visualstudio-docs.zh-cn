---
title: 注册单文件生成器|Microsoft Docs
description: 了解如何在 Visual Studio中注册自定义工具，以将其实例化并将其与特定项目类型关联。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, custom tools
- custom tools, defining registry settings
ms.assetid: db7592c0-1273-4843-9617-6e2ddabb6ca8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: ad56731f0e0432dea2eb583d23dcf4285801e2f6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122062945"
---
# <a name="registering-single-file-generators"></a>注册单个文件生成器
若要在 中提供自定义工具，必须注册它，以便可以实例化它，并 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 关联到特定的项目类型。

### <a name="to-register-a-custom-tool"></a>注册自定义工具

1. 在本地注册表或系统注册表中，在 HKEY_CLASSES_ROOT [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 下注册自定义工具 DLL。

    例如，下面是随附的托管 MSDataSetGenerator 自定义工具的注册信息 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ：

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\CLSID\{E76D53CC-3D4F-40A2-BD4D-4F3419755476}]
   @="COM+ class: Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"
   "InprocServer32"="C:\\WINDOWS\\system32\\mscoree.dll"
   "ThreadingModel"="Both"
   "Class"="Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"
   "Assembly"="Microsoft.VSDesigner, Version=14.0.0.0, Culture=Neutral, PublicKeyToken=b03f5f7f11d50a3a"
   ```

2. 在所需配置单元的"生成器 GUID"下创建注册表项，其中 GUID 是由特定语言的项目系统或服务定义的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] \\ GUID。  密钥的名称将成为自定义工具的编程名称。 自定义工具键具有以下值：

   - （默认值）

        可选。 提供自定义工具的用户友好说明。 此参数是可选的，但建议这样做。

   - CLSID

        必需。 指定实现 的 COM 组件的类库的标识符 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> 。

   - GeneratesDesignTimeSource

        必需。 指示此自定义工具生成的文件的类型是否可供可视化设计器使用。 对于不可用于可视化设计器的类型，此参数的值 (为零) 0;对于可用于可视化设计器的类型， (为) 1。

   > [!NOTE]
   > 必须为希望自定义工具可用的每种语言单独注册自定义工具。

    例如，MSDataSetGenerator 针对每种语言注册一次自身：

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{164b10b9-b200-11d0-8c61-00a0c91e29d5}\MSDataSetGenerator]
   @="Microsoft VB Code Generator for XSD"
   "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"
   "GeneratesDesignTimeSource"=dword:00000001

   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{fae04ec1-301f-11d3-bf4b-00c04f79efbc}\MSDataSetGenerator]
   @="Microsoft C# Code Generator for XSD"
   "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"
   "GeneratesDesignTimeSource"=dword:00000001
   ```

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>
- [实现单个文件生成器](../../extensibility/internals/implementing-single-file-generators.md)
- [向可视化设计器公开类型](../../extensibility/internals/exposing-types-to-visual-designers.md)
- [BuildManager 对象介绍](/previous-versions/8f9kffa8(v=vs.140))