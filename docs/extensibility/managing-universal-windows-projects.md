---
title: 管理通用Windows项目|Microsoft Docs
description: 若要支持通用Windows应用，Visual Studio管理项目的扩展应了解通用Windows应用项目结构。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 47926aa1-3b41-410d-bca8-f77fc950cbe7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: d6e34a8cb8da8158eae9e6c245da45fa37d59b4e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664269"
---
# <a name="manage-universal-windows-projects"></a>管理通用Windows项目

通用Windows应用是面向 Windows 8.1 Windows Phone 8.1 的应用，允许开发人员在这两个平台上使用代码和其他资产。 共享代码和资源保留在共享项目中，而特定于平台的代码和资源保留在单独的项目中，一个项目用于 Windows，另一个用于Windows Phone。 有关通用应用Windows，请参阅[通用Windows应用](/windows/uwp/get-started/create-uwp-apps)。 Visual Studio管理项目的扩展应注意，Windows应用项目的通用扩展具有与单平台应用不同的结构。 本演练演示如何导航共享项目和管理共享项。

## <a name="prerequisites"></a>先决条件

从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

### <a name="navigate-the-shared-project"></a>导航共享项目

1. 创建名为 **TestUniversalProject** 的 C# VSIX 项目。  (  >  **文件**  >  **""新建Project"，** 然后选择 **"C#**  >  **扩展** 性  >  **Visual Studio包) 。** 将自定义 **命令** 项目项模板 (添加到解决方案资源管理器，右键单击项目节点并选择"添加新项"，然后转到"扩展性  >  ") 。  将文件 **"TestUniversalProject"命名**。

2. 在"扩展 *"Microsoft.VisualStudio.Shell.Interop.12.1.DesignTime.dllMicrosoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll(***添加** 对) 的引用。

3. 打开 *TestUniversalProject.cs* 并添加以下 `using` 指令：

    ```csharp
    using EnvDTE;
    using EnvDTE80;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.PlatformUI;
    using Microsoft.Internal.VisualStudio.PlatformUI;
    using System.Collections.Generic;
    using System.IO;
    using System.Windows.Forms;
    ```

4. 在 `TestUniversalProject` 类中，添加指向"输出"窗口 **的私有** 字段。

    ```csharp
    public sealed class TestUniversalProject
    {
        IVsOutputWindowPane output;
    . . .
    }
    ```

5. 在 TestUniversalProject 构造函数中设置对输出窗格的引用：

    ```csharp
    private TestUniversalProject(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException("package");
        }

        this.package = package;

        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        if (commandService != null)
        {
            CommandID menuCommandID = new CommandID(MenuGroup, CommandId);
            EventHandler eventHandler = this.ShowMessageBox;
            MenuCommand menuItem = new MenuCommand(eventHandler, menuCommandID);
            commandService.AddCommand(menuItem);
        }

        // get a reference to the Output window
        output = (IVsOutputWindowPane)ServiceProvider.GetService(typeof(SVsGeneralOutputWindowPane));
    }
    ```

6. 从 方法中删除现有 `ShowMessageBox` 代码：

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
    }
    ```

7. 获取 DTE 对象，我们将在此演练中用于多种不同目的。 此外，请确保在单击菜单按钮时加载解决方案。

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        var dte = (EnvDTE.DTE)this.ServiceProvider.GetService(typeof(EnvDTE.DTE));
        if (dte.Solution != null)
        {
            . . .
        }
        else
        {
            MessageBox.Show("No solution is open");
            return;
        }
    }
    ```

