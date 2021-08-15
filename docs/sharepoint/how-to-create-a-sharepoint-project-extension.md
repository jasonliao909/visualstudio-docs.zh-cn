---
title: 如何：创建SharePoint Project扩展|Microsoft Docs
description: 了解如何创建项目扩展，以便可以将功能添加到在 SharePoint 中打开的任何Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 04/28/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 63bfc09edca9a87df95893758ffe4a6a8c85a465eb8cb23cc6c7d97416361eea
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121352937"
---
# <a name="how-to-create-a-sharepoint-project-extension"></a>如何：创建SharePoint扩展
  若要将功能添加到在 SharePoint 打开的任何项目，请创建项目Visual Studio。 有关详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

### <a name="to-create-a-project-extension"></a>创建项目扩展

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio。SharePoint

    - System.ComponentModel.Composition

3. 创建实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 接口的类。

4. 将 <xref:System.ComponentModel.Composition.ExportAttribute> 添加到 类。 此属性使Visual Studio发现和加载 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 类型传递给属性构造函数。

5. 在 方法的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> 实现中，使用 *projectService* 参数的成员来定义扩展的行为。 此参数是 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 一个对象，提供对接口中定义的事件 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents> 的访问。

## <a name="example"></a>示例
 下面的代码示例演示如何创建一个简单的项目扩展，该扩展SharePoint接口定义的大多数项目 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents> 事件。 若要测试代码，请SharePoint项目，然后将更多项目添加到解决方案、更改项目属性值或删除 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 或排除项目。 该扩展通过向"输出"窗口和"错误列表"窗口 **写入** 消息 **来通知事件** 。

  ```vb
    Imports Microsoft.VisualStudio.SharePoint
    Imports System.ComponentModel
    Imports System.ComponentModel.Composition

    Namespace Contoso.ExampleProjectExtension
      <Export(GetType(ISharePointProjectExtension))> _
      Class ExampleProjectExtension
        Implements ISharePointProjectExtension

        Private WithEvents projectService As ISharePointProjectService

        Public Sub Initialize(ByVal projectService As ISharePointProjectService) _
            Implements ISharePointProjectExtension.Initialize
            Me.projectService = projectService
        End Sub

        ' A project was added.
        Private Sub projectService_ProjectAdded(ByVal sender As Object, ByVal e As SharePointProjectEventArgs) _
            Handles projectService.ProjectAdded
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The following project was added: {0}", e.Project.Name)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub

        ' A project was loaded in the IDE.
        Private Sub projectService_ProjectInitialized(ByVal sender As Object, ByVal e As SharePointProjectEventArgs) _
            Handles projectService.ProjectInitialized
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The following project is being initialized: {0}", e.Project.Name)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub

        ' The name of a property was changed.
        Private Sub projectService_ProjectNameChanged(ByVal sender As Object, ByVal e As NameChangedEventArgs) _
            Handles projectService.ProjectNameChanged
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The project named {0} was changed to {1}.", e.OldName, project.Name)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub

        ' A project property value was changed.
        Private Sub ProjectPropertyChanged(ByVal sender As Object, ByVal e As PropertyChangedEventArgs) _
            Handles projectService.ProjectPropertyChanged
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The following property of the {0} project was changed: {1}",
                project.Name, e.PropertyName)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub

        ' A project is being removed or unloaded.
        Private Sub projectService_ProjectRemoved(ByVal sender As Object, ByVal e As SharePointProjectEventArgs) _
            Handles projectService.ProjectRemoved
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The following project is being removed or unloaded: {0}", e.Project.Name)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub

        ' A project was removed or unloaded.
        Private Sub projectService_ProjectDisposing(ByVal sender As Object, ByVal e As SharePointProjectEventArgs) _
            Handles projectService.ProjectDisposing
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The following project was removed or unloaded: {0}", e.Project.Name)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub
      End Class
    End Namespace
    ```

    ```csharp
    using Microsoft.VisualStudio.SharePoint;
    using System;
    using System.ComponentModel;
    using System.ComponentModel.Composition;

    namespace Contoso.ExampleProjectExtension
    {
      [Export(typeof(ISharePointProjectExtension))]
      internal class ExampleProjectExtension : ISharePointProjectExtension
      {
        public void Initialize(ISharePointProjectService projectService)
        {
            projectService.ProjectAdded += projectService_ProjectAdded;
            projectService.ProjectInitialized += projectService_ProjectInitialized;
            projectService.ProjectNameChanged += projectService_ProjectNameChanged;
            projectService.ProjectPropertyChanged += projectService_ProjectPropertyChanged;
            projectService.ProjectRemoved += projectService_ProjectRemoved;
            projectService.ProjectDisposing += projectService_ProjectDisposing;
        }

        // A project was added.
        void projectService_ProjectAdded(object sender, SharePointProjectEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The following project was added: {0}", e.Project.Name);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }

        // A project is loaded in the IDE.
        void projectService_ProjectInitialized(object sender, SharePointProjectEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The following project is being initialized: {0}", e.Project.Name);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }

        // The name of a project was changed.
        void projectService_ProjectNameChanged(object sender, NameChangedEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The project named {0} was changed to {1}.", e.OldName, project.Name);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }

        // A project property value was changed.
        private void projectService_ProjectPropertyChanged(object sender, PropertyChangedEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The following property of the {0} project was changed: {1}",
                project.Name, e.PropertyName);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }

        // A project is being removed or unloaded.
        void projectService_ProjectRemoved(object sender, SharePointProjectEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The following project is being removed or unloaded: {0}", e.Project.Name);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }

        // A project was removed or unloaded.
        void projectService_ProjectDisposing(object sender, SharePointProjectEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The following project was removed or unloaded: {0}", e.Project.Name);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }
     }
  }
  ```

此示例使用 SharePoint 项目服务将消息写入"输出 **"窗口和**"**错误列表"** 窗口。 有关详细信息，请参阅使用[SharePoint 项目服务。](../sharepoint/using-the-sharepoint-project-service.md)

 有关演示如何处理 和 事件的示例，请参阅如何：向项目添加SharePoint菜单项和如何：向项目添加SharePoint <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> [项](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)。 [](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio。SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署扩展，请为程序集 (VSIX) 包以及要随扩展一起分发的其他任何文件 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建扩展。 有关详细信息，请参阅 在 Visual Studio 中为 SharePoint[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

## <a name="see-also"></a>另请参阅
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
- [如何：向项目添加SharePoint菜单项](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)
- [如何：向项目SharePoint属性](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [演练：创建SharePoint扩展](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)
