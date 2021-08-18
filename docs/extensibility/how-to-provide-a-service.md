---
title: 如何：提供服务|Microsoft Docs
description: VSPackage 可以提供其他 VSPackage 可以使用的服务。 了解 VSPackage 如何将服务注册到 Visual Studio并添加该服务。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- services, providing
ms.assetid: 12bc1f12-47b1-44f6-b8db-862aa88d50d1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 11205634b75c3ae1892e7a4d964ae049ec50afbd
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122050294"
---
# <a name="how-to-provide-a-service"></a>如何：提供服务
VSPackage 可以提供其他 VSPackage 可以使用的服务。 若要提供服务，VSPackage 必须将服务注册到 Visual Studio并添加该服务。

 <xref:Microsoft.VisualStudio.Shell.Package>类实现 和 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> <xref:System.ComponentModel.Design.IServiceContainer> 。 <xref:System.ComponentModel.Design.IServiceContainer> 包含按需提供服务的回调方法。

 有关服务详细信息，请参阅 [服务基本信息](../extensibility/internals/service-essentials.md) 。

> [!NOTE]
> 当 VSPackage 即将卸载时，Visual Studio等待，直到传递了对 VSPackage 提供的服务的所有请求。 它不允许对这些服务进行新的请求。 卸载时，不应显式调用 方法来 <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.RevokeService%2A> 撤销服务。

## <a name="implement-a-service"></a>实现服务

1. 使用 Visual C# 扩展性 VSIX (**Visual** C# 扩展性 Project 创建  >    >    >    >    >  **VSIX 项目Project) 。**

2. 将 VSPackage 添加到项目。 选择项目中的项目节点解决方案资源管理器"添加新项  >    >  **""Visual C#** 项扩展性Visual Studio  >    >  **包"。**

3. 若要实现服务，需要创建三种类型：

   - 描述服务的接口。 其中许多接口为空，即它们没有方法。

   - 描述服务接口的接口。 此接口包括要实现的方法。

   - 同时实现服务和服务接口的类。

     下面的示例演示三种类型的基本实现。 服务类的构造函数必须设置服务提供程序。

   ```csharp
   public class MyService : SMyService, IMyService
   {
       private Microsoft.VisualStudio.OLE.Interop.IServiceProvider serviceProvider;
       private string myString;
       public MyService(Microsoft.VisualStudio.OLE.Interop.IServiceProvider sp)
       {
           Trace.WriteLine(
                  "Constructing a new instance of MyService");
           serviceProvider = sp;
       }
       public void Hello()
       {
           myString = "hello";
       }
       public string Goodbye()
       {
          return "goodbye";
       }
   }
   public interface SMyService
   {
   }
   public interface IMyService
   {
       void Hello();
       string Goodbye();
   }

   ```

### <a name="register-a-service"></a>注册服务

1. 若要注册服务，请 <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> 向提供服务的 VSPackage 添加 。 以下是示例：

    ```csharp
    [ProvideService(typeof(SMyService))]
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [Guid(VSPackage1.PackageGuidString)]
    public sealed class VSPackage1 : Package
    {. . . }
    ```

     此属性注册到 `SMyService` Visual Studio。

    > [!NOTE]
    > 若要注册将另一个服务替换为同名的服务，请使用 <xref:Microsoft.VisualStudio.Shell.ProvideServiceOverrideAttribute> 。 请注意，只允许一个服务的重写。

### <a name="add-a-service"></a>添加服务

1. 在 VSPackage 初始值设置项中，添加服务并添加回调方法以创建服务。 下面是对 方法的 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 更改：

    ```csharp
    protected override void Initialize()
    {
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);

        ((IServiceContainer)this).AddService(typeof(SMyService), callback);
    . . .
    }
    ```

2. 实现回调方法，该方法应创建并返回服务;如果无法创建，则返回 null。

    ```csharp
    private object CreateService(IServiceContainer container, Type serviceType)
    {
        if (typeof(SMyService) == serviceType)
            return new MyService(this);
        return null;
    }
    ```

    > [!NOTE]
    > Visual Studio拒绝提供服务的请求。 如果另一个 VSPackage 已提供服务，则它会这样做。

3. 现在，可以获取服务并使用其方法。 下面的示例演示如何在初始值设置项中使用该服务，但可以在想要使用该服务的任何位置获取该服务。

    ```csharp
    protected override void Initialize()
    {
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);

        ((IServiceContainer)this).AddService(typeof(SMyService), callback);

        MyService myService = (MyService) this.GetService(typeof(SMyService));
        myService.Hello();
        string helloString = myService.Goodbye();

        base.Initialize();
    }
    ```

     的值 `helloString` 应为"Hello"。

## <a name="see-also"></a>请参阅
- [如何：获取服务](../extensibility/how-to-get-a-service.md)
- [使用和提供服务](../extensibility/using-and-providing-services.md)
- [服务要素](../extensibility/internals/service-essentials.md)
