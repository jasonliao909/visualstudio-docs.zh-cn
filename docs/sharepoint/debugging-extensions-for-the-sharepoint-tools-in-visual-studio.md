---
title: 调试中 SharePoint Tools 的Visual Studio |Microsoft Docs
description: 调试 Visual Studio 中 SharePoint 工具的扩展。 调试SharePoint实例或 VS 的常规实例中的工具扩展。
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
ms.openlocfilehash: 11cfbc1386ccd7994e2594f8ddde4a1add3613d27c0fcf1782a3d9dd2a1ed13a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121353041"
---
# <a name="debug-extensions-for-the-sharepoint-tools-in-visual-studio"></a>在 Visual Studio 中调试 SharePoint 工具扩展
  可以在试验SharePoint或实例的常规实例中调试Visual Studio。 如果需要对扩展的行为进行故障排除，还可以修改注册表值以显示其他错误信息，并配置Visual Studio命令SharePoint方式。

## <a name="debug-extensions-in-the-experimental-instance-of-visual-studio"></a>调试试验实例中的扩展Visual Studio
 为了Visual Studio开发环境不经测试的扩展意外损坏，Visual Studio SDK 提供了一个称为实验性实例的 Visual Studio 实例，可用于安装和测试扩展。  使用 常规实例开发新的扩展Visual Studio，但在实验实例中调试和运行它们。 有关详细信息，请参阅 [实验实例](../extensibility/the-experimental-instance.md)。

 如果使用 VSIX 项目来部署扩展，并且 VSIX 项目是解决方案中的启动项目，Visual Studio调试解决方案时自动在试验实例中安装并运行该扩展。 启动项目是在调试包含多个项目的解决方案时启动的项目。 有关使用 VSIX 项目部署扩展的信息，请参阅在 Visual Studio 中为 SharePoint[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

 有关演示如何在 Visual Studio 试验实例中调试各种类型的扩展的示例，请参阅以下演练：

- [演练：扩展SharePoint项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)

- [演练：使用项模板创建自定义操作项目项，第 1 部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)

- [演练：为项目创建SharePoint步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)

- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)

- [演练：调用 SharePoint 扩展中的 服务器资源管理器 客户端对象模型](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)

## <a name="debug-extensions-in-the-regular-instance-of-visual-studio"></a>调试常规实例中的扩展Visual Studio
 如果要在常规实例中调试扩展项目Visual Studio，请首先在常规实例中安装扩展。 然后，将调试器附加到第二Visual Studio进程。 完成后，可以删除扩展，以便它不再在开发计算机上加载。

#### <a name="to-install-the-extension"></a>安装扩展

1. 关闭 Visual Studio 的所有实例。

2. 在扩展项目的生成输出文件夹中，双击 *.vsix* 文件，或者打开其快捷菜单，然后选择"打开 **"以打开该文件**：

3. 在 **"Visual Studio** 安装程序"对话框中，选择要Visual Studio扩展的版本，然后选择"安装 **"** 按钮。

     Visual Studio将扩展文件安装到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0\Extensions 作者扩展 \\  \\ *名* \\ *版本*。 此路径中的最后三个文件夹是使用扩展的 `Author` `Name` `Version` *extension.vsixmanifest* 文件中 、 和 元素构造的。

4. 安装Visual Studio后，选择"关闭 **"** 按钮。

#### <a name="to-debug-the-extension"></a>调试扩展

1. 使用Visual Studio权限打开"扩展"，并打开扩展项目。 以下步骤将此 实例Visual Studio作为 *第一个实例*。

2. 使用管理员权限启动Visual Studio实例。 以下步骤将此 实例Visual Studio作为第 *二个实例*。

3. 切换到第一个实例Visual Studio。

4. 在菜单栏上，选择"**调试"，****然后选择"附加到进程"。**

5. 在"**可用进程"** 列表中，选择 *"devenv.exe"。* 此项引用第二个实例Visual Studio;这是要调试项目扩展的实例。

6. 选择" **附加"** 按钮。

     Visual Studio调试模式下运行扩展项目。

7. 切换到第二个实例Visual Studio。

8. 创建一SharePoint扩展的新项目。 例如，如果要调试列表定义项目项的扩展，请创建列表 **定义** 项目。

9. 执行测试扩展代码所需的任何步骤。

10. 完成扩展调试后，关闭扩展的第二Visual Studio。

#### <a name="to-remove-the-extension"></a>删除扩展

1. 在Visual Studio菜单栏上，选择"**工具****"、"扩展和更新"。**

     此时，“扩展和更新”对话框打开。

2. 在扩展列表中，选择扩展的名称，然后选择"卸载 **"** 按钮。

3. 在出现的对话框中，选择" **是"** 按钮以确认要卸载扩展。

