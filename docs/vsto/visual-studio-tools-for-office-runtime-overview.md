---
title: Visual Studio Tools for Office运行时概述
description: Visual Studio最终用户计算机上安装 Office 2010 Tools for Office，以运行使用 Microsoft Office 开发人员工具创建的解决方案。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office runtime [Office development in Visual Studio], about Office runtime
- VSTOLoader.dll
- runtime loader [Office development in Visual Studio]
- Office runtime [Office development in Visual Studio], assemblies
- Office runtime [Office development in Visual Studio]
- runtime [Office development in Visual Studio], assemblies
- vstoee.dll
- Visual Studio Tools for Office runtime
- Office solutions [Office development in Visual Studio], runtime
- solutions [Office development in Visual Studio], runtime
- versions [Office development in Visual Studio], runtime
- assemblies [Office development in Visual Studio], runtime
- runtime [Office development in Visual Studio], about VSTO runtime
- solution loader [Office development in Visual Studio]
- runtime [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 0bf686a1002f3c7de6c3d91ec7e95ac48761e2085e25d62330774dcc31c4db54
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121365843"
---
# <a name="visual-studio-tools-for-office-runtime-overview"></a>Visual Studio Tools for Office运行时概述
  若要运行使用 Visual Studio 中的 Microsoft Office 开发人员工具创建的解决方案，必须在最终用户计算机上安装 Visual Studio 2010 Tools for Office Runtime。 有关详细信息，请参阅[如何：安装Visual Studio Tools for Office可再发行组件](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)。 Visual Studio 2010 Tools for Office 运行时由两个主要组件组成：

- Office 的 .NET Framework 扩展。 这些组件是提供解决方案和 Microsoft Office 应用程序之间的通信层的托管程序集。 有关详细信息，请参阅了解[Office 的扩展.NET Framework。](#officeextensions)

- Office 解决方案加载程序。 此组件是 Office 应用程序用于加载运行时和解决方案的一组非托管 DLL。 有关详细信息，请参阅[了解解决方案Office加载程序](#UnmanagedLoader)。

  可以通过多种不同的方法安装运行时。 根据计算机上的配置，安装运行时期间将安装不同的运行时组件。 有关详细信息，请参阅 Visual Studio Tools for Office[安装方案](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)。

## <a name="understand-the-office-extensions-for-the-net-framework"></a><a name="officeextensions"></a>了解Office的扩展.NET Framework
 Visual Studio 2010 Tools for Office 运行时包括 Office 3.5 .NET Framework 3.5 及更高版本的 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 扩展。 以 .NET Framework 各版本为目标的解决方法使用该版本适用的扩展。

 这两种扩展包括解决方案用于自动处理和扩展 Office 应用程序的程序集。 在创建新的 Office 项目时，Visual Studio 会自动添加对项目类型和项目的目标 .NET Framework 使用的程序集的引用。 有关这些扩展中的程序集Office，请参阅运行时[中的Visual Studio Tools for Office程序集](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md)。

### <a name="design-differences-in-the-office-extensions"></a>扩展插件Office差异
 在 Office 的 .NET Framework 3.5 扩展中使用的多数类型是类。 这些是 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]的早期版本中包含的相同的类。 相反，你在 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的 Office 扩展中使用的大多数类型都是接口。 例如，如果面向的是 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，则 <xref:Microsoft.Office.Tools.Excel.Worksheet> 和 <xref:Microsoft.Office.Tools.Word.Document> 类型是接口而不是类。

 大多数情况下，无论你的解决方案面向 .NET Framework 3.5 还是 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]，在 Office 解决方案中编写的代码都是相同的。 但是，如果面向 .NET Framework 的不同版本，则某些功能需要不同的代码。 有关详细信息，请参阅将[Office 解决方案迁移到 .NET Framework 4 或更高版本](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)。

### <a name="interfaces-in-the-office-extensions-for-the-net-framework-4-or-later"></a>Office 4 或更高版本的 .NET Framework 扩展中的接口
 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的的 Office 扩展中的大多数接口不应由用户代码实现。 用户只能实现名称以字母 **I** 开头的接口，如 <xref:Microsoft.Office.Tools.Excel.ISmartTagExtension>。

 不以字母 **I** 开头的所有接口都由 Visual Studio 2010 Tools for Office 运行时在内部实现，这些接口可能会在将来版本中更改。 若要创建实现这些接口的对象，请在项目使用由 `Globals.Factory` 对象提供的方法。 例如，若要获取实现 <xref:Microsoft.Office.Tools.Excel.SmartTag> 接口的对象，请使用 `Globals.Factory.CreateSmartTag` 方法。 有关 有关详细信息 `Globals.Factory` ，请参阅[对项目 中的对象的全局Office访问](../vsto/global-access-to-objects-in-office-projects.md)。

### <a name="enable-type-equivalence-and-embedded-types-in-projects-that-target-the-net-framework-4-or-later"></a>在面向 4 或更高版本的项目中启用类型等效.NET Framework嵌入类型
 由于 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的 Office 扩展的对象模型基于接口，因此你可使用 Visual Studio 中的 Visual C# 和 Visual Basic 的类型等效性功能，将类型信息从 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 嵌入你的解决方案。 此功能使 Office 解决方案和 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 的版本相互独立。 例如，如果解决方案将 <xref:Microsoft.Office.Tools.Word.Document> 接口用作嵌入类型，而运行时的下一个版本向 <xref:Microsoft.Office.Tools.Word.Document> 接口添加成员，则该解决方案仍适用于运行时的下一个版本。 如果解决方案不将 <xref:Microsoft.Office.Tools.Word.Document> 接口用作嵌入类型，则该解决方案将不再适用于运行时的下一个版本。

 默认情况下，在创建面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的 Office 项目时不会启用类型等效性功能。 如果要启用此功能，请将项目中以下任何程序集引用的 **“嵌入互操作类型”** 属性设置为 **“True”**：

- Microsoft.Office.Tools.dll

- Microsoft.Office.Tools.Common.dll

- Microsoft.Office.Tools.Excel.dll

- Microsoft.Office.Tools.Outlook.dll

- Microsoft.Office.Tools.Word.dll

  进行此更改后，项目所使用的所有运行时类型的类型信息都会在生成该项目时嵌入到解决方案程序集中。 解决方案在运行时会使用此嵌入类型信息（而不是所引用的程序集中的类型信息）。

## <a name="understand-the-office-solution-loader"></a><a name="UnmanagedLoader"></a>了解 Office 解决方案加载程序
 Visual Studio Tools for Office Runtime 包含一些非托管 DLL，Office 应用程序使用这些 DLL 加载运行时和 Office 解决方案。 虽然从来不必直接使用这些 DLL，但是知道这些 DLL 的用途可以帮助你更好地了解 Office 解决方案的体系结构。

 有关在加载过程中如何使用这些组件的信息，请参阅文档级自定义项[](../vsto/architecture-of-document-level-customizations.md)的体系结构和外接程序[VSTO体系结构](../vsto/architecture-of-vsto-add-ins.md)。

### <a name="vstoeedll"></a>vstoee.dll
 当用户打开文档级自定义项或启动 VSTO 外接程序时，Office应用程序VSTOEE.dll以执行加载 所需的任务 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。

 *VSTOEE.dll* 确保为解决方案加载了正确的 版本，并且加载了已安装版本的 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] Office。 虽然 可以在同一计算机上安装多个版本的 ，但一 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] *次* VSTOEE.dll一个实例。 这是 *VSTOEE.dll* 计算机上安装的最新版本运行时中包含的版本。 有关可用于其他解决方案的 的不同版本的更多信息，请参阅在不同版本的 Microsoft Office [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 中[运行解决方案](../vsto/running-solutions-in-different-versions-of-microsoft-office.md)。

### <a name="vstoloaderdll"></a>VSTOLoader.dll
 在 *VSTOEE.dll* 加载 的适当版本的 后，VSTOLoader.dll将执行加载解决方案程序集 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 所需的大部分工作。  *VSTOLoader.dll* 可进行多项操作：

- 它为每个解决方案程序集创建一个应用程序域。

- 它执行一组安全性检查以验证解决方案程序集是否有运行的权限。

- 它加载解决方案所需的 Office 的 .NET Framework 扩展的版本。

  *VSTOLoader.dll* 还执行特定于外接程序VSTO几项操作：

- 它实现 <xref:Extensibility.IDTExtensibility2> 接口。 <xref:Extensibility.IDTExtensibility2> 是一个 Microsoft Office 应用程序的所有 VSTO 外接程序都必须实现的 COM 接口。 此接口定义应用程序为与 VSTO 外接程序通信而调用的方法。

- 它实现 IManagedAddin 接口。 此接口由 Office 应用程序用来帮助加载VSTO外接程序。有关详细信息，请参阅[IManagedAddin 接口](../vsto/imanagedaddin-interface.md)。

## <a name="understand-the-32-bit-and-64-bit-versions-of-the-runtime"></a>了解运行时的 32 位和 64 位版本
 有单独的 64 位和 32 位版本的 Visual Studio 2010 Tools for Office 运行时。 这两种运行时版本用于在 64 位和 32 位版本的 Office 中运行解决方案。 下表显示 Windows 与 Office 的各种组合所需的运行时版本。

|Windows 版本|Microsoft Office 版本|所需的 Visual Studio Tools for Office Runtime 版本|
|------------------------|---------------------------------|--------------------------------------------------------------------|
|32 位|32 位|32 位|
|64 位|32 位|64 位|
|64 位|64 位|64 位|

 安装 Office 时，所需版本的 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 将与 Office 一起安装。 例如，在 64 位版本的 Windows 上安装 64 位版本的 Office 时，也会安装 64 位版本的 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。 有关使用 Office 安装 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] [Visual Studio Tools for Office，请参阅运行时安装方案](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)。

 64 位版本的 Office 也可以运行在 Visual Studio 2008 中使用 2007 Microsoft Office 系统的项目模板创建的 Office 解决方案。 不过，该版本不能运行在 Visual Studio 2008 中使用 Microsoft Office 2003 项目模板创建的 Office 解决方案，或使用 Visual Studio 2005 创建的 Office 解决方案。 有关详细信息，请参阅在不同版本的 Microsoft Office 中[运行解决方案](../vsto/running-solutions-in-different-versions-of-microsoft-office.md)。

## <a name="repair-the-visual-studio-2010-tools-for-office-runtime"></a>修复 Visual Studio 2010 Tools for Office Runtime
 如果需要修复此运行时，请在“控制面板”中打开 **“程序和功能”** 或 **“添加或删除程序”** ，在程序列表中选择 **“Microsoft Visual Studio 2010 Tools for Office Runtime”** ，然后单击 **“卸载”**。 通过运行的安装程序即可修复此运行时。 如果单击 **“更改”**，则不会向你提供用于修复此运行时的选项。

## <a name="see-also"></a>另请参阅
- [Visual Studio Tools for Office运行时安装方案](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)
- [运行时中的Visual Studio Tools for Office程序集](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md)
- [解决方案Office体系结构Visual Studio](../vsto/architecture-of-office-solutions-in-visual-studio.md)
- [文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [如何：在 Office 创建Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [升级和迁移Office解决方案](../vsto/upgrading-and-migrating-office-solutions.md)
