---
title: 将你的应用与填充码隔离（单元测试）
description: 了解如何使用填充码类型将对特定方法的调用转换为在测试中编写的部分代码。 填充码可以在每次调用时返回一致的结果。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
author: mikejo5000
dev_langs:
- CSharp
- VB
ms.openlocfilehash: 9c8e941a024162e35ec6a5067078a07d4d1c4fae
ms.sourcegitcommit: fc874be3fe4637a23997b4ef2d99a2ee9a499581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2021
ms.locfileid: "135516759"
---
# <a name="use-shims-to-isolate-your-app-for-unit-testing"></a>使用填充码隔离应用以进行单元测试

填充码类型是 Microsoft Fakes 框架使用的两种技术之一，可用于将受测组件与环境隔离开来  。 填充码会将对特定方法的调用转换为在测试中编写的部分代码。 很多方法会依赖于外部条件而返回不同的结果，但填充码处于测试的控制之下，并且可以在每次调用时返回一致的结果。 这样可以更轻松地编写测试。

使用填充码，可以将代码与不属于解决方案的程序集隔离  。 为了相互隔离解决方案的组件，请使用存根  。

有关概述和“快速入门”指南，请参阅[使用 Microsoft Fakes 隔离受测代码](../test/isolating-code-under-test-with-microsoft-fakes.md)。

**惠?**

