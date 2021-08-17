---
title: 管理通用 Windows 项目 |Microsoft Docs
description: 若要支持通用 Windows 应用，管理项目 Visual Studio 扩展应了解通用 Windows 应用项目结构。
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
ms.openlocfilehash: 08c44675c2fcae1035f292a4b2247aef7aad285633b24c28fa2375ef14e4e1de
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401071"
---
# <a name="manage-universal-windows-projects"></a>管理通用 Windows 项目

通用 Windows 应用是面向 Windows 8.1 和 Windows Phone 8.1 的应用，允许开发人员在这两个平台上使用代码和其他资产。 共享代码和资源保留在共享项目中，而特定于平台的代码和资源保留在单独的项目中，一个用于 Windows，另一个用于 Windows Phone。 有关通用 Windows 应用的详细信息，请参阅[通用 Windows 应用](/windows/uwp/get-started/create-uwp-apps)。 管理项目 Visual Studio 扩展应该知道，通用 Windows 应用项目的结构不同于单平台应用。 本演练演示如何导航共享项目并管理共享项。

## <a name="prerequisites"></a>先决条件

从 Visual Studio 2015 开始，你不会从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 也可稍后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

### <a name="navigate-the-shared-project"></a>导航共享项目

1. 创建一个名为 **TestUniversalProject** 的 c # VSIX 项目。  (**文件**  >  **新**  >  **Project** ，然后是 **c #**  >  **扩展**  >  **Visual Studio 包**) 。 添加 **自定义命令** 项目项模板 (在 **解决方案资源管理器** 上，右键单击项目节点并选择 "**添加**  >  **新项**"，然后中转到 "**扩展性**) "。 将该文件命名为 **TestUniversalProject**。