8. 查找共享项目。 共享项目是纯容器;它不会生成或生成输出。 以下方法通过查找具有共享项目功能的对象来查找解决方案 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 中的第一个共享项目。

    ```csharp
    private IVsHierarchy FindSharedProject()
    {
        var sln = (IVsSolution)this.ServiceProvider.GetService(typeof(SVsSolution));
        Guid empty = Guid.Empty;
        IEnumHierarchies enumHiers;

        //get all the projects in the solution
        ErrorHandler.ThrowOnFailure(sln.GetProjectEnum((uint)__VSENUMPROJFLAGS.EPF_LOADEDINSOLUTION, ref empty, out enumHiers));
        foreach (IVsHierarchy hier in ComUtilities.EnumerableFrom(enumHiers))
        {
            if (PackageUtilities.IsCapabilityMatch(hier, "SharedAssetsProject"))
            {
                return hier;
            }
        }
        return null;
    }
    ```

9. 在 方法中，输出 (共享项目的名称解决方案资源管理器) `ShowMessageBox` 项目名称。 

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        var dte = (DTE)this.ServiceProvider.GetService(typeof(DTE));

        if (dte.Solution != null)
        {
            var sharedHier = this.FindSharedProject();
            if (sharedHier != null)
            {
                string sharedCaption = HierarchyUtilities.GetHierarchyProperty<string>(sharedHier, (uint)VSConstants.VSITEMID.Root,
                     (int)__VSHPROPID.VSHPROPID_Caption);
                output.OutputStringThreadSafe(string.Format("Found shared project: {0}\n", sharedCaption));
            }
            else
            {
                MessageBox.Show("Solution has no shared project");
                return;
            }
        }
        else
        {
            MessageBox.Show("No solution is open");
            return;
        }
    }
    ```

10. 获取活动平台项目。 平台项目是包含特定于平台的代码和资源的项目。 以下方法使用 new 字段 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy> 获取活动平台项目。

    ```csharp
    private IVsHierarchy GetActiveProjectContext(IVsHierarchy hierarchy)
    {
        IVsHierarchy activeProjectContext;
        if (HierarchyUtilities.TryGetHierarchyProperty(hierarchy, (uint)VSConstants.VSITEMID.Root,
             (int)__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy, out activeProjectContext))
        {
            return activeProjectContext;
        }
        else
        {
            return null;
        }
    }
    ```

11. 在 `ShowMessageBox` 方法中，输出活动平台项目的标题。

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        var dte = (DTE)this.ServiceProvider.GetService(typeof(DTE));

        if (dte.Solution != null)
        {
            var sharedHier = this.FindSharedProject();
            if (sharedHier != null)
            {
                string sharedCaption = HierarchyUtilities.GetHierarchyProperty<string>(sharedHier, (uint)VSConstants.VSITEMID.Root,
                     (int)__VSHPROPID.VSHPROPID_Caption);
                output.OutputStringThreadSafe(string.Format("Shared project: {0}\n", sharedCaption));

                var activePlatformHier = this.GetActiveProjectContext(sharedHier);
                if (activePlatformHier != null)
                {
                    string activeCaption = HierarchyUtilities.GetHierarchyProperty<string>(activePlatformHier,
                         (uint)VSConstants.VSITEMID.Root, (int)__VSHPROPID.VSHPROPID_Caption);
                    output.OutputStringThreadSafe(string.Format("Active platform project: {0}\n", activeCaption));
                }
                else
                {
                    MessageBox.Show("Shared project has no active platform project");
                }
            }
            else
            {
                MessageBox.Show("Solution has no shared project");
            }
        }
        else
        {
            MessageBox.Show("No solution is open");
        }
    }
    ```

12. 浏览平台项目。 以下方法获取从共享 (导入) 项目的所有导入内容。

    ```csharp
    private IEnumerable<IVsHierarchy> EnumImportingProjects(IVsHierarchy hierarchy)
    {
        IVsSharedAssetsProject sharedAssetsProject;
        if (HierarchyUtilities.TryGetHierarchyProperty(hierarchy, (uint)VSConstants.VSITEMID.Root,
            (int)__VSHPROPID7.VSHPROPID_SharedAssetsProject, out sharedAssetsProject)
            && sharedAssetsProject != null)
        {
            foreach (IVsHierarchy importingProject in sharedAssetsProject.EnumImportingProjects())
            {
                yield return importingProject;
            }
        }
    }
    ```

    > [!IMPORTANT]
    > 如果用户在实验性实例中Windows C++ 通用应用项目，上述代码将引发异常。 这是一个已知问题。 若要避免此异常，请将 `foreach` 上面的 块替换为以下内容：

    ```csharp
    var importingProjects = sharedAssetsProject.EnumImportingProjects();
    for (int i = 0; i < importingProjects.Count; ++i)
    {
        yield return importingProjects[i];
    }
    ```

