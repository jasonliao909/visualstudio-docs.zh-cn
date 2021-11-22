---
title: 使用 ClickOnce 部署 COM 组件 | Microsoft Docs
description: 了解在包含旧版 COM 组件的 ClickOnce 中部署 .NET 应用程序所需的步骤。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- registration-free COM deployment
- ClickOnce deployment, COM components
- COM components, deploying
- deploying applications [ClickOnce], COM components
- components, deploying
ms.assetid: 1a4c7f4c-7a41-45f2-9af4-8b1666469b89
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 68f62aab190686dbed88628b18e0b1ad0f89a723
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665638"
---
# <a name="deploy-com-components-with-clickonce"></a>使用 ClickOnce 部署 COM 组件
就传统意义而言，部署旧版 COM 组件是一项困难的任务。 组件需要全局注册，因此可能会导致重叠应用程序之间产生不良副作用。 这种情况通常不是 .NET Framework 应用程序的问题，因为组件与应用程序完全隔离或并行兼容。 借助 Visual Studio，你可以在 Windows XP 或更高版本的操作系统上部署独立的 COM 组件。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 提供了一种简单且安全的机制，用于部署 .NET 应用程序。 但是，如果应用程序使用旧版 COM 组件，则需要执行其他步骤来部署它们。 本主题介绍了如何部署独立的 COM 组件和引用本机组件（例如，从 Visual Basic 6.0 或 Visual C++）。

 有关部署独立 COM 组件的更多信息，请参阅[使用 ClickOnce 和免注册 COM 简化应用部署](https://web.archive.org/web/20050326005413/msdn.microsoft.com/msdnmag/issues/05/04/RegFreeCOM/default.aspx)。

## <a name="registration-free-com"></a>免注册 COM
 免注册 COM 是一种用于部署和激活独立 COM 组件的新技术。 它的工作原理是，将组件的所有类型库和注册信息（通常安装到系统注册表中）放入名为清单的 XML 文件中，该文件与应用程序存储在同一文件夹中。

 隔离 COM 组件需要在开发人员的计算机上注册该组件，但无需在最终用户的计算机上注册。 若要隔离 COM 组件，只需将其引用的 Isolated 属性设置为 True 即可。 默认情况下，此属性设置为 False，指示它应被视为已注册的 COM 引用。 如果此属性为 True，则会导致在生成时为此组件生成清单。 它还会导致在安装过程中将相应的文件复制到应用程序文件夹。

 当清单生成器遇到独立的 COM 引用时，它会枚举组件的类型库中的所有 `CoClass` 条目，将每个条目与其对应的注册数据匹配，并为类型库文件中的所有 COM 类生成清单定义。

## <a name="deploy-registration-free-com-components-using-clickonce"></a>使用 ClickOnce 部署免注册 COM 组件
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署技术非常适合用于部署独立的 COM 组件，因为 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 和免注册 COM 都要求组件具有清单才能被部署。

 通常，组件的作者应提供清单。 但是，如果没有，Visual Studio COM 能够为 COM 组件自动生成清单。 清单生成是在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 发布过程中执行的；有关详细信息，请参阅[发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)。 此功能还允许利用在早期开发环境（如 Visual Basic 6.0）中创作的旧版组件。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署 COM 组件有两种方法：

- 使用引导程序部署 COM 组件；这适用于所有受支持的平台。

- 使用本机组件隔离（也称为免注册 COM）部署。 但是，这仅适用于 Windows XP 或更高版本的操作系统。

### <a name="example-of-isolating-and-deploying-a-simple-com-component"></a>隔离和部署简单 COM 组件的示例
 为了演示免注册 COM 组件部署，此示例将在 Visual Basic 中创建一个基于 Windows 的应用程序，该应用程序引用使用 Visual Basic 6.0 创建的隔离本机 COM 组件，然后使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 进行部署。

 首先，需要创建本机 COM 组件：

##### <a name="to-create-a-native-com-component"></a>创建本机 COM 组件

1. 使用 Visual Basic 6.0，从“文件”菜单中，依次单击“新建”和“项目”。

2. 在“新建项目”对话框中，依次选择“Visual Basic”节点和“ActiveX DLL”项目  。 在“名称”  框中键入 `VB6Hello`。

    > [!NOTE]
    > 免注册 COM 仅支持 ActiveX DLL 和 ActiveX 控件项目类型；不支持 ActiveX EXE 和 ActiveX 文档项目类型。

3. 在“解决方案资源管理器”中，双击 Class1.vb 打开文本编辑器。

4. 在 Class1.vb 中，在 `New` 方法生成的代码后添加以下代码：

    ```vb
    Public Sub SayHello()
       MsgBox "Message from the VB6Hello COM component"
    End Sub
    ```

5. 生成组件。 在“生成”菜单中，单击“生成解决方案”。

> [!NOTE]
> 免注册 COM 仅支持 DLL 和 COM 控件项目类型。 不能将 EXE 与免注册 COM 一起使用。

 现在，可以创建基于 Windows 的应用程序，并向其添加对 COM 组件的引用。

##### <a name="to-create-a-windows-based-application-using-a-com-component"></a>使用 COM 组件创建基于 Windows 的应用程序

1. 使用 Visual Basic，从“文件”菜单中，依次单击“新建”和“项目”。

2. 在“新建项目”对话框中，依次选择“Visual Basic”节点和“Windows 应用程序”。 在“名称”  框中键入 `RegFreeComDemo`。

3. 在“解决方案资源管理器”中，单击“显示所有文件”按钮以显示项目引用。

4. 从上下文菜单中，右键单击“引用”节点并选择“添加引用” 。

5. 在“添加引用”对话框中，单击“浏览”选项卡，导航到 VB6Hello.dll，然后选择它。

    VB6Hello 引用出现在引用列表中。

6. 指向“工具箱”，选择“按钮”控件，然后将其拖动到 Form1 窗体。

7. 在“属性”窗口中，将按钮的“Text”属性设置为“Hello”  。

8. 双击按钮以添加处理程序代码，在代码文件中添加代码，使处理程序如下所示：

   ```vb
   Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
       Dim VbObj As New VB6Hello.Class1
       VbObj.SayHello()
   End Sub
   ```

9. 运行应用程序。 在“调试”菜单中，单击“开始调试” 。

   接下来，需要隔离控件。 应用程序使用的每个 COM 组件在项目中表示为 COM 引用。 这些引用在“解决方案资源管理器”窗口中的“引用”节点下可见。 （请注意，可以使用“项目”菜单上的“添加引用”命令直接添加引用，或者通过将 ActiveX 控件拖动到窗体上间接添加引用。）

   以下步骤显示了如何隔离 COM 组件并发布包含独立控件的更新应用程序：

##### <a name="to-isolate-a-com-component"></a>隔离 COM 组件

1. 在“解决方案资源管理器”中，在“引用”节点中，选择“VB6Hello”引用  。

2. 在“属性”窗口中，将“Isolated”属性的值从“False”更改为“True”   。

3. 在“生成”菜单中，单击“生成解决方案”。

   现在，按 F5 时，应用程序按预期运行，但现在它在免注册 COM 下运行。 为了证明这一点，请尝试取消注册 VB6Hello.dll 组件，并在 Visual Studio IDE 之外运行 RegFreeComDemo1.exe。 此次单击按钮时，它仍然有效。 如果临时重命名应用程序清单，它同样会失败。

> [!NOTE]
> 可以通过暂时取消注册 COM 组件来模拟该组件的缺失。 打开命令提示符，通过键入 `cd /d %windir%\system32` 转到系统文件夹，然后通过键入 `regsvr32 /u VB6Hello.dll` 取消注册组件。 可以通过键入 `regsvr32 VB6Hello.dll` 再次注册它。

 最后一步是使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 发布应用程序：

##### <a name="to-publish-an-application-update-with-an-isolated-com-component"></a>使用独立的 COM 组件发布应用程序更新

1. 从“生成”菜单中，单击“发布 RegFreeComDemo” 。

    出现“发布向导”。

2. 在“发布向导”中，指定本地计算机磁盘上可以访问和检查已发布文件的位置。

3. 单击“完成”以发布应用程序。

   如果检查已发布的文件，将注意到包含 sysmon.ocx 文件。 控件与此应用程序完全隔离，这意味着，如果最终用户计算机有另一个使用不同版本的控件的应用程序，则它不能干扰此应用程序。

## <a name="reference-native-assemblies"></a>引用本机程序集
 Visual Studio 支持对本机 Visual Basic 6.0 或 C++ 程序集的引用；此类引用称为本机引用。 可以通过验证引用的“文件类型”属性是否设置为“本机”或“ActiveX”来判断是否为本机引用。

 若要添加本机引用，请使用“添加引用”命令，然后浏览到清单。 某些组件将清单放在 DLL 中。 在这种情况下，只需选择 DLL 本身，如果 Visual Studio 检测到该组件包含嵌入的清单，则会将其添加为本机引用。 Visual Studio 还将自动包括清单中列出的任何依赖文件或程序集（如果它们与引用的组件在同一文件夹中）。

 通过 COM 控件隔离，可以轻松部署尚未具有清单的 COM 组件。 但是，如果组件随清单一起提供，则可以直接引用清单。 事实上，应始终尽可能使用组件作者提供的清单，而不是使用 Isolated 属性。

## <a name="limitations-of-registration-free-com-component-deployment"></a>免注册 COM 组件部署的限制
 与传统的部署技术相比，免注册 COM 具有明显优势。 但是，还应指出一些限制和注意事项。最大的限制是它仅适用于 Windows XP 或更高版本。 实现免注册 COM 需要更改组件在核心操作系统中的加载方式。 遗憾的是，无注册 COM 没有下级支持层。

 并非每个组件都是免注册 COM 的合适候选项。 如果以下任一项为 True，则组件不适合：

- 组件是进程外服务器。 不支持 EXE 服务器；仅支持 DLL。

- 组件是操作系统的一部分，或者是系统组件（例如 XML、Internet Explorer 或 Microsoft 数据访问组件 (MDAC)。 应遵循组件作者的再分发策略；请咨询供应商。

- 组件是应用程序的一部分，如 Microsoft Office。 例如，不应尝试隔离 Microsoft Excel 对象模型。 这是 Office 的一部分，只能在安装有完整 Office 产品的计算机上使用。

- 组件用作加载项或管理单元（例如 Office 加载项或 Web 浏览器中的控件）。 此类组件通常需要宿主环境定义的某种注册方案，而该方案超出了清单本身的范围。

- 组件管理系统的物理或虚拟设备，例如，打印后台处理程序的设备驱动程序。

- 该组件是可再发行的数据访问组件。 数据应用程序通常需要单独安装可再发行的数据访问组件，然后才能运行。 不应尝试隔离某些组件，如 Microsoft ADO 数据控件、Microsoft OLE DB 或 Microsoft 数据访问组件 (MDAC)。 相反，如果应用程序使用 MDAC 或 SQL Server Express，则应将其设置为先决条件；请参阅[如何：使用 ClickOnce 应用程序安装必备组件](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)。

  在某些情况下，组件的开发人员可能会将其重新设计为免注册 COM。 如果无法做到这一点，则仍可使用引导程序通过标准注册方案生成并发布依赖于它们的应用程序。 有关详细信息，请参阅[创建引导程序包](../deployment/creating-bootstrapper-packages.md)。

  每个应用程序的 COM 组件只能被隔离一次。 例如，不能将同一 COM 组件与属于同一应用程序的两个不同类库项目隔离开来。 这样做会导致生成警告，并且应用程序在运行时将无法加载。 为了避免此问题，Microsoft 建议你将 COM 组件封装在单个类库中。

  有几种方案需要在开发人员的计算机上进行 COM 注册，即使应用程序的部署不需要注册也是如此。 `Isolated` 属性要求在开发人员的计算机上注册 COM 组件，以便在生成过程中自动生成清单。 未提供在生成期间调用自注册的注册捕获功能。 此外，类型库中未显式定义的任何类将不会反映在清单中。 将 COM 组件与预先存在的清单（如本机引用）结合使用时，可能不需要在开发时注册该组件。 但是，如果组件是 ActiveX 控件并且想要将其包含在“工具箱”和“Windows 窗体设计器”中，则需要进行注册。

## <a name="see-also"></a>另请参阅
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)