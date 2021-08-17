---
title: 打包&项中的部署信息
description: 使用功能属性、功能SharePoint、项目输出引用和安全控制实体在项目项中添加打包和部署数据。
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
ms.openlocfilehash: c9b9b91f97d1eb7f2025f3c96f588ddf1094491820e0c875b002c9b0ea0a415f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121409380"
---
# <a name="provide-packaging-and-deployment-information-in-project-items"></a>在项目项中提供打包和部署信息
  所有SharePoint项目项都有属性，在将项目部署到项目时，可以使用这些属性提供 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint。 这些属性如下所示：

- 功能属性

- 功能接收器

- 项目输出引用

- 安全控件项

  这些属性显示在"属性 **"** 窗口中。

## <a name="feature-properties"></a>功能属性
 使用 **"功能属性** "属性指定功能使用的数据。 功能属性数据是一组值， (作为键/值对存储) 在功能部署到 SharePoint 时随功能一起SharePoint。 部署功能后，可在代码中访问属性值。

 向项目项添加特征属性值时，该值作为元素添加到项的功能清单中。 例如，在业务数据 (BDC) 模型项目中，ModelFileName 功能属性显示为：

```xml
<Property Key="ModelFileName" Value="BdcModel1\BdcModel1.bdcm" />
```

 设置 Feature Property 值后，它将作为 FeatureProperty 元素添加到项目的 *.spdata* 文件中。 有关访问中属性的信息，SharePoint [SPFeaturePropertyCollection 类](/previous-versions/office/sharepoint-server/ms461895(v=office.15))。

 所有项目项中的相同功能属性值合并到功能清单中。 但是，如果两个不同的项目项使用不匹配的值指定相同的特征属性键，则会发生验证错误。

 若要将特征属性直接添加到 *.feature (文件) ，* 请SharePoint [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 对象模型方法 <xref:Microsoft.VisualStudio.SharePoint.Features.IPropertyCollection.Add%2A> 。 如果使用此方法，请注意，有关在功能属性中添加相同功能属性值的相同规则也适用于直接添加到功能文件的属性。

## <a name="feature-receiver"></a>功能接收器
 功能接收器是当项目项的包含功能发生特定事件时执行的代码。 例如，可以定义在安装、激活或升级功能时执行的功能接收器。 添加功能接收器的一种方式是直接将其添加到功能，如演练 [：添加功能事件接收器中所述](../sharepoint/walkthrough-add-feature-event-receivers.md)。 另一种方式是在功能接收器属性中引用功能接收器类 **名和** 程序集。

### <a name="direct-method"></a>直接方法
 将功能接收器直接添加到功能时，代码文件将放置在"功能 **"节点下的** 解决方案资源管理器。 生成 SharePoint 解决方案时，代码将编译为程序集并部署到SharePoint。 默认情况下，功能属性 **Receiver Assembly** 和 **Receiver Class** 引用类名称和程序集。

### <a name="reference-method"></a>Reference 方法
 添加功能接收器的另一种方式是使用项目项的"功能接收器"属性引用功能接收器程序集。 功能接收器属性值有两个子属性：**程序集和****类名**。 程序集必须使用其完全限定的"强"名称，并且类名必须是完整类型名称。 有关详细信息，请参阅[具有强名称的程序集](/previous-versions/dotnet/netframework-4.0/wd40t7ad(v=vs.100))。 将解决方案部署到 SharePoint，该功能使用引用的功能接收器来处理功能事件。

 在解决方案生成时，功能及其项目中的功能接收器属性值合并在一起，以在 SharePoint 解决方案 (*.wsp*) 文件的功能清单中设置 Feature 元素的 ReceiverAssembly 和 ReceiverClass 属性。 因此，如果同时指定了项目项和特征的 Assembly 和 Class Name 属性值，则项目项和特征属性值必须匹配。 如果值不匹配，将收到验证错误。 如果希望项目项引用功能接收器程序集，而不是其功能使用的功能接收器程序集，请将其移到另一个功能。

 如果引用尚未在服务器上的功能接收方程序集，则还必须在包中包括程序集文件本身; [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 不添加它。 部署该功能时，程序集文件将复制到系统或物理目录中SharePoint [!INCLUDE[TLA#tla_gac](../sharepoint/includes/tlasharptla-gac-md.md)] Bin 文件夹。 有关详细信息，请参阅如何： [如何：添加和删除其他程序集](../sharepoint/how-to-add-and-remove-additional-assemblies.md)。

 有关功能接收器的信息，请参阅[功能事件接收器](/previous-versions/office/developer/sharepoint-2007/bb862634(v=office.12))[和特征事件](/previous-versions/office/developer/sharepoint-2010/ms469501(v=office.14))。

## <a name="project-output-references"></a>Project输出引用
 "Project引用"属性指定项目项需要运行的依赖项（如程序集）。 例如，假设解决方案具有 BDC 项目和类项目。 如果 BDC 项目依赖于类项目输出的程序集，可以在 BDC 项目的"输出引用"属性中引用Project程序集。 打包 BDC 项目时，依赖程序集将包含在包中。

 Project引用通常是程序集，但在某些情况下， (Silverlight 项目) 可以是其他文件类型。

 有关详细信息，请参阅 [如何：添加项目输出引用](../sharepoint/how-to-add-a-project-output-reference.md)。

## <a name="safe-control-entries"></a>保险箱控件条目
 SharePoint提供了一种称为安全控制条目的安全机制，用于限制不受信任的用户访问某些控件。 根据设计SharePoint，不受信任的用户可以在 SharePoint 服务器上上传和创建 ASPX 页。 为了防止这些用户向 ASPX 页添加不安全代码，SharePoint限制他们访问 *安全控件*。 保险箱控件是 ASPX 控件和指定为安全的 Web 部件，网站上的任何用户都可以使用这些控件。 有关详细信息，请参阅步骤[4：将 Web](/previous-versions/office/developer/sharepoint-2007/ms581321(v=office.12))部件添加到保险箱列表。

 中SharePoint项目项都有一个称为"保险箱控件项"的属性，该属性具有两个布尔子属性：保险箱 和 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 保险箱 **脚本**。  “安全”属性指定不受信任的用户是否能访问控件。 "保险箱脚本"属性指定不受信任的用户是否可以查看和更改控件的属性。

 保险箱控件项是作为程序集引用的。 在项目项的"控件项"属性中输入安全控件项，保险箱 **项** 添加到项目的程序集。 但是，在将其他程序集添加到包时，还可通过包设计器中的"高级"选项卡将安全控件条目添加到项目的程序集。 有关详细信息，请参阅[如何：将控件标记为安全](../sharepoint/how-to-mark-controls-as-safe-controls.md)控件或将 Web 部件程序集注册为保险箱[控件](/previous-versions/office/developer/sharepoint2003/dd587360(v=office.11))。

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

## <a name="see-also"></a>请参阅
- [打包和部署SharePoint解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
- [使用模块包括解决方案中的文件](../sharepoint/using-modules-to-include-files-in-the-solution.md)
- [扩展SharePoint打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
