---
title: 调试 SharePoint 解决方案 | Microsoft Docs
description: 使用 Visual Studio 调试器调试 SharePoint 解决方案。 浏览 F5 调试和部署过程、调试工作流和调试功能事件接收器。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.WebConfigModificationDialog
- VS.SharePointTools.Project.DebuggingNotEnabled
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, debugging
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 63ae84fb6b7450a65962383b986625945440e432
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671939"
---
# <a name="debug-sharepoint-solutions"></a>调试 SharePoint 解决方案
  你可以使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 调试器调试 SharePoint 解决方案。 开始调试时，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会将项目文件部署到 SharePoint 服务器，然后在 Web 浏览器中打开 SharePoint 网站的实例。 以下部分说明如何在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中调试 SharePoint 应用程序。

- [启用调试](#enable-debugging)

- [F5 调试和部署过程](#f5-debug-and-deployment-process)

- [SharePoint 项目功能](#sharepoint-project-features)

- [调试工作流](#debug-workflows)

- [调试功能事件接收器](#debug-feature-event-receivers)

- [启用增强型调试信息](#enable-enhanced-debugging-information)

## <a name="enable-debugging"></a>启用调试
 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中首次调试 SharePoint 解决方案时，会出现一个对话框提醒你，web.config 文件未配置为启用调试。 （web.config 文件是在安装 SharePoint 服务器时创建的。 有关详细信息，请参阅[使用 Web.config 文件](/previous-versions/office/developer/sharepoint-2010/ms460914(v=office.14))。）通过该对话框，你可以选择在不调试的情况下运行项目或修改 web.config 文件以启用调试。 如果选择第一个选项，则项目会正常运行。 如果选择第二个选项，则 web.config 文件将配置为：

- 打开调用堆栈 (`CallStack="true"`)

- 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中禁用自定义错误 (`<customErrors mode="Off" />`)

- 启用编译调试 (`<compilation debug="true">`)

  生成的 web.config 文件如下所示：

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <configuration>
        ...
        <SharePoint>
            <SafeMode MaxControls="200"
                CallStack="true"
                DirectFileDependencies="10"
                TotalFileDependencies="50"
                AllowPageLevelTrace="false">
                ...
            </SafeMode>
        ...
        </SharePoint>
        <system.web>
            ...
            <customErrors mode="Off" />
            ...
            <compilation debug="true">
            ...
            </compilation>
            ...
        </system.web>
        ...
    </configuration>
```

 若要撤消更改并禁用调试，请在 web.config 文件中更改以下 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]：

- 关闭调用堆栈 (`CallStack="false"`)

- 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中启用自定义错误 (`<customErrors mode="On" />`)

- 禁用编译调试 (`<compilation debug="false">`)

## <a name="f5-debug-and-deployment-process"></a>F5 调试和部署过程
 在调试模式下运行 SharePoint 项目时，SharePoint 部署过程将执行以下任务：

1. 运行可自定义的预部署命令。

2. 使用 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 命令创建 Web 解决方案包 (.wsp) 文件。 .wsp 文件包含所有必需的文件和功能。 有关详细信息，请参阅[解决方案概述](/previous-versions/office/developer/sharepoint-2010/aa543214(v=office.14))。

3. 如果 SharePoint 解决方案为场解决方案，则回收指定站点 [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 的 [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] 应用程序池。 此步骤将释放 [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] 工作进程锁定的文件。

4. 如果以前版本的包已存在，则收回 .wsp 文件中以前版本的功能和文件。 此步骤将停用这些功能，卸载解决方案包，然后删除 SharePoint 服务器上的解决方案包。

5. 在 .wsp 文件中安装当前版本的功能和文件。 此步骤在 SharePoint 服务器上添加和安装解决方案。

6. 对于工作流，安装工作流程序集。 可以通过使用程序集位置属性来更改其位置。

7. 如果范围为站点或 Web，则在 SharePoint 中激活项目的功能。 将不激活场和 WebApplication 范围中的功能。

8. 对于工作流，将工作流与你在“SharePoint 自定义向导”中选择的 SharePoint 库、列表或站点相关联。

   > [!NOTE]
   > 仅当在向导中选择了“自动关联工作流”时，才会发生此关联。

9. 运行可自定义的部署后命令。

10. 将 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 调试器附加到 [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] 进程 (w3wp.exe)。 如果项目类型允许更改沙盒解决方案属性，并且其值设置为“true”，则调试器会附加到另一进程 (SPUCWorkerProcess.exe)。 有关详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

11. 如果 SharePoint 解决方案是场解决方案，则启动 JavaScript 调试器。

12. 在 Web 浏览器中显示适当的库、列表或站点页面。

    在每个任务完成后，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会在“输出”窗口中显示一条状态消息。 如果任务无法完成，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 则会在“错误列表”窗口中显示一条错误消息。

## <a name="sharepoint-project-features"></a>SharePoint 项目功能
 功能是一种可移植、模块化的功能单元，它通过使用站点定义来简化站点的修改。 它也是一个 [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] (WSS) 元素包，可以针对特定范围激活并帮助用户完成特定目标或任务。 模板部署为功能。

 在调试模式下运行项目时，部署进程会在 %COMMONPROGRAMFILES%\Microsoft Shared\web server extensions\14\TEMPLATE\FEATURES 的 feature 目录中创建一个文件夹。 功能名称的格式为 project name_Featurex，例如 TestProject_Feature1。 

 功能目录中的解决方案文件夹包含功能定义文件和工作流定义文件。  功能定义文件 (Feature.xml) 用于描述项目功能中的文件。项目定义文件 (Elements.xml) 用于描述项目模板。 Elements.xml 可以在“解决方案资源管理器”中找到，但 Feature.xml 是在创建解决方案包时生成的。 有关这些文件的详细信息，请参阅 [SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

## <a name="debug-workflows"></a>调试工作流
 在调试工作流项目时，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会将工作流模板（取决于其类型）添加到库或列表中。 然后，你可以手动启动工作流模板，也可以通过添加或更新项来启动它。 然后，可以使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 调试工作流。

> [!NOTE]
> 如果你添加了对其他程序集的引用，请确保将这些程序集安装在全局程序集缓存 ([!INCLUDE[TLA2#tla_gac](../sharepoint/includes/tla2sharptla-gac-md.md)]) 中。 否则，工作流解决方案将失败。 有关如何安装程序集的信息，请参阅[在文档或项上手动启动工作流](https://support.office.com/article/Manually-start-a-workflow-on-a-document-or-item-5C106E0E-6FF2-4A75-AF99-F01653BC7963)。

 但是，部署过程不会启动工作流。 必须从 SharePoint 网站启动工作流。 也可以通过使用客户端应用程序（如 Microsoft Office Word 2010）或使用单独的服务器端代码来启动工作流。 请使用“SharePoint 自定义向导”中指定的一种方法。

 例如，如果你指定可以手动启动工作流，请直接从库或列表中的项启动工作流。 有关如何手动启动工作流的详细信息，请参阅[在文档项上手动启动工作流](https://support.office.com/article/Manually-start-a-workflow-on-a-document-or-item-5C106E0E-6FF2-4A75-AF99-F01653BC7963)。

## <a name="debug-feature-event-receivers"></a>调试功能事件接收器
 默认情况下，当你运行 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint 应用程序时，将自动在 SharePoint 服务器上为你激活其功能。 但是，这会在你调试功能事件接收器时导致问题，因为当 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 激活某项功能时，它会在与调试器不同的进程中运行。 这意味着某些调试功能（例如断点）将无法正常工作。

 若要在 SharePoint 中禁用功能的自动激活并允许对功能事件接收器进行适当调试，请在调试前将项目的“活动部署配置”属性的值设置为“不激活”。  然后，在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中开始调试 SharePoint 应用程序后，在 SharePoint 中手动激活此功能。 为此，请在 SharePoint 中打开“站点操作”菜单，选择“站点设置”，再选择“管理站点功能”链接，然后选择功能旁边的“激活”按钮，将调试恢复为正常状态。   

## <a name="enable-enhanced-debugging-information"></a>启用增强型调试信息
 由于 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 进程 (devenv.exe)、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint 主机进程 (vssphost4.exe)、SharePoint 和 WCF 层之间有时会进行复杂的交互，因此诊断在构建、部署等过程中发生的错误可能是一个挑战。 为了解决此类错误，可以启用增强型调试信息。 为此，请转到 Windows 注册表中的以下注册表项：

 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\11.0\SharePointTools

 如果“EnableDiagnostics”REG_DWORD 值已不存在，请手动创建它。 将“EnableDiagnostics”值设置为“1”。

 将此键值设置为 1 会导致在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中运行时，每当出现项目系统错误时，堆栈跟踪信息都会出现在“输出”窗口中。 若要禁用增强的调试信息，请将 EnableDiagnostics 设置回 0 或者删除该值。

 有关其他 SharePoint 注册表项的详细信息，请参阅[在 Visual Studio 中调试 SharePoint 工具扩展](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [SharePoint 解决方案疑难解答](../sharepoint/troubleshooting-sharepoint-solutions.md)