- Visual Studio Enterprise
- .NET Framework 项目
::: moniker range=">=vs-2019"
- .net Core、.net 5.0 或更高版本，以及 SDK 样式项目支持 Visual Studio 2019 更新6中预览，并在 update 8 中默认启用。 有关详细信息，请参阅[适用于 .NET Core 和 SDK 样式项目的 Microsoft Fakes](/visualstudio/releases/2019/release-notes#microsoft-fakes-for-net-core-and-sdk-style-projects)。
::: moniker-end

## <a name="example-the-y2k-bug"></a>示例: 计算机 2000 年问题 Bug

设想一种会在 2000 年 1 月 1 日引发异常的方法：

```csharp
// code under test
public static class Y2KChecker {
    public static void Check() {
        if (DateTime.Now == new DateTime(2000, 1, 1))
            throw new ApplicationException("y2kbug!");
    }
}
```

测试此方法会出现问题，因为程序依赖于 `DateTime.Now`，这是一种依赖于计算机时钟的方法、一种依赖于环境的非确定性方法。 此外，`DateTime.Now` 为静态属性，因此无法在此处使用存根类型。 此问题是单元测试中隔离问题的症状：直接调用数据库 API、与 Web 服务通信等的程序很难进行单元测试，因为它们的逻辑依赖于环境。

这种情况下应该使用填充码类型。 填充码类型提供了一种机制，可以使任何 .NET 方法绕道至用户定义的委托。 Fakes 类型是由 Fakes 生成器生成的代码，它们使用委托（我们称为填充码类型）来指定新的方法实现。

下面的代码演示如何使用填充码类型 `ShimDateTime` 来提供 DateTime.Now 的自定义实现：

```csharp
//unit test code
// create a ShimsContext cleans up shims
using (ShimsContext.Create()) {
    // hook delegate to the shim method to redirect DateTime.Now
    // to return January 1st of 2000
    ShimDateTime.NowGet = () => new DateTime(2000, 1, 1);
    Y2KChecker.Check();
}
```

## <a name="how-to-use-shims"></a>如何使用填充码

首先，添加 Fakes 程序集：

1. 在“解决方案资源管理器”中： 
    - 对于旧版 .NET Framework 项目（非 SDK 样式），展开单元测试项目的“引用”节点。
    ::: moniker range=">=vs-2019"
    - 对于面向 .NET Framework、.net Core 或 .net 5.0 或更高版本的 SDK 样式项目，请展开 "**依赖项**" 节点，以查找要在 **程序集**、**项目** 或 **包** 下伪造的程序集。
    ::: moniker-end
    - 如果使用的是 Visual Basic，请选择“解决方案资源管理器”工具栏中的“显示所有文件”，以查看“引用”节点。

2. 选择包含要为其创建填充码的类定义的程序集。 例如，如果要填充 DateTime，请选择 System.dll   。

3. 选择快捷菜单中的“添加 Fakes 程序集”  。

### <a name="use-shimscontext"></a>使用 ShimsContext

当在单元测试框架中使用填充码类型时，将测试代码包装在 `ShimsContext` 中，以便控制填充码的生存期。 否则，填充码将一直持续到 AppDomain 关闭。 最简单的方法是使用静态 `ShimsContext` 方法创建一个 `Create()`，如下面的代码中所示：

```csharp
//unit test code
[Test]
public void Y2kCheckerTest() {
  using(ShimsContext.Create()) {
    ...
  } // clear all shims
}
```

正确释放每个填充码上下文至关重要。 根据经验，请调用 `using` 语句内的 `ShimsContext.Create`，以便确保清除已注册的填充码。 例如，您可能为某一测试方法注册了填充码，而且该方法会将 `DateTime.Now` 方法替换为始终返回 2000 年 1 月 1 日的委托。 如果忘记清除测试方法中的已注册填充码，则剩余的测试运行将始终返回 2000 年 1 月 1 日作为 `DateTime.Now` 值。 这可能会让人感到惊讶和困惑。

### <a name="write-a-test-with-shims"></a>编写包含填充码的测试

在测试代码中，为要虚设的方法插入 *绕道*。 例如:

```csharp
[TestClass]
public class TestClass1
{
        [TestMethod]
        public void TestCurrentYear()
        {
            int fixedYear = 2000;

            using (ShimsContext.Create())
            {
              // Arrange:
                // Detour DateTime.Now to return a fixed date:
                System.Fakes.ShimDateTime.NowGet =
                () =>
                { return new DateTime(fixedYear, 1, 1); };

                // Instantiate the component under test:
                var componentUnderTest = new MyComponent();

              // Act:
                int year = componentUnderTest.GetTheCurrentYear();

              // Assert:
                // This will always be true if the component is working:
                Assert.AreEqual(fixedYear, year);
            }
        }
}
```

```vb
<TestClass()> _
Public Class TestClass1
    <TestMethod()> _
    Public Sub TestCurrentYear()
        Using s = Microsoft.QualityTools.Testing.Fakes.ShimsContext.Create()
            Dim fixedYear As Integer = 2000
            ' Arrange:
            ' Detour DateTime.Now to return a fixed date:
            System.Fakes.ShimDateTime.NowGet = _
                Function() As DateTime
                    Return New DateTime(fixedYear, 1, 1)
                End Function

            ' Instantiate the component under test:
            Dim componentUnderTest = New MyComponent()
            ' Act:
            Dim year As Integer = componentUnderTest.GetTheCurrentYear
            ' Assert:
            ' This will always be true if the component is working:
            Assert.AreEqual(fixedYear, year)
        End Using
    End Sub
End Class
```

填充码类名称是通过在原始类型名称前加上 `Fakes.Shim` 前缀构成的。

填充码的运行方式为在受测应用的代码中插入 *绕道*。 无论在什么位置调用原始方法，Fakes 系统都会执行绕道，这样就会调用填充码代码而不是实际方法。

请注意，绕道是在运行时创建和删除的。 必须始终在 `ShimsContext` 生存期内创建绕道。 释放绕道后，在绕道活动期间创建的任何填充码都会被移除。 为此，最好的方法是在 `using` 语句内执行。

您可能会看到一个说明 Fakes 命名空间不存在的生成错误。 此错误有时会在发生其他编译错误时出现。 修复其他错误，然后它就会消失。

## <a name="shims-for-different-kinds-of-methods"></a>用于不同方法类型的存根

使用填充码方法，您可以将任何 .NET 方法（包括静态方法或非虚拟方法）替换为自己的委托。

### <a name="static-methods"></a>静态方法

用于将填充码附加到静态方法的属性将放置在填充码类型中。 每个属性只有一个资源库，可用来将委托附加到目标方法。 例如，给定一个具有静态方法 `MyClass` 的类 `MyMethod`：

```csharp
//code under test
public static class MyClass {
    public static int MyMethod() {
        ...
    }
}
```

我们可以将填充码附加到始终返回 5 的 `MyMethod`：

```csharp
// unit test code
ShimMyClass.MyMethod = () => 5;
```

### <a name="instance-methods-for-all-instances"></a>实例方法（对于所有实例）

与静态方法类似，可以为所有实例填充实例方法。 为了避免混淆，用于附加这些填充码的属性放置在名为 AllInstances 的嵌套类型中。 例如，给定一个具有静态方法 `MyClass` 的类 `MyMethod`：

```csharp
// code under test
public class MyClass {
    public int MyMethod() {
        ...
    }
}
```

无论任何实例，您都可以将一个填充码附加到始终返回 5 的 `MyMethod`：

```csharp
// unit test code
ShimMyClass.AllInstances.MyMethod = () => 5;
```

所生成的 ShimMyClass 类型结构类似于以下代码：

```csharp
// Fakes generated code
public class ShimMyClass : ShimBase<MyClass> {
    public static class AllInstances {
        public static Func<MyClass, int>MyMethod {
            set {
                ...
            }
        }
    }
}
```

请注意，在此示例中，Fakes 会将运行时实例作为委托的第一个自变量传递。

### <a name="instance-methods-for-one-runtime-instance"></a>实例方法（对于一个运行时实例）

根据调用的接收方，也可以通过不同的委托来填充实例方法。 这样一来，同一实例方法可以根据类型实例而具有不同的行为。 用于设置这些填充码的属性是填充码类型本身的实例方法。 每个实例化的填充码类型也会与一个所填充类型的原始实例相关联。

例如，给定一个具有静态方法 `MyClass` 的类 `MyMethod`：

```csharp
// code under test
public class MyClass {
    public int MyMethod() {
        ...
    }
}
```

我们可以设置两种填充码类型的 MyMethod，以便第一个始终返回 5，而第二个始终返回 10：

```csharp
// unit test code
var myClass1 = new ShimMyClass()
{
    MyMethod = () => 5
};
var myClass2 = new ShimMyClass { MyMethod = () => 10 };
```

所生成的 ShimMyClass 类型结构类似于以下代码：

```csharp
// Fakes generated code
public class ShimMyClass : ShimBase<MyClass> {
    public Func<int> MyMethod {
        set {
            ...
        }
    }
    public MyClass Instance {
        get {
            ...
        }
    }
}
```

实际填充的类型实例可通过 Instance 属性来访问：

```csharp
// unit test code
var shim = new ShimMyClass();
var instance = shim.Instance;
```

填充码类型还具有到所填充类型的隐式转换，因此您通常可以原样使用填充码类型：

```csharp
// unit test code
var shim = new ShimMyClass();
MyClass instance = shim; // implicit cast retrieves the runtime instance
```

### <a name="constructors"></a>构造函数

构造函数也可以进行填充，以便将填充码类型附加到未来的对象。 在填充码类型中，每个构造函数都作为静态方法构造函数而公开。 例如，给定一个使用整数的构造函数的类 `MyClass`：

```csharp
// code under test
public class MyClass {
    public MyClass(int value) {
        this.Value = value;
    }
    ...
}
```

我们设置构造函数的填充码类型，以便在调用值 getter 时，使每个未来实例都返回 -5，而无论构造函数中的值是什么：

```csharp
// unit test code
ShimMyClass.ConstructorInt32 = (@this, value) => {
    var shim = new ShimMyClass(@this) {
        ValueGet = () => -5
    };
};
```

每个填充码类型都会公开两个构造函数。 当需要新实例时，应使用默认构造函数，而以填充的实例为参数的构造函数只应在构造函数填充码中使用：

```csharp
// unit test code
public ShimMyClass() { }
public ShimMyClass(MyClass instance) : base(instance) { }
```

所生成的 ShimMyClass 类型结构类似于以下代码：

```csharp
// Fakes generated code
public class ShimMyClass : ShimBase<MyClass>
{
    public static Action<MyClass, int> ConstructorInt32 {
        set {
            ...
        }
    }

    public ShimMyClass() { }
    public ShimMyClass(MyClass instance) : base(instance) { }
    ...
}
```

### <a name="base-members"></a>基成员

基成员的填充码属性可以通过以下方式来访问：为基类型创建填充码，并将子实例作为参数传递给基填充码类的构造函数。

例如，给定一个具有实例方法 `MyBase` 和子类型 `MyMethod` 的类 `MyChild`：

```csharp
public abstract class MyBase {
    public int MyMethod() {
        ...
    }
}

public class MyChild : MyBase {
}
```

我们可以通过创建新的 `MyBase` 填充码来设置 `ShimMyBase` 的填充码：

```csharp
// unit test code
var child = new ShimMyChild();
new ShimMyBase(child) { MyMethod = () => 5 };
```

请注意，当作为参数传递给基填充码构造函数时，子填充码类型将隐式转换为子实例。

所生成的 ShimMyChild 和 ShimMyBase 类型结构类似于以下代码：

```csharp
// Fakes generated code
public class ShimMyChild : ShimBase<MyChild> {
    public ShimMyChild() { }
    public ShimMyChild(Child child)
        : base(child) { }
}
public class ShimMyBase : ShimBase<MyBase> {
    public ShimMyBase(Base target) { }
    public Func<int> MyMethod
    { set { ... } }
}
```

### <a name="static-constructors"></a>静态构造函数

填充码类型会公开静态方法 `StaticConstructor`，以便填充类型的静态构造函数。 由于静态构造函数仅执行一次，因此，在访问任何类型成员之前，你需要确保配置填充码。

### <a name="finalizers"></a>终结器

Fakes 中不支持终结器。

### <a name="private-methods"></a>私有方法

Fakes 代码生成器会为仅具有签名中的可见类型的私有方法创建填充码属性，即可见的参数类型和返回类型。

### <a name="binding-interfaces"></a>绑定接口

当填充的类型实现某一接口时，代码生成器将发出一个方法，以便它同时绑定该接口的所有成员。

例如，给定一个实现 `MyClass` 的类 `IEnumerable<int>`：

```csharp
public class MyClass : IEnumerable<int> {
    public IEnumerator<int> GetEnumerator() {
        ...
    }
    ...
}
```

通过调用 Bind 方法，可以填充 MyClass 中的 `IEnumerable<int>` 实现：

```csharp
// unit test code
var shimMyClass = new ShimMyClass();
shimMyClass.Bind(new List<int> { 1, 2, 3 });
```

所生成的 ShimMyClass 类型结构类似于以下代码：

```csharp
// Fakes generated code
public class ShimMyClass : ShimBase<MyClass> {
    public ShimMyClass Bind(IEnumerable<int> target) {
        ...
    }
}
```

## <a name="change-the-default-behavior"></a>更改默认行为

每个生成的填充码类型都保留 `IShimBehavior` 接口的一个实例（通过 `ShimBase<T>.InstanceBehavior` 属性）。 只要客户端调用未显式填充的实例成员，系统就会使用该行为。

如果未显式设置该行为，它会使用静态 `ShimBehaviors.Current` 属性返回的实例。 默认情况下，此属性将返回引发 `NotImplementedException` 异常的行为。

通过设置任何填充码实例的 `InstanceBehavior` 属性，可以随时更改该行为。 例如，下面的代码片段将更改填充码的行为，使之不执行任何操作或返回返回类型的默认值，即 `default(T)`：

```csharp
// unit test code
var shim = new ShimMyClass();
//return default(T) or do nothing
shim.InstanceBehavior = ShimBehaviors.DefaultValue;
```

通过设置静态 `InstanceBehavior` 属性，还可以为所有未设置 `ShimBehaviors.Current` 属性的填充实例全局更改此行为：

```csharp
// unit test code
// change default shim for all shim instances
// where the behavior has not been set
ShimBehaviors.Current = ShimBehaviors.DefaultValue;
```

## <a name="detect-environment-accesses"></a>检测环境访问权限

通过将 `ShimBehaviors.NotImplemented` 行为分配给相应填充码类型的静态属性 `Behavior`，可以将行为附加到特定类型的所有成员（包括静态方法）：

```csharp
// unit test code
// assigning the not implemented behavior
ShimMyClass.Behavior = ShimBehaviors.NotImplemented;
// shorthand
ShimMyClass.BehaveAsNotImplemented();
```

## <a name="concurrency"></a>并发

填充码类型适用于 AppDomain 中的所有线程，且不具备线程关联性。 如果计划使用支持并发的测试运行程序，这是需要注意的重点。 涉及填充码类型的测试不能同时运行。 此属性不由 Fakes 运行时来实施。

## <a name="call-the-original-method-from-the-shim-method"></a>通过填充码方法调用原始方法

假设想要在验证文件名已传递给方法之后，再将文本写到文件系统。 这种情况下，需要调用填充码方法中的原始方法。

要解决这一问题，第一种方法是使用委托和 `ShimsContext.ExecuteWithoutShims()` 来包装对原始方法的调用，如下面的代码中所示：

```csharp
// unit test code
ShimFile.WriteAllTextStringString = (fileName, content) => {
  ShimsContext.ExecuteWithoutShims(() => {

      Console.WriteLine("enter");
      File.WriteAllText(fileName, content);
      Console.WriteLine("leave");
  });
};
```

另一种方法是将填充码设置为 NULL，再调用原始方法，然后恢复填充码。

```csharp
// unit test code
ShimsDelegates.Action<string, string> shim = null;
shim = (fileName, content) => {
  try {
    Console.WriteLine("enter");
    // remove shim in order to call original method
    ShimFile.WriteAllTextStringString = null;
    File.WriteAllText(fileName, content);
  }
  finally
  {
    // restore shim
    ShimFile.WriteAllTextStringString = shim;
    Console.WriteLine("leave");
  }
};
// initialize the shim
ShimFile.WriteAllTextStringString = shim;
```

## <a name="systemenvironment"></a>System.Environment

若要填充 <xref:System.Environment?displayProperty=fullName>，请将以下内容添加到“程序集”元素后面的 mscorlib.fakes 文件中  ：

```xml
<ShimGeneration>
    <Add FullName="System.Environment"/>
</ShimGeneration>
```

重新生成解决方案后，可对 <xref:System.Environment?displayProperty=fullName> 类中的方法和属性进行填充，例如：

```csharp
System.Fakes.ShimEnvironment.GetCommandLineArgsGet = ...
```

## <a name="limitations"></a>限制

无法在 .NET Framework 中的 .net 基类库 **mscorlib** 和 **system** 中的所有类型上使用填充码，而在 .net Core 或 .net 5.0 和更高版本中，则不能用于 **system.web** 。

## <a name="see-also"></a>另请参阅

- [通过 Microsoft Fakes 隔离受测代码](../test/isolating-code-under-test-with-microsoft-fakes.md)
- [Peter Provost 的博客：Visual Studio 2012 填充码](http://www.peterprovost.org/blog/2012/04/25/visual-studio-11-fakes-part-2)