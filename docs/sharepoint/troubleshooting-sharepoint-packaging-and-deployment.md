---
title: 打包SharePoint部署故障排除|Microsoft Docs
description: 了解并修复打包和部署解决方案时可能会遇到的SharePoint问题。
ms.custom: SEO-VS-2020
ms.date: 02/22/2017
ms.topic: conceptual
f1_keywords:
- VSTO.WorkflowDeployment.Troubleshooting
- VS.SharePointTools.Project.PackageRetraction
- VS.SharePointTools.Deployment.Troubleshooting
- VS.SharePointTools.Deploying.Troubleshooting
- VS.SharePointTools.Project.DeploymentTroubleshooting
- VS.SharePointTools.Project.SharePointNotInstalled
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packaging
- SharePoint development in Visual Studio, troubleshooting
- SharePoint development in Visual Studio, deployment conflict resolution
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 6d02271664f9a259754c19c9ae90612b76e1645c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122156248"
---
# <a name="troubleshoot-sharepoint-packaging-and-deployment"></a>对SharePoint和部署进行故障排除
  本主题论述了您在打包和部署 SharePoint 解决方案时可能遇到的各种问题。

## <a name="enable-enhanced-debugging"></a>启用增强的调试
 若要在 Visual Studio、SharePoint 和其他层之间进行诊断，您可以使用 EnableDiagnostics 注册表项来查看堆栈跟踪。 有关详细信息，请参阅调试[SharePoint解决方案](../sharepoint/debugging-sharepoint-solutions.md)。

## <a name="add-project-output-to-the-solution-package"></a>将项目输出添加到解决方案包
 可以通过包设计器向包中添加项目输出。 但是，在添加项目输出时，请确保项目的平台与 SharePoint 解决方案的平台匹配。 建议对要部署到服务器中的程序集使用"任何 **CPU** 平台SharePoint目标。 有关详细信息，请参阅"编译"页[、Project设计器](../ide/reference/compile-page-project-designer-visual-basic.md)&#40;Visual Basic&#41;和"高级编译器设置[对话框&#40;Visual Basic&#41;。 ](../ide/reference/advanced-compiler-settings-dialog-box-visual-basic.md)

## <a name="validation-warnings-and-errors"></a>验证警告和错误
 Visual Studio 中的 SharePoint 开发工具将执行验证步骤来验证解决方案包的格式是否正确。 也可以为功能和包创建自定义验证步骤。 有关详细信息，请参阅[如何：为 SharePoint 解决方案创建自定义功能和包验证规则](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md)。

## <a name="deployment-conflict-resolution"></a>部署冲突解决
 在部署 SharePoint 解决方案时，当服务器上的项与解决方案包中的项具有相同的名称、URL 或 ID 时，您可能会发现冲突。 可以更改" **部署冲突解决"** 属性，解决、报告或忽略模块、Web 部件、列表实例和内容类型的冲突。

 下表演示了"部署冲突 **解决"属性** 的设置。

|值|说明|
|-----------|-----------------|
|自动|自动检测冲突和解决冲突。|
|提示|检测冲突并在解决冲突之前向开发人员报告冲突。|
|无|不检测冲突。|

## <a name="differences-between-f5-deployment"></a>F5 部署之间的差异
 当你使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 SharePoint 项目部署到本地 SharePoint 服务器进行测试和调试时，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将执行一些其他步骤。

1. 在部署步骤过程中重置 Internet Information Services (IIS)。

2. 自动关联工作流。

3. 根据包设计器中的层次结构设置功能激活顺序。

   可以添加自定义部署步骤以进一步更改 **F5** 行为。 有关详细信息，请参阅[演练：为项目创建自定义SharePoint步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)。

## <a name="delay-displaying-sharepoint-page-when-deploy-visual-web-part"></a>部署可视 Web 部件SharePoint延迟显示页面
 在 [!INCLUDE[wiprlhext](../sharepoint/includes/wiprlhext-md.md)]、[!INCLUDE[win7](../sharepoint/includes/win7-md.md)] 或 [!INCLUDE[winsvr08](../sharepoint/includes/winsvr08-md.md)] 上将可视 Web 部件部署到 Bin 文件夹时，SharePoint 页需要很长时间才会显示。 如果更改顶级 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 目录（例如 Bin 目录）中的任何文件，则整个 Web 应用程序将重新编译。 这可能会导致 SharePoint 页延迟长达 25 秒才会呈现。

### <a name="error-message"></a>错误消息
 无。

### <a name="resolution"></a>解决方案
 若要解决此问题，请执行以下步骤：

1. 安装更新 KB967535，如 Microsoft 支持 文章修复：修补程序可用于修复 Windows Vista 和[Windows Server 2008 的 IIS 7.0](https://support.microsoft.com/help/967535)上的 ASP.NET 中的两个问题。

2. 将以下行添加到 Web.config 文件中：

    ```xml
    <compilation batch="false" optimizeCompilations="true">
    ```

## <a name="sharepoint-project-deployment-fails-with-error-failed-to-extract-the-cab-file-in-the-solution"></a>SharePoint项目部署失败，并出现错误"无法提取解决方案中的 cab 文件"
 如果任何 SharePoint 项目项的名称包含括号，则该项目项的解决方案将无法部署，并返回一个错误。

### <a name="error-message"></a>错误消息
 在‘添加解决方案’这一部署步骤中发生错误：“未能提取解决方案中的 cab 文件”。

### <a name="resolution"></a>解决方案
 若要解决此问题，请移除 SharePoint 项目项名称中的任何括号。

## <a name="error-appears-when-deploying-a-visual-web-part-to-a-site-on-a-different-web-application"></a>将可视 Web 部件部署到其他 Web 应用程序上的站点时出现错误
 首次将可视 Web 部件部署到 Web 应用程序上当前已部署该部件的网站之外的另一个网站时（通过更改可视 Web 部件的 SiteUrl 属性），会收到错误。

### <a name="error-message"></a>错误消息
 在‘添加解决方案’这一部署步骤中发生错误：“已在该场中安装 ID 为 [#] 的功能”。 使用强制特性显式重新安装此功能。

### <a name="resolution"></a>解决方案
 此错误因 SharePoint 中收回可视 Web 部件功能的方式导致发生。 若要成功部署可视化 Web 部件，请再次通过选择 **F5 键来部署** 解决方案。

## <a name="warning-appears-when-deploying-nested-user-controls"></a>部署嵌套用户控件时出现警告
 在你部署包含嵌套用户控件（如包含用户控件的可视 Web 部件或包含可视 Web 部件或其他用户控件的用户控件）的 SharePoint 解决方案时会出现此警告。 无论是通过从"工具箱"拖动控件还是通过使用"源"视图中的 指令将控件添加到设计器，都会出现 @Register 此警告。

### <a name="error-message"></a>错误消息
 警告 1 元素"[*控件名称*]"不是已知元素。 如果网站中存在编译错误或缺少 web.config 文件，则会出现此警告。

### <a name="resolution"></a>解决方案
 如果项目系统不知道嵌套用户控件，则它无法提供 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] IntelliSense 并发出警告。 如果未生成项目且设计器在未关闭和重新打开，或者启用了自动收回选项（这会导致在调试后从 SharePoint 收回用户控件），则项目系统将无法识别嵌套用户控件。

 若要删除此警告，请生成项目，然后关闭设计器并重新打开设计器，或者禁用项目的自动收回选项。 为此，请清除"项目属性 **"对话框的**"SharePoint选项卡上的"调试后自动收回"复选框。

## <a name="see-also"></a>请参阅

- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)