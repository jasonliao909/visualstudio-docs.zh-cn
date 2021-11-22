---
title: 在 Visual Studio 中调试 SharePoint 工具扩展 | Microsoft Docs
description: 在 Visual Studio 中调试 SharePoint 工具扩展。 调试 VS 试验实例或常规实例中的 SharePoint 工具扩展。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, debugging extensions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: f9b6cb0d017fdfade0b78f2d42609a7e52ad9a3b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602544"
---
# <a name="debug-extensions-for-the-sharepoint-tools-in-visual-studio"></a>在 Visual Studio 中调试 SharePoint 工具扩展
  你可以调试 Visual Studio 试验实例或常规实例中的 SharePoint 工具扩展。 如果需要对扩展行为进行故障排除，还可以修改注册表值以显示其他错误信息，并配置 Visual Studio 执行 SharePoint 命令的方式。

## <a name="debug-extensions-in-the-experimental-instance-of-visual-studio"></a>调试 Visual Studio 试验实例中的扩展
 若要保护 Visual Studio 开发环境，避免未经测试的扩展意外损坏，Visual Studio SDK 提供了一个可选 Visual Studio 实例，称为试验实例，可用于安装和测试扩展。 可以使用 Visual Studio 的常规实例开发新扩展，但在试验实例中进行调试和运行。 有关详细信息，请参阅[试验实例](../extensibility/the-experimental-instance.md)。

 如果使用 VSIX 项目来部署扩展，而 VSIX 项目是解决方案中的启动项目，则调试解决方案时，会自动在试验实例中安装并运行该扩展。 启动项目是在调试包含多个项目的解决方案时启动的项目。 有关使用 VSIX 项目部署扩展的信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

 有关演示如何在 Visual Studio 试验实例中调试各种类型的扩展的示例，请参阅以下演练：

- [演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)

- [演练：使用项模板创建自定义操作项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)

- [演练：为 SharePoint 项目创建自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)

- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)

- [演练：在服务器资源管理器扩展中调入 SharePoint 客户端对象模型](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)

## <a name="debug-extensions-in-the-regular-instance-of-visual-studio"></a>调试 Visual Studio 常规实例中的扩展
 如果要调试 Visual Studio 常规实例中的扩展项目，请首先安装常规实例中的扩展。 然后，将调试程序附加到第二个 Visual Studio 进程。 完成后，可以删除扩展，这样它就不会加载在开发计算机上。

#### <a name="to-install-the-extension"></a>安装扩展

1. 关闭 Visual Studio 的所有实例。

2. 在扩展项目的生成输出文件夹中，通过双击“.vsix”文件或打开其快捷菜单，然后选择“打开”，打开“.vsix”文件：

3. 在“Visual Studio 扩展安装程序”对话框中，选择要安装扩展的 Visual Studio 版本，然后选择“安装”按钮。

     Visual Studio 将扩展文件安装到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0\Extensions\\author name\\extension name\\version  。 此路径中的最后三个文件夹由扩展的 extension.vsixmanifest 文件中的 `Author`、`Name` 和 `Version` 元素构成。

4. Visual Studio 安装扩展后，选择“关闭”按钮。

#### <a name="to-debug-the-extension"></a>调试扩展

1. 使用管理员权限打开 Visual Studio，然后打开扩展项目。 以下步骤将此 Visual Studio 实例称为第一个实例。

2. 使用管理员权限启动另一个 Visual Studio 实例。 以下步骤将此 Visual Studio 实例称为第二个实例。

3. 切换到 Visual Studio 的第一个实例。

4. 在菜单栏上，依次选择“调试”和“附加到进程”。

5. 在“可用进程”列表中，选择“devenv.exe”。 此项引用第二个 Visual Studio 实例；这是要在其中调试项目扩展的实例。

6. 选择“附加”按钮。

     Visual Studio 在调试模式下运行扩展项目。

7. 切换到第二个 Visual Studio 实例。

8. 创建加载扩展的新 SharePoint 项目。 例如，如果要调试列表定义项目项的扩展，请创建“列表定义”项目。

9. 执行测试扩展代码所需的任何步骤。

10. 调试完扩展后，关闭第二个 Visual Studio 实例。

#### <a name="to-remove-the-extension"></a>删除扩展

1. 在 Visual Studio 中，在菜单栏上，选择“工具”，再选择“扩展和更新”。

     此时，“扩展和更新”对话框打开。

2. 在扩展列表中，选择扩展名称，然后选择“卸载”按钮。

3. 在出现的对话框中，选择“是”按钮以确认要卸载扩展。

4. 选择“立即重新启动”按钮以完成卸载。