13. 在 `ShowMessageBox` 方法中，输出每个平台项目的标题。 在输出活动平台项目标题的行后插入以下代码。 此列表只显示已加载的平台项目。

    ```csharp
    output.OutputStringThreadSafe("Platform projects:\n");

    IEnumerable<IVsHierarchy> projects = this.EnumImportingProjects(sharedHier);

    bool isActiveProjectSet = false;
    foreach (IVsHierarchy platformHier in projects)
    {
        string platformCaption = HierarchyUtilities.GetHierarchyProperty<string>(platformHier, (uint)VSConstants.VSITEMID.Root,
            (int)__VSHPROPID.VSHPROPID_Caption);
        output.OutputStringThreadSafe(string.Format(" * {0}\n", platformCaption));
    }
    ```

14. 更改活动平台项目。 以下方法使用 设置活动项目 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A> 。

    ```csharp
    private int SetActiveProjectContext(IVsHierarchy hierarchy, IVsHierarchy activeProjectContext)
    {
        return hierarchy.SetProperty((uint)VSConstants.VSITEMID.Root, (int)__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy, activeProjectContext);
    }
    ```

15. 在 `ShowMessageBox` 方法中，更改活动平台项目。 在 块内插入此 `foreach` 代码。

    ```csharp
    bool isActiveProjectSet = false;
    string platformCaption = null;
    foreach (IVsHierarchy platformHier in projects)
    {
        platformCaption = HierarchyUtilities.GetHierarchyProperty<string>(platformHier, (uint)VSConstants.VSITEMID.Root,
             (int)__VSHPROPID.VSHPROPID_Caption);
        output.OutputStringThreadSafe(string.Format(" * {0}\n", platformCaption));

        // if this project is neither the shared project nor the current active platform project,
        // set it to be the active project
        if (!isActiveProjectSet && platformHier != activePlatformHier)
        {
            this.SetActiveProjectContext(sharedHier, platformHier);
            activePlatformHier = platformHier;
            isActiveProjectSet = true;
        }
    }
    output.OutputStringThreadSafe("set active project: " + platformCaption +'\n');
    ```

16. 现在尝试一下。按 F5 启动实验实例。 在"新建应用"对话框中的" ("visual **C#** Windows Windows 8 **Project** 通用中心应用") 中，在试验实例Windows创建 C#  >    >  **通用** 中心  >    >  应用项目。 加载解决方案后，转到"工具"菜单，单击"**调用 TestUniversalProject"，** 然后在"输出 **"窗格中检查** 文本。 会看到下面这样的内容：

    ```
    Found shared project: HubApp.Shared
    The active platform project: HubApp.Windows
    Platform projects:
     * HubApp.Windows
     * HubApp.WindowsPhone
    set active project: HubApp.WindowsPhone
    ```

### <a name="manage-the-shared-items-in-the-platform-project"></a>管理平台项目中的共享项

