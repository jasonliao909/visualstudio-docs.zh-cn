---
title: 添加语言服务器协议扩展 |Microsoft Docs
description: 了解如何创建基于语言服务器协议 (LSP) 的 Visual Studio 扩展。
ms.custom: SEO-VS-2020
ms.date: 07/05/2021
ms.topic: conceptual
ms.assetid: 52f12785-1c51-4c2c-8228-c8e10316cd83
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 9daeb0358c1dfe638cf3ca49ad973ffd6dc19cc0
ms.sourcegitcommit: 42aec4a2ea6dec67dbe4c93bcf0fa1116a4b93d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2021
ms.locfileid: "122980782"
---
# <a name="add-a-language-server-protocol-extension"></a>添加语言服务器协议扩展

语言服务器协议 (LSP) 是一个采用 JSON RPC v2.0 格式的通用协议，用于向各种代码编辑器提供语言服务功能。 使用该协议，开发人员可以编写单一的语言服务器来向支持 LSP 的各种代码编辑器提供 IntelliSense、错误诊断、查找所有引用等语言服务功能。 传统上，可以使用 TextMate 语法文件添加 Visual Studio 中的语言服务，以提供基本功能，如语法突出显示或编写自定义语言服务（使用整套 Visual Studio 扩展性 api 提供更丰富的数据）。 对于 LSP Visual Studio 支持，还有第三个选项。

![Visual Studio 中的语言服务器协议服务](media/lsp-service-in-VS.png)

## <a name="language-server-protocol"></a>语言服务器协议

![语言服务器协议实现](media/lsp-implementation.png)

本文介绍如何创建使用基于 LSP 的语言服务器的 Visual Studio 扩展。 它假定您已经开发了基于 LSP 的语言服务器，并且只想将其集成到 Visual Studio 中。

为了 Visual Studio 中的支持，语言服务器可通过任何基于流的传输机制与客户端 (Visual Studio) 进行通信，例如：

* 标准输入/输出流
* Named pipes
* 套接字 (仅限 TCP) 