2. 在) 的 "**扩展**" 部分中添加对 *Microsoft.VisualStudio.Shell.Interop.12.1.DesignTime.dll* 和 *Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll* (的引用。

3. 打开 *TestUniversalProject* ，添加以下 `using` 指令：

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

4. 在类中， `TestUniversalProject` 添加指向 " **输出** " 窗口的私有字段。

    ```csharp
    public sealed class TestUniversalProject
    {
        IVsOutputWindowPane output;
    . . .
    }
    ```

5. 将引用设置为 TestUniversalProject 构造函数中的 "输出" 窗格：

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

6. 从方法中删除现有代码 `ShowMessageBox` ：

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
    }
    ```

7. 获取 DTE 对象，在本演练中，我们将使用这些对象进行多种不同的目的。 此外，请确保在单击菜单按钮时加载解决方案。

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

8. 查找共享项目。 共享项目是一个纯容器;它不生成或生成输出。 下面的方法通过查找 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 具有共享项目功能的对象查找解决方案中的第一个共享项目。

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

9. 在 `ShowMessageBox` 方法中，将标题输出 (在共享项目的 **解决方案资源管理器**) 中显示的项目名称。

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

10. 获取活动平台项目。 平台项目是包含特定于平台的代码和资源的项目。 下面的方法使用新的字段 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy> 获取活动平台项目。

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

12. 遍历平台项目。 以下方法获取共享项目中的所有导入 (平台) 项目。

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
    > 如果用户已在实验实例中打开 c + + 通用 Windows 应用项目，则上述代码将引发异常。 这是一个已知问题。 若要避免此异常，请将 `foreach` 上面的块替换为以下内容：

    ```csharp
    var importingProjects = sharedAssetsProject.EnumImportingProjects();
    for (int i = 0; i < importingProjects.Count; ++i)
    {
        yield return importingProjects[i];
    }
    ```

13. 在 `ShowMessageBox` 方法中，输出每个平台项目的标题。 在输出活动平台项目标题的行的后面插入以下代码。 此列表中仅显示已加载的平台项目。

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

14. 更改 "活动平台" 项目。 下面的方法使用设置活动项目 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A> 。

    ```csharp
    private int SetActiveProjectContext(IVsHierarchy hierarchy, IVsHierarchy activeProjectContext)
    {
        return hierarchy.SetProperty((uint)VSConstants.VSITEMID.Root, (int)__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy, activeProjectContext);
    }
    ```

15. 在 `ShowMessageBox` 方法中，更改 "活动平台" 项目。 将此代码插入到 `foreach` 块中。

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

16. 现在试试看。按 F5 启动实验实例。 在实验实例中创建一个 c # 通用中心应用项目 (在 "**新建 Project** " 对话框的 " **Visual c #**"  >  **Windows**  >  **Windows 8**  >  **通用**  >  **集线器应用**) "。 加载解决方案后，请切换到 " **工具** " 菜单，单击 " **调用 TestUniversalProject**"，然后在 " **输出** " 窗格中查看文本。 会看到下面这样的内容：

    ```
    Found shared project: HubApp.Shared
    The active platform project: HubApp.Windows
    Platform projects:
     * HubApp.Windows
     * HubApp.WindowsPhone
    set active project: HubApp.WindowsPhone
    ```

### <a name="manage-the-shared-items-in-the-platform-project"></a>管理平台项目中的共享项

1. 在平台项目中查找共享项。 共享项目中的项在平台项目中显示为共享项。 你无法在 **解决方案资源管理器** 中查看它们，但你可以浏览项目层次结构来查找它们。 下面的方法遍历层次结构并收集所有共享项。 它还可以输出每个项的标题。 共享项由新的属性标识 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7.VSHPROPID_IsSharedItem> 。

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

2. 在 `ShowMessageBox` 方法中，添加以下代码来演练平台项目层次结构项。 将其插入到 `foreach` 块中。

    ```csharp
    output.OutputStringThreadSafe("Walk the active platform project:\n");
    var sharedItemIds = new List<uint>();
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);
    ```

3. 读取共享项。 共享项作为隐藏链接文件显示在平台项目中，您可以将所有属性作为普通链接文件读取。 下面的代码读取第一个共享项的完整路径。

    ```csharp
    var sharedItemId = sharedItemIds[0];
    string fullPath;
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));
    output.OutputStringThreadSafe(string.Format("Shared item full path: {0}\n", fullPath));
    ```

4. 现在试试看。按 **F5** 启动实验实例。 在实验实例中创建一个 c # 通用中心应用项目 (在 **"新建 Project** " 对话框中的 " **Visual c #**"  >  **Windows**  >  **Windows 8**  >  **通用**  >  **集线器应用**) 中转到 "**工具**" 菜单，单击 "**调用 TestUniversalProject**"，然后在 "**输出**" 窗格中检查文本。 会看到下面这样的内容：

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

1. 您可以使用层次结构和项目事件来检测共享项目中的更改，就像对平台项目一样。 但是，共享项目中的项目项是不可见的，这意味着在更改共享项目项时，某些事件不会激发。

    重命名项目中的文件时，请考虑事件的顺序：

   1. 在磁盘上更改文件名。

   2. 项目文件将更新为包含文件的新名称。

       (的层次结构事件例如， <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents>) 通常跟踪 UI 中显示的更改，如 **解决方案资源管理器** 中所示。 层次结构事件将文件重命名操作视为包含文件删除和文件添加操作。 但是，当不可见项发生更改时，层次结构事件系统将引发一个 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> 事件，但不会引发 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> 事件。 因此，如果重命名平台项目中的文件，则会同时获取 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> ，但如果重命名共享项目中的文件，则只会获得 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> 。

      若要跟踪项目项中的更改，你可以处理 DTE 项目项事件 (在) 中找到的事件 <xref:EnvDTE.ProjectItemsEventsClass> 。 但是，如果要处理大量事件，可以在中更好地处理事件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> 。 在本演练中，我们只显示层次结构事件和 DTE 事件。 在此过程中，您将向共享项目和平台项目中添加一个事件侦听器。 然后，当你重命名共享项目中的一个文件和平台项目中的另一个文件时，可以查看为每个重命名操作触发的事件。

      在此过程中，您将向共享项目和平台项目中添加一个事件侦听器。 然后，当你重命名共享项目中的一个文件和平台项目中的另一个文件时，可以查看为每个重命名操作触发的事件。

2. 添加事件侦听器。 向项目中添加一个新的类文件，并将其称为 " *HierarchyEventListener*"。

3. 打开 *HierarchyEventListener* 文件并添加以下 using 指令：

   ```csharp
   using Microsoft.VisualStudio.Shell.Interop;
   using Microsoft.VisualStudio;
   using System.IO;
   ```

4. 让 `HierarchyEventListener` 类实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents> ：

   ```csharp
   class HierarchyEventListener : IVsHierarchyEvents
   { }
   ```

5. 实现的成员 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents> ，如下面的代码所示。

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

6. 在同一个类中，为 DTE 事件添加另一个事件处理程序 <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> ，每当重命名项目项时，就会发生这种情况。

   ```csharp
   public void OnItemRenamed(EnvDTE.ProjectItem projItem, string oldName)
   {
       output.OutputStringThreadSafe(string.Format("[Event] Renamed {0} to {1} in project {2}\n",
            oldName, Path.GetFileName(projItem.get_FileNames(1)), projItem.ContainingProject.Name));
   }
   ```

7. 注册层次结构事件。 需要为要跟踪的每个项目单独进行注册。 在中添加以下代码 `ShowMessageBox` ，一个用于共享项目，另一个用于平台项目。

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

8. 注册 DTE 项目项事件 <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> 。 在挂钩第二个侦听器后，添加以下代码。

   ```csharp
   // hook up DTE events for project items
   Events2 dteEvents = (Events2)dte.Events;
   dteEvents.ProjectItemsEvents.ItemRenamed += listener1.OnItemRenamed;
   ```

9. 修改共享项。 不能修改平台项目中的共享项;相反，你必须在作为这些项的实际所有者的共享项目中对其进行修改。 您可以在共享项目中获取相应的项 ID，并为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A> 其提供共享项的完整路径。 然后，可以修改共享项。 更改将传播到平台项目。

    > [!IMPORTANT]
    > 在修改项目项之前，应查明项目项是否为共享项。

     下面的方法修改项目项文件的名称。

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

10. 在中的所有其他代码之后调用此方法 `ShowMessageBox` ，以修改共享项目中的项的文件名。 在获取共享项目中项的完整路径的代码后插入此项。

    ```csharp
    // change the file name of an item in a shared project
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));
    output.OutputStringThreadSafe(string.Format("Shared project item ID = {0}, full path = {1}\n", sharedItemId, fullPath));
    this.ModifyFileNameInProject(sharedHier, fullPath);
    ```

11. 生成并运行该项目。 在实验实例中创建 C# 通用中心应用，转到"工具"菜单，单击"**调用 TestUniversalProject"，** 并检查常规输出窗格中的文本。 共享项目中第一项的名称 (我们预计它是 *App.xaml* 文件) 应更改，并且应看到事件 <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> 已触发。 在这种情况下，由于重命名 *App.xaml* 也会导致 *App.xaml.cs* 重命名，因此应该会看到每个平台项目 (两个事件) 。  (DTE 事件不跟踪共享项目中的项。) 应该会看到两个事件 (一个事件用于每个平台项目) ，但没有事件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> 。

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