1. 在平台项目中查找共享项。 共享项目中的项在平台项目中显示为共享项。 在"项目"中看不到解决方案资源管理器，但可以演练项目层次结构来查找它们。 以下方法将引导层次结构并收集所有共享项。 它可以选择输出每个项的标题。 共享项由新属性 标识 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7.VSHPROPID_IsSharedItem> 。

    ```csharp
    private void InspectHierarchyItems(IVsHierarchy hier, uint itemid, int level, List<uint> itemIds, bool getSharedItems, bool printItems)
    {
        string caption = HierarchyUtilities.GetHierarchyProperty<string>(hier, itemid, (int)__VSHPROPID.VSHPROPID_Caption);
        if (printItems)
            output.OutputStringThreadSafe(string.Format("{0}{1}\n", new string('\t', level), caption));

        // if getSharedItems is true, inspect only shared items; if it's false, inspect only unshared items
        bool isSharedItem;
        if (HierarchyUtilities.TryGetHierarchyProperty(hier, itemid, (int)__VSHPROPID7.VSHPROPID_IsSharedItem, out isSharedItem)
            && (isSharedItem == getSharedItems))
        {
            itemIds.Add(itemid);
        }

        uint child;
        if (HierarchyUtilities.TryGetHierarchyProperty(hier, itemid, (int)__VSHPROPID.VSHPROPID_FirstChild, Unbox.AsUInt32, out child)
            && child != (uint)VSConstants.VSITEMID.Nil)
        {
            this.InspectHierarchyItems(hier, child, level + 1, itemIds, isSharedItem, printItems);

            while (HierarchyUtilities.TryGetHierarchyProperty(hier, child, (int)__VSHPROPID.VSHPROPID_NextSibling, Unbox.AsUInt32, out child)
                && child != (uint)VSConstants.VSITEMID.Nil)
            {
                this.InspectHierarchyItems(hier, child, level + 1, itemIds, isSharedItem, printItems);
            }
        }
    }
    ```

2. 在 `ShowMessageBox` 方法中，添加以下代码以演练平台项目层次结构项。 将其插入 `foreach` 块内。

    ```csharp
    output.OutputStringThreadSafe("Walk the active platform project:\n");
    var sharedItemIds = new List<uint>();
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);
    ```

3. 读取共享项。 共享项在平台项目中显示为隐藏的链接文件，你可以读取所有属性作为普通链接文件。 以下代码读取第一个共享项的完整路径。

    ```csharp
    var sharedItemId = sharedItemIds[0];
    string fullPath;
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));
    output.OutputStringThreadSafe(string.Format("Shared item full path: {0}\n", fullPath));
    ```

