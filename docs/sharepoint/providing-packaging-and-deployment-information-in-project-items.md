---
title: 项目项中的打包和部署信息
description: 使用功能属性、功能接收器、项目输出引用和安全控制实体，在 SharePoint 项目项中添加打包和部署数据。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.SafeControlEntries
- VS.SharePointTools.Project.ProjectOutputReference
- VS.SharePointTools.Project.FeatureProperties
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, safe controls
- project output references [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, feature properties
- SharePoint development in Visual Studio, project output references
- SharePoint development in Visual Studio, advanced packaging tools
- feature properties [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, feature receiver
- feature receiver [SharePoint development in Visual Studio]
- safe controls [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 907bb1ed7131859dbf618c7b4b53e1d87b23e2ae
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602543"
---
# <a name="provide-packaging-and-deployment-information-in-project-items"></a>在项目项中提供打包和部署信息
  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的所有 SharePoint 项目项都具有可用于在将项目部署到 SharePoint 时提供其他数据的属性。 这些属性如下所示：

- 功能属性

- 功能接收器

- 项目输出引用

- 安全控件项

  这些属性将显示在“属性”窗口中。

## <a name="feature-properties"></a>功能属性
 使用“功能属性”属性指定功能使用的数据。 功能属性数据是在功能部署到 SharePoint 时所随附的一组值（以键/值对的形式存储）。 部署功能后，可在代码中访问属性值。

 向项目项添加功能属性值时，该值作为元素添加到项的功能清单中。 例如，在业务数据连接 (BDC) 模型项目中，ModelFileName 功能属性显示如下：

```xml
<Property Key="ModelFileName" Value="BdcModel1\BdcModel1.bdcm" />
```

 设置功能属性值后，它将作为 FeatureProperty 元素添加到项目的 .spdata 文件中。 有关在 SharePoint 中访问属性的信息，请参阅 [SPFeaturePropertyCollection 类](/previous-versions/office/sharepoint-server/ms461895(v=office.15))。

 所有项目项中的相同功能属性值合并到功能清单中。 但是，如果两个不同的项目项指定具有不匹配值的同一功能属性键，则会发生验证错误。

 若要将功能属性直接添加到功能文件 (.feature)，请调用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]SharePoint 对象模型方法<xref:Microsoft.VisualStudio.SharePoint.Features.IPropertyCollection.Add%2A>。 如果使用此方法，请注意，有关在功能属性中添加相同功能属性值的相同规则也适用于直接添加到功能文件的属性。

## <a name="feature-receiver"></a>功能接收器
 功能接收器是在项目项包含的功能中发生特定事件时执行的代码。 例如，可以定义在安装、激活或升级功能时执行的功能接收器。 添加功能接收器的一种方式是直接将其添加到功能，如[演练：添加功能事件接收器](../sharepoint/walkthrough-add-feature-event-receivers.md)中所述。 另一种方式是在“功能接收器”属性中引用功能接收器类名称和程序集。

### <a name="direct-method"></a>直接方法
 将功能接收器直接添加到功能时，代码文件将放置在解决方案资源管理器中“功能”节点下。 生成 SharePoint 解决方案时，代码会编译为程序集并部署到 SharePoint。 默认情况下，功能属性“接收器程序集”和“接收器类”引用类名称和程序集。

### <a name="reference-method"></a>Reference 方法
 添加功能接收器的另一种方式是使用项目项的“功能接收器”属性来引用功能接收器程序集。 功能接收器属性值有两个子属性：“程序集”和类名称” 。 程序集必须使用其完全限定的“强”名称，并且类名必须是完整类型名称。 有关详细信息，请参阅[具有强名称的程序集](/previous-versions/dotnet/netframework-4.0/wd40t7ad(v=vs.100))。 将解决方案部署到 SharePoint 后，功能使用引用的功能接收器来处理功能事件。

 在解决方案生成时，功能及其项目中的功能接收器属性值合并在一起，以设置 SharePoint 解决方案 (.wsp) 文件的功能清单中功能要素的 ReceiverAssembly 和 ReceiverClass 属性。 因此，如果同时指定了项目项和功能的“程序集”和“类名称”属性值，则项目项和功能属性值必须匹配。 如果值不匹配，将收到验证错误。 如果想要项目项引用功能接收器程序集，而不是其功能使用的功能接收器程序集，请将其移至另一个功能。

 如果引用尚未存在于服务器上的功能接收器程序集，则还必须在包中包含程序集文件本身；[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 不会为其添加它。 部署该功能时，会将程序集文件复制到系统的 [!INCLUDE[TLA#tla_gac](../sharepoint/includes/tlasharptla-gac-md.md)] 或 SharePoint 物理目录中的 Bin 文件夹。 有关详细信息，请查阅[操作说明：添加和移除其他程序集](../sharepoint/how-to-add-and-remove-additional-assemblies.md)。

 有关功能接收器的详细信息，请参阅[功能事件接收器](/previous-versions/office/developer/sharepoint-2007/bb862634(v=office.12))和[功能事件](/previous-versions/office/developer/sharepoint-2010/ms469501(v=office.14))。

## <a name="project-output-references"></a>项目输出引用
 “项目输出引用”属性指定依赖项，如项目项需要运行的程序集。 例如，假设解决方案具有 BDC 项目和类项目。 如果 BDC 项目依赖于类项目输出的程序集，可以在 BDC 项目的“项目输出引用”属性中引用程序集。 打包 BDC 项目时，依赖程序集将包含在包中。

 项目输出引用通常是程序集，但在某些情况下（例如 Silverlight 项目）可以是其他文件类型。

 有关更多信息，请参阅[操作说明：添加项目输出引用](../sharepoint/how-to-add-a-project-output-reference.md)。

## <a name="safe-control-entries"></a>安全控件项
 SharePoint 提供了一种称为安全控件项的安全机制，用于限制不受信任的用户访问某些控件。 根据设计，SharePoint 允许不受信任的用户在 SharePoint 服务器上上传和创建 ASPX 页。 为了防止这些用户向 ASPX 页添加不安全代码，SharePoint 限制他们对安全控件的访问权限。 安全控件指的是被指定为安全的 ASPX 控件和 Web 部件，网站上的任何用户都可以使用它们。 有关详细信息，请参阅[步骤 4：将 Web 部件添加到安全控件列表](/previous-versions/office/developer/sharepoint-2007/ms581321(v=office.12))。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的每个 SharePoint 项目项都有一个名为“安全控件项”的属性，该属性包含两个布尔子属性：“安全”和“安全应对脚本”。 “安全”属性指定不受信任的用户是否能访问控件。 “安全应对脚本”属性指定不受信任的用户是否可以查看和更改控件的属性。

 安全控件项是基于程序集引用的。 通过在项目项的“安全控件项”属性中输入安全控制项，将其添加到项目的程序集中。 但是，在将其他程序集添加到包时，还可通过“包设计器”中的“高级”选项卡将安全控件项添加到项目的程序集中。 有关详细信息，请参阅[操作说明：将控件标记为安全控件](../sharepoint/how-to-mark-controls-as-safe-controls.md)或[将 Web 部件程序集注册为安全控件](/previous-versions/office/developer/sharepoint2003/dd587360(v=office.11))。

### <a name="xml-entries-for-safe-controls"></a>安全控件的 XML 条目
 将安全控件项添加到项目项或项目程序集时，将按照以下格式将引用写入包清单：

```xml
<Assemblies>
    <Assembly Location="<assembly name>.dll"
      DeploymentTarget="<'GlobalAssemblyCache' or 'WebApplication'">>
        <SafeControls>
            <SafeControl Assembly="<assembly name>.dll" Namespace=
              "<SharePoint project name>" Safe="<true/false>"
                TypeName="<control name>"
                SafeAgainstScript="<true/false>" />
        </SafeControls>
    </Assembly>
</Assemblies>
```

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
- [使用模块包括解决方案中的文件](../sharepoint/using-modules-to-include-files-in-the-solution.md)
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