## <a name="debug-sharepoint-commands"></a>调试 SharePoint 命令
 如果要调试属于 SharePoint 工具扩展的 SharePoint 命令，则必须将调试程序附加到 vssphost4.exe 进程。 这是执行 SharePoint 命令的 64 位主机进程。 有关 SharePoint 命令和 vssphost4.exe 的详细信息，请参阅[调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

#### <a name="to-attach-the-debugger-to-the-vssphost4exe-process"></a>将调试程序附加到 vssphost4.exe 进程

1. 按照上述说明，开始在 Visual Studio 试验实例或 Visual Studio 常规实例中调试扩展。

2. 在运行调试程序的 Visual Studio 的实例中，在菜单栏上，依次选择“调试”和“附加到进程” 。

3. 在“可用进程”列表中，选择“vssphost.exe”。

    > [!NOTE]
    > 如果列表中未出现 vssphost.exe，则必须在运行扩展的 Visual Studio 实例中启动 vssphost4.exe 进程。 通常，可以执行一个操作，使 Visual Studio 连接到开发计算机上的 SharePoint 站点来实现这一目标。 例如，当你在“服务器资源管理器”窗口中的“SharePoint 连接”节点下展开站点连接节点（显示站点 URL 的节点）时或向 SharePoint 项目添加某些 SharePoint 项目项（如“列表实例”或“事件接收器项”）时，Visual Studio 会启动 vssphost4.exe   。

4. 选择“附加”按钮。

5. 在正在调试的 Visual Studio 实例中，执行执行命令所需的步骤。

## <a name="modify-registry-values-to-help-debug-sharepoint-tools-extensions"></a>修改注册表值以帮助调试 SharePoint 工具扩展
 在 Visual Studio 中调试 SharePoint 工具的扩展时，可以修改注册表中的值，以帮助对扩展进行故障排除。 这些值存在于 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\11.0\SharePointTools 键下。 默认情况下，这些值不存在。

 为了帮助对 SharePoint 工具的任何扩展进行故障排除，可以创建并设置 EnableDiagnostics 值。 下表对此值进行了说明。

|值|说明|
|-----------|-----------------|
|EnableDiagnostics|REG_DWORD 指定是否在“输出”窗口中显示诊断消息。<br /><br /> 若要显示诊断消息，将此值设置为 1。 若要停止显示消息，将此值设置为 0 或删除此值。<br /><br /> 若要将消息从 SharePoint 工具扩展写入“Output”窗口，请使用 SharePoint 项目服务。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。|

 如果扩展包含 SharePoint 命令，可以创建和设置其他值以帮助对命令进行故障排除。 下表介绍了这些值。

|值|说明|
|-----------|-----------------|
|AttachDebuggerToHostProcess|REG_DWORD 指定是否显示一个对话框，该对话框使你能够在调调试程序启动时将其附加到 vssphost4.exe。 如果要调试的命令在启动后立即由 vssphost.exe 执行，而且在执行命令之前没有足够的时间手动附加调试程序，则这非常有用。 若要显示对话框，在调试程序启动时，vssphost4.exe 调用 <xref:System.Diagnostics.Debugger.Break%2A> 方法。<br /><br /> 若要启用此行为，将此值设置为 1。 若要关闭此行为，将此值设置为 0 或删除此值。<br /><br /> 如果将此值设置为 1，则你可能还想要增加 HostProcessStartupTimeout 值，以在 Visual Studio 预期 vssphost4.exe 指示调试程序已成功启动之前，为自己提供足够的时间来附加调试程序。|
|ChannelOperationTimeout|REG_DWORD 指定 Visual Studio 等待 SharePoint 命令执行的时间（以秒为单位）。 如果命令未及时执行，则引发 <xref:Microsoft.VisualStudio.SharePoint.SharePointConnectionException>。<br /><br /> 默认值为 120 秒。|
|HostProcessStartupTimeout|REG_DWORD 指定 Visual Studio 等待 vssphost4.exe 指示它已成功启动的时间（以秒为单位）。 如果 vssphost4.exe 未及时指示成功开始，则引发 <xref:Microsoft.VisualStudio.SharePoint.SharePointConnectionException>。<br /><br /> 默认值为 60 秒。|
|MaxReceivedMessageSize|REG_DWORD 指定在 Visual Studio 和 vssphost4.exe 之间传递的 WCF 消息的最大允许大小（以字节为单位）。<br /><br /> 默认值为 1,048,576 字节 (1 MB)。|
|MaxStringContentLength|REG_DWORD 指定在 Visual Studio 和 vssphost4.exe 之间传递的字符串的最大允许大小（以字节为单位）。<br /><br /> 默认值为 1,048,576 字节 (1 MB)。|

## <a name="see-also"></a>另请参阅

- [扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
- [在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
