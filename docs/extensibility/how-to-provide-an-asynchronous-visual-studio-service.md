---
title: 如何：提供异步Visual Studio服务|Microsoft Docs
description: 了解如何提供异步Visual Studio服务。 此方法允许你在不阻止 UI 线程的情况下获取服务。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 0448274c-d3d2-4e12-9d11-8aca78a1f3f5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 41777f9b04060928799c621de8262d50d027014aaa4a2831ad0a6656bfa0b9c1
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401708"
---
# <a name="how-to-provide-an-asynchronous-visual-studio-service"></a>如何：提供异步Visual Studio服务
如果要在不阻止 UI 线程的情况下获取服务，应创建异步服务，并在后台线程上加载包。 为此，可以使用 而不是 ，并使用异步包的特殊异步方法 <xref:Microsoft.VisualStudio.Shell.AsyncPackage> <xref:Microsoft.VisualStudio.Shell.Package> 添加服务。

 有关提供同步服务Visual Studio，请参阅[如何：提供服务](../extensibility/how-to-provide-a-service.md)。

## <a name="implement-an-asynchronous-service"></a>实现异步服务

1. 使用 Visual C# 扩展性 VSIX (**文件** 新建Project  >    >    >    >    >  **VSIX 项目Project) 。** 将项目名称 **为 TestAsync**。

2. 将 VSPackage 添加到项目。 选择项目中的项目节点解决方案资源管理器"添加新项  >    >  **""Visual C#** 项扩展性Visual Studio  >    >  **包"。** 将此文件命名 *TestAsyncPackage.cs*。

3. 在 *TestAsyncPackage.cs 中*，将包更改为继承自 `AsyncPackage` 而不是 `Package` ：

    ```csharp
    public sealed class TestAsyncPackage : AsyncPackage
    ```

4. 若要实现服务，需要创建三种类型：

    - 标识服务的接口。 其中许多接口为空，也就是说，它们没有方法，因为它们仅用于查询服务。

    - 描述服务接口的接口。 此接口包括要实现的方法。

    - 同时实现服务和服务接口的类。

5. 下面的示例演示这三种类型的非常基本的实现。 服务类的构造函数必须设置服务提供程序。 本示例仅将服务添加到包代码文件。

6. 将以下 using 指令添加到包文件：

    ```csharp
    using System.Threading;
    using System.Threading.Tasks;
    using System.Runtime.CompilerServices;
    using System.IO;
    using Microsoft.VisualStudio.Threading;
    using IAsyncServiceProvider = Microsoft.VisualStudio.Shell.IAsyncServiceProvider;
    using Task = System.Threading.Tasks.Task;
    ```

7. 下面是异步服务实现。 请注意，需要在构造函数中设置异步服务提供程序，而不是同步服务提供程序：

    ```csharp
    public class TextWriterService : STextWriterService, ITextWriterService
    {
        private IAsyncServiceProvider asyncServiceProvider;

        public TextWriterService(IAsyncServiceProvider provider)
        {
            // constructor should only be used for simple initialization
            // any usage of Visual Studio service, expensive background operations should happen in the
            // asynchronous InitializeAsync method for best performance
            asyncServiceProvider = provider;
        }

        public async Task InitializeAsync(CancellationToken cancellationToken)
        {
            await TaskScheduler.Default;
            // do background operations that involve IO or other async methods

            await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync(cancellationToken);
            // query Visual Studio services on main thread unless they are documented as free threaded explicitly.
            // The reason for this is the final cast to service interface (such as IVsShell) may involve COM operations to add/release references.

            IVsShell vsShell = this.asyncServiceProvider.GetServiceAsync(typeof(SVsShell)) as IVsShell;
            // use Visual Studio services to continue initialization
        }

        public async Task WriteLineAsync(string path, string line)
        {
            StreamWriter writer = new StreamWriter(path);
            await writer.WriteLineAsync(line);
            writer.Close();
        }
    }

    public interface STextWriterService
    {
    }

    public interface ITextWriterService
    {
        System.Threading.Tasks.Task WriteLineAsync(string path, string line);
    }
    ```

## <a name="register-a-service"></a>注册服务
 若要注册服务，请 <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> 向提供服务的包添加 。 与注册同步服务不同，必须确保包和服务都支持异步加载：

- 必须将 **"AllowsBackgroundLoading = true"** 字段添加到 以确保可以异步初始化包。有关 <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> PackageRegistrationAttribute 详细信息，请参阅注册和注销 [VSPackage。](../extensibility/registering-and-unregistering-vspackages.md)

- 必须将 **IsAsyncQueryable = true** 字段添加到 ， <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> 以确保可以异步初始化服务实例。

  下面是具有异步 `AsyncPackage` 服务注册的 的示例：