在 Visual Studio 中，LSP 和对其的支持是指不是 Visual Studio 产品一部分的内置语言服务。 这并不是为了在 Visual Studio (如 c # ) 扩展现有语言服务。 若要扩展现有语言，请参阅语言服务的扩展性指南 (例如， ["Roslyn" .NET Compiler Platform](../extensibility/dotnet-compiler-platform-roslyn-extensibility.md)) 或参阅[扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)。

有关协议本身的详细信息，请参阅 [此处](https://github.com/Microsoft/language-server-protocol)的文档。

若要详细了解如何创建示例语言服务器或者如何将现有语言服务器集成到 Visual Studio Code 中，请参阅[此处](https://code.visualstudio.com/docs/extensions/example-language-server)的文档。

## <a name="language-server-protocol-supported-features"></a>语言服务器协议支持的功能

下表显示 Visual Studio 支持的 LSP 功能：

消息 | 支持 Visual Studio
--- | ---
初始化 | 是
已初始化 | 是
shutdown | 是
exit | 是
$/cancelRequest | 是
窗口/showMessage | 是
窗口/showMessageRequest | 是
窗口/logMessage | 是
遥测/事件 |
客户端/registerCapability |
客户端/unregisterCapability |
workspace/didChangeConfiguration | 是
workspace/didChangeWatchedFiles | 是
工作区/符号 | 是
workspace/executeCommand | 是
workspace/applyEdit | 是
textDocument/publishDiagnostics | 是
textDocument/didOpen | 是
textDocument/didChange | 是
textDocument/willSave |
textDocument/willSaveWaitUntil |
textDocument/didSave | 是
textDocument/didClose | 是
textDocument/完成 | 是
完成/解决 | 是
textDocument/悬停 | 是
textDocument/signatureHelp | 是
textDocument/引用 | 是
textDocument/documentHighlight | 是
textDocument/documentSymbol | 是
textDocument/格式 | 是
textDocument/rangeFormatting | 是
textDocument/onTypeFormatting |
textDocument/definition | 是
textDocument/codeAction | 是
textDocument/codeLens |
codeLens/解析 |
textDocument/documentLink |
documentLink/resolve |
textDocument/rename | 是

## <a name="get-started"></a>入门

> [!NOTE]
> 从 Visual Studio 2017 版15.8 开始，Visual Studio 中内置了对公共语言服务器协议的支持。 如果使用预览版 [语言服务器客户端 VSIX](https://marketplace.visualstudio.com/items?itemName=vsext.LanguageServerClientPreview) 版本生成了 LSP 扩展，则在升级到版本15.8 或更高版本后，它们将停止运行。 你将需要执行以下操作，以使 LSP 扩展再次工作：
>
> 1. 卸载 Microsoft Visual Studio 语言服务器协议预览 VSIX。
>
>    从版本 15.8 开始，每次在 Visual Studio升级时，都会自动检测并删除预览版 VSIX。
>
> 2. 将 Nuget 引用更新为 LSP 包 的最新非 [预览版本](https://www.nuget.org/packages/Microsoft.VisualStudio.LanguageServer.Client)。
>
> 3. 删除 VSIX 清单中Microsoft Visual Studio语言服务器协议预览 VSIX 的依赖项。
>
> 4. 确保 VSIX 将 2017 Visual Studio 15.8 预览版 3 指定为安装目标的下限。
>
> 5. 重新生成并重新部署。

### <a name="create-a-vsix-project"></a>创建 VSIX 项目

若要使用基于 LSP 的语言服务器创建语言服务扩展，首先请确保为 VS 实例Visual Studio扩展开发工作负荷。

接下来，通过导航到"文件""新建"Project   >    >  **Visual C#**  >  **扩展**  >  **性 VSIX** Project：

![创建 vsix 项目](media/lsp-vsix-project.png)

### <a name="language-server-and-runtime-installation"></a>语言服务器和运行时安装

默认情况下，为支持 Visual Studio基于 LSP 的语言服务器而创建的扩展不包含语言服务器本身或执行这些服务器所需的运行时。 扩展开发人员负责分发语言服务器和所需的运行时。 有几种方法可以这样做：

* 语言服务器可以嵌入 VSIX 中作为内容文件。
* 创建 MSI 以安装语言服务器和/或所需的运行时。
* 提供有关市场的说明，告知用户如何获取运行时和语言服务器。

### <a name="textmate-grammar-files"></a>TextMate 语法文件

LSP 不包括如何为语言提供文本着色的规范。 若要为中语言提供自定义着色Visual Studio，扩展开发人员可以使用 TextMate 语法文件。 若要添加自定义 TextMate 语法或主题文件，请执行以下步骤：

1. 在扩展插件内创建一个名为"Grammars"的文件夹 (该文件夹可以是你选择的任何) 。

2. 在 *Grammars* 文件夹中，包括任何需要提供自定义着色的 *.tmlanguage、.plist、.tmtheme \** 或 *\***\* .json* 文件。 *\**

   > [!TIP]
   > *.tmtheme* 文件定义范围如何映射到Visual Studio命名颜色 (键的) 。 有关指导，可以在 *%ProgramFiles (x86) %\Microsoft Visual Studio \\ \<version> \\ \<SKU> \Common7\IDE\CommonExtensions\Microsoft\TextMate\Starterkit\Themesg* 目录中引用全局 *.tmtheme* 文件。

3. 创建 *.pkgdef* 文件并添加类似于以下的行：

    ```
    [$RootKey$\TextMate\Repositories]
    "MyLang"="$PackageFolder$\Grammars"
    ```

4. 右键单击文件，然后选择"属性 **"。** 将"**生成"** 操作 **更改为"内容**"，将 **"在 VSIX 中包括"属性** 更改为 **true。**

完成前面的步骤后，将 *Grammars* 文件夹添加到包的安装目录中，因为名为"MyLang" ("MyLang"的存储库源只是一个名称，用于解除二元性，可以是任何唯一的字符串) 。 此目录中的所有语法 (*.tmlanguage* 文件) 和主题文件 (*.tmtheme* 文件) 都选作潜在语法，并取代 TextMate 提供的内置语法。 如果语法文件的已声明扩展名与正在打开的文件的扩展名匹配，TextMate 将进入。

## <a name="create-a-simple-language-client"></a>创建简单的语言客户端

### <a name="main-interface---ilanguageclient"></a>主接口 - [ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017&preserve-view=true)

创建 VSIX 项目后，将以下NuGet包 () 添加到项目中：

* [Microsoft.VisualStudio.LanguageServer.Client](https://www.nuget.org/packages/Microsoft.VisualStudio.LanguageServer.Client)

> [!NOTE]
> 完成上述步骤后，对 NuGet 包执行依赖项时，Newtonsoft.Json 和 StreamJsonRpc 包也添加到项目中。 **除非确定这些新版本** 将安装在扩展面向 的 Visual Studio版本上，否则不要更新这些包。 这些程序集不会包含在 VSIX 中;而是从安装目录中Visual Studio它们。 如果引用的程序集版本比用户计算机上安装的版本更新，则扩展将不起作用。

然后，可以创建一个实现 [ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017&preserve-view=true) 接口的新类，该接口是连接到基于 LSP 的语言服务器的语言客户端所需的主接口。

下面是一个示例：

```csharp
namespace MockLanguageExtension
{
    [ContentType("bar")]
    [Export(typeof(ILanguageClient))]
    public class BarLanguageClient : ILanguageClient
    {
        public string Name => "Bar Language Extension";

        public IEnumerable<string> ConfigurationSections => null;

        public object InitializationOptions => null;

        public IEnumerable<string> FilesToWatch => null;

        public event AsyncEventHandler<EventArgs> StartAsync;
        public event AsyncEventHandler<EventArgs> StopAsync;

        public async Task<Connection> ActivateAsync(CancellationToken token)
        {
            await Task.Yield();

            ProcessStartInfo info = new ProcessStartInfo();
            info.FileName = Path.Combine(Path.GetDirectoryName(Assembly.GetExecutingAssembly().Location), "Server", @"MockLanguageServer.exe");
            info.Arguments = "bar";
            info.RedirectStandardInput = true;
            info.RedirectStandardOutput = true;
            info.UseShellExecute = false;
            info.CreateNoWindow = true;

            Process process = new Process();
            process.StartInfo = info;

            if (process.Start())
            {
                return new Connection(process.StandardOutput.BaseStream, process.StandardInput.BaseStream);
            }

            return null;
        }

        public async Task OnLoadedAsync()
        {
            await StartAsync.InvokeAsync(this, EventArgs.Empty);
        }

        public Task OnServerInitializeFailedAsync(Exception e)
        {
            return Task.CompletedTask;
        }

        public Task OnServerInitializedAsync()
        {
            return Task.CompletedTask;
        }
    }
}
```

需要实现的主要方法是 [OnLoadedAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.onloadedasync?view=visualstudiosdk-2017&preserve-view=true) 和 [ActivateAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.activateasync?view=visualstudiosdk-2017&preserve-view=true)。 当已加载扩展Visual Studio语言服务器已准备好启动时，将调用[OnLoadedAsync。](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.onloadedasync?view=visualstudiosdk-2017&preserve-view=true) 在此方法中，可以立即调用[StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017&preserve-view=true)委托来指示应启动语言服务器，也可以执行其他逻辑，并稍后调用[StartAsync。](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017&preserve-view=true) **若要激活语言服务器，必须在某些时候调用 StartAsync。**

[ActivateAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.activateasync?view=visualstudiosdk-2017&preserve-view=true) 是最终通过调用 [StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017&preserve-view=true) 委托调用的方法。 它包含启动语言服务器并建立与它的连接的逻辑。 必须返回一个连接对象，该对象包含用于写入服务器和从服务器进行读取的流。 此处引发的任何异常都通过消息中的 InfoBar 消息捕获并显示给用户Visual Studio。

### <a name="activation"></a>激活

实现语言客户端类后，需要为它定义两个属性，以定义如何将它加载到Visual Studio激活：

```csharp
  [Export(typeof(ILanguageClient))]
  [ContentType("bar")]
```

### <a name="mef"></a>MEF

Visual Studio [MEF (Managed Extensibility Framework) ](https://github.com/Microsoft/vs-mef/blob/master/doc/index.md)管理其扩展性点。 Export [](/dotnet/api/system.componentmodel.composition.exportattribute)属性指示Visual Studio此类应作为扩展点选取并在适当时间加载。

若要使用 MEF，还必须在 VSIX 清单中将 MEF 定义为资产。

打开 VSIX 清单设计器并导航到"资产 **"** 选项卡：

![添加 MEF 资产](media/lsp-add-asset.png)

单击 **"新建** "以创建新资产：

![定义 MEF 资产](media/lsp-define-asset.png)

* **类型**：Microsoft.VisualStudio.MefComponent
* **源**：当前解决方案中的项目
* **Project**：[你的项目]

### <a name="content-type-definition"></a>内容类型定义

目前，加载基于 LSP 的语言服务器扩展插件的唯一方法就是按文件内容类型。 也就是说，在定义实现 [ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017&preserve-view=true)) 的语言客户端类 (时，需要定义打开时会导致加载扩展的文件类型。 如果未打开任何与定义的内容类型匹配的文件，将不会加载扩展名。

这通过定义一个或多个类 `ContentTypeDefinition` 完成：

```csharp
namespace MockLanguageExtension
{
    public class BarContentDefinition
    {
        [Export]
        [Name("bar")]
        [BaseDefinition(CodeRemoteContentDefinition.CodeRemoteContentTypeName)]
        internal static ContentTypeDefinition BarContentTypeDefinition;

        [Export]
        [FileExtension(".bar")]
        [ContentType("bar")]
        internal static FileExtensionToContentTypeDefinition BarFileExtensionDefinition;
    }
}
```

在上一示例中，为以 *.bar* 文件扩展名结尾的文件创建内容类型定义。 内容类型定义的名称为"bar"，必须派生自 [CodeRemoteContentTypeName](/dotnet/api/microsoft.visualstudio.languageserver.client.coderemotecontentdefinition.coderemotecontenttypename?view=visualstudiosdk-2017&preserve-view=true)。

添加内容类型定义后，可以定义何时在语言客户端类中加载语言客户端扩展：

```csharp
    [ContentType("bar")]
    [Export(typeof(ILanguageClient))]
    public class BarLanguageClient : ILanguageClient
    {
    }
```

添加对 LSP 语言服务器的支持时，无需在 Visual Studio 中实现自己的项目系统。 客户可以在 Visual Studio中打开单个文件或文件夹，以开始使用语言服务。 事实上，对 LSP 语言服务器的支持仅适用于打开的文件夹/文件方案。 如果实现了自定义项目系统， (某些功能（例如) 设置）将不起作用。

## <a name="advanced-features"></a>高级功能

### <a name="settings"></a>设置

提供对特定于自定义语言服务器的设置的支持，但它仍在改进中。 设置特定于语言服务器支持哪些内容，并且通常控制语言服务器如何发出数据。 例如，语言服务器可能有针对报告的最大错误数的设置。 扩展作者将定义一个默认值，用户可以为特定项目更改该值。

按照以下步骤将设置支持添加到 LSP 语言服务扩展：

1. 添加 JSON 文件 (例如，MockLanguageExtensionSettings.js上) 包含设置及其默认值的项目。 例如：

    ```json
    {
        "foo.maxNumberOfProblems": -1
    }
    ```

2. 右键单击 JSON 文件，然后选择"属性 **"。** 将"**生成"** 操作更改为"内容"，将"在 VSIX 中包括"属性更改为 **true。**

3. 实现 ConfigurationSections 并返回 JSON 文件 (In Visual Studio Code 中定义的设置的前缀列表，这会映射到) 上 package.js中的配置节) ：

    ```csharp
    public IEnumerable<string> ConfigurationSections
    {
        get
        {
            yield return "foo";
        }
    }
    ```

4. 将 .pkgdef 文件添加到项目 (添加新文本文件，将文件扩展名更改为 .pkgdef) 。 pkgdef 文件应包含此信息：

    ```
    [$RootKey$\OpenFolder\Settings\VSWorkspaceSettings\[settings-name]]
    @="$PackageFolder$\[settings-file-name].json"
    ```

    示例：

    ```
    [$RootKey$\OpenFolder\Settings\VSWorkspaceSettings\MockLanguageExtension]
    @="$PackageFolder$\MockLanguageExtensionSettings.json"
    ```

5. 右键单击 .pkgdef 文件，然后选择"属性 **"。** 将"**生成"** 操作 **更改为"内容**"，将 **"在 VSIX 中包括"属性** 更改为 **true。**

6. 打开 *source.extension.vsixmanifest* 文件，在"资产"选项卡 **中添加** 资产：

   ![编辑 vspackage 资产](media/lsp-add-vspackage-asset.png)

   * **类型**：Microsoft.VisualStudio.VsPackage
   * **源**：文件系统上的文件
   * **路径**：[.pkgdef *文件* 的路径]

### <a name="user-editing-of-settings-for-a-workspace&quot;></a>用户编辑工作区的设置

1. 用户打开一个工作区，其中包含服务器拥有的文件。
2. 用户在 上的 *.vs* 文件夹中添加名为 *VSWorkspaceSettings.js文件*。
3. 用户向服务器提供的设置 *VSWorkspaceSettings.json* 文件添加一行。 例如：

    ```json
    {
        &quot;foo.maxNumberOfProblems&quot;: 10
    }
    ```

### <a name=&quot;enable-diagnostics-tracing&quot;></a>启用诊断跟踪

可以启用诊断跟踪来输出客户端和服务器之间的所有消息，这在调试问题时非常有用。 若要启用诊断跟踪，请执行以下操作：

1. 打开或创建 (*VSWorkspaceSettings.js上* 的工作区设置文件，请参阅 &quot;用户编辑工作区的设置" ) 。
2. 在设置 json 文件中添加以下行：

```json
{
    "foo.trace.server": "Off"
}
```

跟踪详细级别有三个可能的值：

* "关闭"：完全关闭跟踪
* "消息"：启用跟踪，但只跟踪方法名称和响应 ID。
* "详细"：启用跟踪;跟踪整个 rpc 消息。

当启用跟踪时，会将内容写入 *%temp%\VisualStudio\LSP* 目录中的文件。 日志采用命名格式 *[LanguageClientName]-[Datetime 戳记] .log*。 目前，只能对打开的文件夹方案启用跟踪。 打开单个文件以激活语言服务器没有诊断跟踪支持。

### <a name="custom-messages"></a>自定义消息

::: moniker range="vs-2017"

存在一些 Api，可帮助将消息传递到不属于标准语言服务器协议的语言服务器并从其接收消息。 若要处理自定义消息，请在语言客户端类中实现 [ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017&preserve-view=true) 接口。 [VS-StreamJsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md) 库用于在语言客户端和语言服务器之间传输自定义消息。 由于你的 lsp 语言客户端扩展与任何其他 Visual Studio 扩展一样，你可以决定添加 LSP) 不支持的附加功能 (通过自定义消息 Visual Studio (使用其他 Visual Studio api。

#### <a name="receive-custom-messages"></a>接收自定义消息

若要从语言服务器接收自定义消息，请在[ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017&preserve-view=true)上实现[CustomMessageTarget](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.custommessagetarget?view=visualstudiosdk-2017&preserve-view=true)属性，并返回一个知道如何处理自定义消息的对象。 示例如下：

```csharp
internal class MockCustomLanguageClient : MockLanguageClient, ILanguageClientCustomMessage
{
    private JsonRpc customMessageRpc;

    public MockCustomLanguageClient() : base()
    {
        CustomMessageTarget = new CustomTarget();
    }

    public object CustomMessageTarget
    {
        get;
        set;
    }

    public class CustomTarget
    {
        public void OnCustomNotification(JToken arg)
        {
            // Provide logic on what happens OnCustomNotification is called from the language server
        }

        public string OnCustomRequest(string test)
        {
            // Provide logic on what happens OnCustomRequest is called from the language server
        }
    }
}
```

#### <a name="send-custom-messages"></a>发送自定义消息

若要将自定义消息发送到语言服务器，请在[ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017&preserve-view=true)上实现[AttachForCustomMessageAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.attachforcustommessageasync?view=visualstudiosdk-2017&preserve-view=true)方法。 当您的语言服务器启动并准备好接收消息时，将调用此方法。 [JsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/src/StreamJsonRpc/JsonRpc.cs)对象作为参数传递，你随后可以使用[VS-StreamJsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md) api 将消息发送到语言服务器。 示例如下：

```csharp
internal class MockCustomLanguageClient : MockLanguageClient, ILanguageClientCustomMessage
{
    private JsonRpc customMessageRpc;

    public MockCustomLanguageClient() : base()
    {
        CustomMessageTarget = new CustomTarget();
    }

    public async Task AttachForCustomMessageAsync(JsonRpc rpc)
    {
        await Task.Yield();

        this.customMessageRpc = rpc;
    }

    public async Task SendServerCustomNotification(object arg)
    {
        await this.customMessageRpc.NotifyWithParameterObjectAsync("OnCustomNotification", arg);
    }

    public async Task<string> SendServerCustomMessage(string test)
    {
        return await this.customMessageRpc.InvokeAsync<string>("OnCustomRequest", test);
    }
}
```

### <a name="middle-layer"></a>中间层

有时，扩展开发人员可能需要拦截发送到语言服务器并从语言服务器接收的 LSP 消息。 例如，扩展开发人员可能需要更改为特定 LSP 消息发送的消息参数，或修改从语言服务器返回的结果以获得 LSP 功能 (例如) 完成。 如果需要，扩展开发人员可以使用 MiddleLayer API 来拦截 LSP 消息。

每个 LSP 消息都有自己的用于侦听的中间层接口。 若要截获特定消息，请创建一个实现该消息的中间层接口的类。 然后，在语言客户端类中实现 [ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017&preserve-view=true) 接口，并在 [MiddleLayer](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.middlelayer?view=visualstudiosdk-2017&preserve-view=true) 属性中返回对象的实例。 示例如下：

```csharp
public class MockLanguageClient: ILanguageClient, ILanguageClientCustomMessage
{
    public object MiddleLayer => MiddleLayerProvider.Instance;

    private class MiddleLayerProvider : ILanguageClientWorkspaceSymbolProvider
    {
        internal readonly static MiddleLayerProvider Instance = new MiddleLayerProvider();

        private MiddleLayerProvider()
        {
        }

        public async Task<SymbolInformation[]> RequestWorkspaceSymbols(WorkspaceSymbolParams param, Func<WorkspaceSymbolParams, Task<SymbolInformation[]>> sendRequest)
        {
            // Send along the request as given
            SymbolInformation[] symbols = await sendRequest(param);

            // Only return symbols that are "files"
            return symbols.Where(sym => string.Equals(new Uri(sym.Location.Uri).Scheme, "file", StringComparison.OrdinalIgnoreCase)).ToArray();
        }
    }
}
```

::: moniker-end

::: moniker range="vs-2019"

存在一些 Api，可帮助将消息传递到不属于标准语言服务器协议的语言服务器并从其接收消息。 若要处理自定义消息，请在语言客户端类中实现 [ILanguageClientCustomMessage2](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage2) 接口。 [VS-StreamJsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md) 库用于在语言客户端和语言服务器之间传输自定义消息。 由于你的 lsp 语言客户端扩展与任何其他 Visual Studio 扩展一样，你可以决定添加 LSP) 不支持的附加功能 (通过自定义消息 Visual Studio (使用其他 Visual Studio api。

#### <a name="receive-custom-messages"></a>接收自定义消息

若要从语言服务器接收自定义消息，请在 [ILanguageClientCustomMessage2](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage2) 上实现 [CustomMessageTarget] ( (/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.custommessagetarget) 属性，并返回一个知道如何处理自定义消息的对象。 示例如下：

 ([ILanguageClientCustomMessage2](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage2) 上的/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.custommessagetarget) 属性并返回知道如何处理自定义消息的对象。 示例如下：

```csharp
internal class MockCustomLanguageClient : MockLanguageClient, ILanguageClientCustomMessage2
{
    private JsonRpc customMessageRpc;

    public MockCustomLanguageClient() : base()
    {
        CustomMessageTarget = new CustomTarget();
    }

    public object CustomMessageTarget
    {
        get;
        set;
    }

    public class CustomTarget
    {
        public void OnCustomNotification(JToken arg)
        {
            // Provide logic on what happens OnCustomNotification is called from the language server
        }

        public string OnCustomRequest(string test)
        {
            // Provide logic on what happens OnCustomRequest is called from the language server
        }
    }
}
```

#### <a name="send-custom-messages"></a>发送自定义消息

若要将自定义消息发送到语言服务器，请在[ILanguageClientCustomMessage2](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage2)上实现[AttachForCustomMessageAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage2.attachforcustommessageasync)方法。 当您的语言服务器启动并准备好接收消息时，将调用此方法。 [JsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/src/StreamJsonRpc/JsonRpc.cs)对象作为参数传递，你随后可以使用[VS-StreamJsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md) api 将消息发送到语言服务器。 示例如下：

```csharp
internal class MockCustomLanguageClient : MockLanguageClient, ILanguageClientCustomMessage2
{
    private JsonRpc customMessageRpc;

    public MockCustomLanguageClient() : base()
    {
        CustomMessageTarget = new CustomTarget();
    }

    public async Task AttachForCustomMessageAsync(JsonRpc rpc)
    {
        await Task.Yield();

        this.customMessageRpc = rpc;
    }

    public async Task SendServerCustomNotification(object arg)
    {
        await this.customMessageRpc.NotifyWithParameterObjectAsync("OnCustomNotification", arg);
    }

    public async Task<string> SendServerCustomMessage(string test)
    {
        return await this.customMessageRpc.InvokeAsync<string>("OnCustomRequest", test);
    }
}
```

### <a name="middle-layer"></a>中间层

有时，扩展开发人员可能需要拦截发送到语言服务器并从语言服务器接收的 LSP 消息。 例如，扩展开发人员可能需要更改为特定 LSP 消息发送的消息参数，或修改从语言服务器返回的结果以获得 LSP 功能 (例如) 完成。 如果需要，扩展开发人员可以使用 MiddleLayer API 来拦截 LSP 消息。

若要截获特定消息，请创建一个实现 [ILanguageClientMiddleLayer](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientmiddlelayer) 接口的类。 然后，在语言客户端类中实现 [ILanguageClientCustomMessage2](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage2) 接口，并在 [MiddleLayer](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage2.middlelayer) 属性中返回对象的实例。 示例如下：

```csharp
public class MockLanguageClient : ILanguageClient, ILanguageClientCustomMessage2
{
  public object MiddleLayer => DiagnosticsFilterMiddleLayer.Instance;

  private class DiagnosticsFilterMiddleLayer : ILanguageClientMiddleLayer
  {
    internal readonly static DiagnosticsFilterMiddleLayer Instance = new DiagnosticsFilterMiddleLayer();

    private DiagnosticsFilterMiddleLayer() { }

    public bool CanHandle(string methodName)
    {
      return methodName == "textDocument/publishDiagnostics";
    }

    public async Task HandleNotificationAsync(string methodName, JToken methodParam, Func<JToken, Task> sendNotification)
    {
      if (methodName == "textDocument/publishDiagnostics")
      {
        var diagnosticsToFilter = (JArray)methodParam["diagnostics"];
        // ony show diagnostics of severity 1 (error)
        methodParam["diagnostics"] = new JArray(diagnosticsToFilter.Where(diagnostic => diagnostic.Value<int?>("severity") == 1));

      }
      await sendNotification(methodParam);
    }

    public async Task<JToken> HandleRequestAsync(string methodName, JToken methodParam, Func<JToken, Task<JToken>> sendRequest)
    {
      return await sendRequest(methodParam);
    }
  }
}
```

::: moniker-end

中间层功能仍处于开发阶段，但并不全面。

## <a name="sample-lsp-language-server-extension"></a>示例 LSP 语言服务器扩展

若要在 Visual Studio 中使用 LSP 客户端 API 查看示例扩展的源代码，请参阅 VSSDK 的可扩展性[示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/LanguageServerProtocol)。

## <a name="faq"></a>常见问题解答

**我要构建一个自定义项目系统来补充我的 LSP 语言服务器，以在 Visual Studio 中提供更丰富的功能支持，如何实现此目的？**

对 Visual Studio 中基于 LSP 的语言服务器的支持依赖于 "[打开文件夹" 功能](https://devblogs.microsoft.com/visualstudio/open-any-folder-with-visual-studio-15-preview/)，并且设计为不需要自定义项目系统。 您可以按照 [此处](https://github.com/Microsoft/VSProjectSystem)的说明生成您自己的自定义项目系统，但某些功能（如设置）可能不起作用。 LSP 语言服务器的默认初始化逻辑是传递当前正在打开的文件夹的根文件夹位置，因此，如果使用自定义项目系统，则可能需要在初始化期间提供自定义逻辑，以确保语言服务器可以正常启动。

**如何实现添加调试器支持？**

在将来的版本中，我们将为 [通用调试协议](https://code.visualstudio.com/docs/extensionAPI/api-debugging) 提供支持。

**如果已安装了 VS 支持的语言服务 (例如，JavaScript) ，我是否仍然可以安装可提供附加功能 (如 linting) 的 LSP 语言服务器扩展？**

是的，但并非所有功能都能正常工作。 LSP 语言服务器扩展的最终目标是启用 Visual Studio 不本机支持的语言服务。 你可以使用 LSP 语言服务器创建提供附加支持的扩展，但某些功能 (例如 IntelliSense) 不会是一种流畅的体验。 通常，建议使用 LSP 语言服务器扩展来提供新的语言体验，而不是扩展现有的语言。

**在何处发布已完成的 LSP 语言服务器 VSIX？**

请参阅 [此处](walkthrough-publishing-a-visual-studio-extension.md)的 Marketplace 说明。

## <a name="see-also"></a>请参阅

- [为其他语言添加 Visual Studio 编辑器支持](../ide/adding-visual-studio-editor-support-for-other-languages.md)