4. 现在尝试一下。按 **F5** 启动实验实例。 在"新建 **Project"** 对话框的实验实例 (中创建 C# 通用中心应用项目 **，Visual C#** Windows Windows 8 通用中心应用) 转到"工具"菜单，单击"  >    >    >    >  **调用 TestUniversalProject"，** 然后检查"输出"窗格中的文本。 会看到下面这样的内容：

    ```
    Found shared project: HubApp.Shared
    The active platform project: HubApp.Windows
    Platform projects:
     * HubApp.Windows
     * HubApp.WindowsPhone
    set active project: HubApp.WindowsPhone
    Walk the active platform project:
        HubApp.WindowsPhone
            <HubApp.Shared>
                App.xaml
                    App.xaml.cs
                Assets
                    DarkGray.png
                    LightGray.png
                    MediumGray.png
                Common
                    NavigationHelper.cs
                    ObservableDictionary.cs
                    RelayCommand.cs
                    SuspensionManager.cs
                DataModel
                    SampleData.json
                    SampleDataSource.cs
                HubApp.Shared.projitems
                Strings
                    en-US
                        Resources.resw
            Assets
                HubBackground.theme-dark.png
                HubBackground.theme-light.png
                Logo.scale-240.png
                SmallLogo.scale-240.png
                SplashScreen.scale-240.png
                Square71x71Logo.scale-240.png
                StoreLogo.scale-240.png
                WideLogo.scale-240.png
            HubPage.xaml
                HubPage.xaml.cs
            ItemPage.xaml
                ItemPage.xaml.cs
            Package.appxmanifest
            Properties
                AssemblyInfo.cs
            References
                .NET for Windows Store apps
                HubApp.Shared
                Windows Phone 8.1
            SectionPage.xaml
                SectionPage.xaml.cs
    ```

### <a name="detect-changes-in-platform-projects-and-shared-projects"></a>检测平台项目和共享项目中的更改

1. 可以使用层次结构和项目事件来检测共享项目中的更改，就像对平台项目一样。 但是，共享项目中的项目项不可见，这意味着在更改共享项目项时不会执行某些事件。

    考虑重命名项目中的文件时的事件序列：

   1. 文件名在磁盘上更改。

   2. 项目文件将更新为包含文件的新名称。

      例如，层次结构 (，) 跟踪 UI 中显示的更改，如 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents> 解决方案资源管理器。  层次结构事件将文件重命名操作考虑为包含文件删除和添加文件。 但是，当更改不可见项时，层次结构事件系统将触发 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> 事件，而不是 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> 事件。 因此，如果重命名平台项目中的文件，则同时获得 和 ，但如果重命名共享项目中的文件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> ，则只会获得 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> 。

      若要跟踪项目项中的更改，可以处理 DTE 项目项 (在项目项 <xref:EnvDTE.ProjectItemsEventsClass>) 。 但是，如果要处理大量事件，可以更好地处理 中的事件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> 。 本演练只显示层次结构事件和 DTE 事件。 此过程将事件侦听器添加到共享项目和平台项目。 然后，重命名共享项目中的一个文件和平台项目中的另一个文件时，可以看到针对每个重命名操作触发的事件。

      此过程将事件侦听器添加到共享项目和平台项目。 然后，重命名共享项目中的一个文件和平台项目中的另一个文件时，可以看到针对每个重命名操作触发的事件。

2. 添加事件侦听器。 将新的类文件添加到项目，并调用它 *HierarchyEventListener.cs*。

3. 打开 *HierarchyEventListener.cs 文件* 并添加以下 using 指令：

   ```csharp
   using Microsoft.VisualStudio.Shell.Interop;
   using Microsoft.VisualStudio;
   using System.IO;
   ```

4. 使 `HierarchyEventListener` 类实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents> ：

   ```csharp
   class HierarchyEventListener : IVsHierarchyEvents
   { }
   ```

5. 实现 的成员 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents> ，如下面的代码所示。

   ```csharp
   class HierarchyEventListener : IVsHierarchyEvents
   {
       private IVsHierarchy hierarchy;
       IVsOutputWindowPane output;

       internal HierarchyEventListener(IVsHierarchy hierarchy, IVsOutputWindowPane outputWindow) {
            this.hierarchy = hierarchy;
            this.output = outputWindow;
       }

       int IVsHierarchyEvents.OnInvalidateIcon(IntPtr hIcon) {
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnInvalidateItems(uint itemIDParent) {
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnItemAdded(uint itemIDParent, uint itemIDSiblingPrev, uint itemIDAdded) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnItemAdded: " + itemIDAdded + "\n");
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnItemDeleted(uint itemID) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnItemDeleted: " + itemID + "\n");
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnItemsAppended(uint itemIDParent) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnItemsAppended\n");
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnPropertyChanged(uint itemID, int propID, uint flags) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnPropertyChanged: item ID " + itemID + "\n");
           return VSConstants.S_OK;
       }
   }
   ```

6. 在同一类中，为 DTE 事件 添加另一个事件处理程序 <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> ，每当重命名项目项时就会发生该事件处理程序。

   ```csharp
   public void OnItemRenamed(EnvDTE.ProjectItem projItem, string oldName)
   {
       output.OutputStringThreadSafe(string.Format("[Event] Renamed {0} to {1} in project {2}\n",
            oldName, Path.GetFileName(projItem.get_FileNames(1)), projItem.ContainingProject.Name));
   }
   ```

7. 注册层次结构事件。 需要为要跟踪的每个项目单独注册。 在 中添加以下 `ShowMessageBox` 代码，一个代码用于共享项目，另一个代码用于一个平台项目。

   ```csharp
   // hook up the event listener for hierarchy events on the shared project
   HierarchyEventListener listener1 = new HierarchyEventListener(sharedHier, output);
   uint cookie1;
   sharedHier.AdviseHierarchyEvents(listener1, out cookie1);

   // hook up the event listener for hierarchy events on the
   active project
   HierarchyEventListener listener2 = new HierarchyEventListener(activePlatformHier, output);
   uint cookie2;
   activePlatformHier.AdviseHierarchyEvents(listener2, out cookie2);
   ```

8. 注册 DTE 项目项事件 <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> 。 在挂钩第二个侦听器后添加以下代码。

   ```csharp
   // hook up DTE events for project items
   Events2 dteEvents = (Events2)dte.Events;
   dteEvents.ProjectItemsEvents.ItemRenamed += listener1.OnItemRenamed;
   ```

9. 修改共享项。 不能修改平台项目中的共享项;相反，必须在作为这些项的实际所有者的共享项目中修改它们。 可以使用 获取共享项目中的相应项 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A> ID，从而提供共享项的完整路径。 然后，可以修改共享项。 更改将传播到平台项目。

    > [!IMPORTANT]
    > 在修改项目项之前，应确定项目项是否是共享项。

     以下方法修改项目项文件的名称。

    ```csharp
    private void ModifyFileNameInProject(IVsHierarchy project, string path)
    {
        int found;
        uint projectItemID;
        VSDOCUMENTPRIORITY[] priority = new VSDOCUMENTPRIORITY[1];
        if (ErrorHandler.Succeeded(((IVsProject)project).IsDocumentInProject(path, out found, priority, out projectItemID))
            && found != 0)
        {
            var name = DateTime.Now.Ticks.ToString() + Path.GetExtension(path);
            project.SetProperty(projectItemID, (int)__VSHPROPID.VSHPROPID_EditLabel, name);
            output.OutputStringThreadSafe(string.Format("Renamed {0} to {1}\n", path,name));
        }
    }
    ```

10. 在 中的所有其他代码之后调用此方法 `ShowMessageBox` ，以修改共享项目中项的文件名。 在获取共享项目中项的完整路径的代码后插入此项。

    ```csharp
    // change the file name of an item in a shared project
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));
    output.OutputStringThreadSafe(string.Format("Shared project item ID = {0}, full path = {1}\n", sharedItemId, fullPath));
    this.ModifyFileNameInProject(sharedHier, fullPath);
    ```

11. 生成并运行该项目。 在实验实例中创建 C# 通用中心应用，转到"工具"菜单，单击"**调用 TestUniversalProject"，** 并检查常规输出窗格中的文本。 共享项目中第一 (项的名称，我们希望它是 *App.xaml* 文件) 应更改，并且应看到事件 <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> 已触发。 在这种情况下，由于 *重命名 App.xaml* 也会导致 *App.xaml.cs* 重命名，因此应该会看到每个平台项目 (两个事件) 。  (DTE 事件不跟踪共享项目中的项。) 应该会看到两个事件 (一个事件用于每个平台项目) ，但没有 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> 事件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> 。

12. 现在尝试重命名平台项目中的文件，可以看到触发的事件的差异。 在调用 后， `ShowMessageBox` 在 中添加以下代码 `ModifyFileName` 。

    ```csharp
    // change the file name of an item in a platform project
    var unsharedItemIds = new List<uint>();
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, unsharedItemIds, false, false);

    var unsharedItemId = unsharedItemIds[0];
    string unsharedPath;
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(unsharedItemId, out unsharedPath));
    output.OutputStringThreadSafe(string.Format("Platform project item ID = {0}, full path = {1}\n", unsharedItemId, unsharedPath));

    this.ModifyFileNameInProject(activePlatformHier, unsharedPath);
    ```

13. 生成并运行该项目。 在实验实例Project C# 通用数据库，转到"工具"菜单，单击"调用 **TestUniversalProject"，** 并检查常规输出窗格中的文本。 重命名平台项目中的文件后，应会看到 事件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> 事件。 由于更改文件导致其他文件不会更改，并且由于平台项目中的项更改不会传播到任何位置，因此只有其中一个事件。