```csharp
[ProvideService((typeof(STextWriterService)), IsAsyncQueryable = true)]
[ProvideAutoLoad(UIContextGuids80.SolutionExists, PackageAutoLoadFlags.BackgroundLoad)]
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]
[Guid(TestAsyncPackage.PackageGuidString)]
public sealed class TestAsyncPackage : AsyncPackage
{. . . }
```

## <a name="add-a-service"></a>添加服务

1. 在 *TestAsyncPackage.cs 中*，删除 `Initialize()` 方法并重写 `InitializeAsync()` 方法。 添加服务，并添加回调方法以创建服务。 下面是添加服务的异步初始化程序的示例：

    ```csharp
    protected override async Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);
    }

    ```
    若要使此服务在此包外部可见，将提升标志值设置为 *true* 作为最后一个参数：  `this.AddService(typeof(STextWriterService), CreateTextWriterService, true);`

2. 添加对 *Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll* 的引用。

3. 将回调方法实现为创建和返回服务的异步方法。

    ```csharp
    public async Task<object> CreateTextWriterService(IAsyncServiceContainer container, CancellationToken cancellationToken, Type serviceType)
    {
        TextWriterService service = new TextWriterService(this);
        await service.InitializeAsync(cancellationToken);
        return service;
    }

    ```

## <a name="use-a-service"></a>使用服务
 现在，可以获取服务并使用其方法。

1. 我们将在初始值设置项中显示此内容，但可以在想要使用该服务的任何位置获取服务。

    ```csharp
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);

        ITextWriterService textService = await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;
        string userpath = @"C:\MyDir\MyFile.txt";
        await textService.WriteLineAsync(userpath, "this is a test");
    }

    ```

     不要忘记更改计算机上有意义的文件名 `userpath` 和路径！

2. 生成并运行代码。 当实验性实例Visual Studio，打开解决方案。 这将导致 自动 `AsyncPackage` 加载。 初始值设置项运行后，应找到指定位置中的文件。

## <a name="use-an-asynchronous-service-in-a-command-handler"></a>在命令处理程序中使用异步服务
 以下示例演示了如何在菜单命令中使用异步服务。 可以使用此处显示的过程在其他非异步方法中使用该服务。

1. 向项目添加菜单命令。  (在 解决方案资源管理器中，选择项目节点，右键单击，然后选择"添加新项扩展性自定义命令 .) 将命令文件命名  >    >    >  *TestAsyncCommand.cs"。*

2. 自定义命令模板将 方法重新添加到 `Initialize()` *TestAsyncPackage.cs* 文件中，以便初始化该命令。 在 `Initialize()` 方法中，复制初始化命令的行。 它应如下所示：

    ```csharp
    TestAsyncCommand.Initialize(this);
    ```

     移动此项 `InitializeAsync()` *AsyncPackageForService.cs* 文件中的方法。 由于这位于异步初始化中，因此在使用 初始化命令之前，必须切换到主线程 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> 。 它现在应如下所示：

    ```csharp

    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);

        ITextWriterService textService =
           await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;
        
        string userpath = @"C:\MyDir\MyFile.txt";
        await textService.WriteLineAsync(userpath, "this is a test");

        await this.JoinableTaskFactory.SwitchToMainThreadAsync(cancellationToken);
        TestAsyncCommand.Initialize(this);
    }

    ```

3. 删除 `Initialize()` 方法。

4. 在 *TestAsyncCommand.cs* 文件中，找到 `MenuItemCallback()` 方法。 删除方法的正文。

5. 添加 using 指令：

    ```csharp
    using System.IO;
    ```

6. 添加名为 的异步 `UseTextWriterAsync()` 方法，该方法获取服务并使用其方法：

    ```csharp
    private async System.Threading.Tasks.Task UseTextWriterAsync()
    {
        // Query text writer service asynchronously to avoid a blocking call.
        ITextWriterService textService =
           await AsyncServiceProvider.GlobalProvider.GetServiceAsync(typeof(STextWriterService))
              as ITextWriterService;

        string userpath = @"C:\MyDir\MyFile.txt";
        await textService.WriteLineAsync(userpath, "this is a test");
       }

    ```

7. 从 方法调用 `MenuItemCallback()` 此方法：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        UseTextWriterAsync();
    }

    ```

8. 生成解决方案并启动调试。 当实验实例出现Visual Studio，转到"工具 **"菜单并** 查找"**调用 TestAsyncCommand"** 菜单项。 单击它时，TextWriterService 将写入指定的文件。  (不需要打开解决方案，因为调用 命令也会导致包加载。) 

## <a name="see-also"></a>请参阅
- [使用和提供服务](../extensibility/using-and-providing-services.md)