4. 选择" **立即重启** "按钮以完成卸载。

## <a name="debug-sharepoint-commands"></a>调试SharePoint命令
 如果要调试属于 SharePoint 工具扩展的 SharePoint 命令，则必须将调试器附加到 *vssphost4.exe进程。* 这是执行以下命令的 64 位SharePoint进程。 有关命令和 *SharePointvssphost4.exe，* 请参阅调用 [SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

#### <a name="to-attach-the-debugger-to-the-vssphost4exe-process"></a>将调试器附加到vssphost4.exe进程

1. 按照上述说明，开始在 Visual Studio 或 Visual Studio 的常规实例中调试扩展。

2. 在运行Visual Studio的实例中，在菜单栏上，选择"调试 **"，然后选择**"**附加到进程"。**

3. 在"**可用进程"** 列表中，选择 *"vssphost.exe"。*

    > [!NOTE]
    > 如果未vssphost.exe，则必须在运行扩展的vssphost4.exe实例中启动 Visual Studio进程。 通常，通过执行一个操作来Visual Studio连接到开发SharePoint站点。 例如，Visual Studio 在展开站点连接节点 (在 服务器资源管理器 窗口中的 **SharePoint 连接** 节点下显示站点 URL **)** 的节点，或者将某些 SharePoint 项目项（如列表实例或事件接收器项）添加到 SharePoint 项目时，将启动vssphost4.exe。  

4. 选择" **附加"** 按钮。

5. 在正在Visual Studio实例中，执行执行命令所需的步骤。

## <a name="modify-registry-values-to-help-debug-sharepoint-tools-extensions"></a>修改注册表值以帮助调试SharePoint扩展
 在 Visual Studio 中调试 SharePoint 工具的扩展时，可以修改注册表中的值，以帮助对扩展进行故障排除。 这些值存在于键 **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\11.0\SharePointTools** 下。 默认情况下，这些值不存在。

 为了帮助排查扩展工具SharePoint，可以创建并设置 EnableDiagnostics 值。 下表描述了此值。

|值|说明|
|-----------|-----------------|
|EnableDiagnostics|REG_DWORD指定是否在"输出"窗口中显示 **诊断** 消息。<br /><br /> 若要显示诊断消息，将此值设置为 1。 若要停止显示消息，将此值设置为 0 或删除此值。<br /><br /> 若要将消息从工具扩展SharePoint"输出"窗口，请使用SharePoint 项目服务。 有关详细信息，请参阅使用[SharePoint 项目服务。](../sharepoint/using-the-sharepoint-project-service.md)|

 如果扩展包含 SharePoint 命令，可以创建和设置其他值以帮助对命令进行故障排除。 下表介绍了这些值。

|值|说明|
|-----------|-----------------|
|AttachDebuggerToHostProcess|REG_DWORD指定是否显示一个对话框，该对话框使你能够在调试器启动时vssphost4.exe附加调试器。  如果要调试的命令在启动后立即由 vssphost.exe执行，并且没有足够的时间在执行命令之前手动附加调试器，则这非常有用。 若要显示对话框 *，vssphost4.exe时* <xref:System.Diagnostics.Debugger.Break%2A> 调用 方法。<br /><br /> 若要启用此行为，将此值设置为 1。 若要关闭此行为，将此值设置为 0 或删除此值。<br /><br /> 如果将此值设置为 1，则你可能还希望增加 HostProcessStartupTimeout 值，以在 Visual Studio 预期vssphost4.exe指示调试器已成功启动之前，为自己 *提供足够的时间来附加* 调试器。|
|ChannelOperationTimeout|REG_DWORD指定等待命令执行Visual Studio的时间（SharePoint秒）。 如果命令未实时执行，则 <xref:Microsoft.VisualStudio.SharePoint.SharePointConnectionException> 会引发 。<br /><br /> 默认值为 120 秒。|
|HostProcessStartupTimeout|REG_DWORD，它指定用户等待Visual Studio时间（*以* 秒vssphost4.exe来指示它已成功启动。 如果 *vssphost4.exe* 未指示开始时间成功，则 <xref:Microsoft.VisualStudio.SharePoint.SharePointConnectionException> 会引发 。<br /><br /> 默认值为 60 秒。|
|MaxReceivedMessageSize|REG_DWORD指定在 Visual Studio 和 之间传递的 WCF 消息的最大允许 *大小（以字节vssphost4.exe）。*<br /><br /> 默认值为1048576字节 (1 MB) 。|
|MaxStringContentLength|REG_DWORD，它指定在 Visual Studio 和 *vssphost4.exe* 之间传递的字符串的最大允许大小（以字节为单位）。<br /><br /> 默认值为1048576字节 (1 MB) 。|

## <a name="see-also"></a>另请参阅

- [扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
- [在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
