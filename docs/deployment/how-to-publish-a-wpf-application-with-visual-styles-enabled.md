---
title: 发布已启用视觉样式的 WPF 应用
description: 了解如何发布已启用视觉样式的 WPF 应用程序，该应用程序允许控件的外观基于用户选择的主题进行更改。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 73b22b02-fc75-42aa-82d3-51fdcaf8e5c8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: b231fc6635b5c974898ee2cc85ce8a4a64318039
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664874"
---
# <a name="how-to-publish-a-wpf-application-with-visual-styles-enabled"></a>如何：发布启用了视觉样式的 WPF 应用程序

视觉样式允许基于用户选择的主题更改常见控件的外观。 默认情况下，不会为 Windows Presentation Foundation (WPF) 应用程序启用视觉样式，因为必须手动启用它们。 但是，为 WPF 应用程序启用视觉样式，然后发布解决方案会导致错误。 本主题介绍如何解决该错误，以及发布启用了视觉样式的 WPF 应用程序的过程。 有关视觉样式的详细信息，请参阅[视觉样式概述](/windows/desktop/Controls/visual-styles-overview)。 有关错误消息的详细信息，请参阅[对 ClickOnce 部署中的特定错误进行故障排除](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md)。

 若要解决此错误并发布解决方案，必须执行以下任务：

- [未启用视觉样式时发布解决方案](#publish-the-solution-without-visual-styles-enabled)。

- [创建清单文件](#create-a-manifest-file)。

- [将清单文件嵌入到已发布的解决方案的可执行文件中](#embed-the-manifest-file-into-the-executable-file-of-the-published-solution)。

- [对应用程序清单和部署清单进行签名](#sign-the-application-and-deployment-manifests)。

  然后，可以将已发布的文件移动到希望最终用户安装应用程序的位置。

## <a name="publish-the-solution-without-visual-styles-enabled"></a>未启用视觉样式时发布解决方案

1. 确保项目未启用视觉样式。 首先，针对以下 XML 检查项目的清单文件。 然后，如果存在 XML，请使用注释标记将 XML 括起来。

     默认情况下，不会启用视觉样式。

    ```xml
    <dependency>
        <dependentAssembly>
            <assemblyIdentity type="win32" name="Microsoft.Windows.Common-Controls" version="6.0.0.0" processorArchitecture="*" publicKeyToken="6595b64144ccf1df" language="*" />
        </dependentAssembly>
    </dependency>
    ```

     以下过程介绍如何打开与项目关联的清单文件。

    若要打开 Visual Basic 项目中的清单文件

    1. 在菜单栏上，选择“项目”、“ProjectName”属性，其中“ProjectName”是 WPF 项目的名称。

         WPF 项目的属性页面会显示出来。

    2. 在“应用程序”选项卡上，选择“查看 Windows 设置”。 

         随即会在“代码编辑器”中打开 app.manifest 文件。

    若要打开 C# 项目中的清单文件

    1. 在菜单栏上，选择“项目”、“ProjectName”属性，其中“ProjectName”是 WPF 项目的名称。

         WPF 项目的属性页面会显示出来。

    2. 在“应用程序”选项卡上，对显示在清单字段的名称进行备注。 这是与项目关联的清单的名称。

        > [!NOTE]
        > 如果“使用默认设置嵌入清单”或“创建没有清单文件的应用程序”显示在清单字段，那么不会启用视觉样式。  如果清单文件的名称显示在清单字段中，则继续执行该过程的下一步。

    3. 在“解决方案资源管理器”中，选择“显示所有文件”。

         该按钮显示所有项目项，包括已排除的项目项和那些通常隐藏的项目项。 清单文件显示为项目项。

2. 生成并发布解决方案。 有关如何发布解决方案的详细信息，请参阅[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

## <a name="create-a-manifest-file"></a>创建清单文件

1. 将以下 XML 粘贴到记事本文件中。

     该 XML 介绍了包含支持视觉样式的控件的程序集。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <asmv1:assembly manifestVersion="1.0"
        xmlns="urn:schemas-microsoft-com:asm.v1"
        xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"
        xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <dependency>
            <dependentAssembly>
                <assemblyIdentity type="win32" name="Microsoft.Windows.Common-Controls" version="6.0.0.0" processorArchitecture="*" publicKeyToken="6595b64144ccf1df" language="*" />
            </dependentAssembly>
        </dependency>
    </asmv1:assembly>
    ```

2. 在记事本中，单击“文件”，然后单击“另存为”。 

3. 在“另存为”对话框的“保存类型”下拉列表中，选择“所有文件”  。

4. 在“文件名”框中，给文件命名并将 .manifest 追加到文件名的尾部。 例如：themes.manifest。

5. 选择“浏览文件夹”按钮，选择任意文件夹，然后单击“保存”。 

    > [!NOTE]
    > 剩余步骤假设该文件的名称为 themes.manifest，且该文件保存到计算机的 C:\temp 目录。

## <a name="embed-the-manifest-file-into-the-executable-file-of-the-published-solution"></a>将清单文件嵌入到已发布的解决方案的可执行文件中

1. 打开 **Visual Studio 的开发人员命令提示**。

    若要详细了解如何为 Visual Studio 打开开发人员命令提示，请参阅[开发人员命令提示和开发者 PowerShell](../ide/reference/command-prompt-powershell.md)。

   > [!NOTE]
   > 剩余步骤假设你的解决方案存在以下情况：
   >
   > - 解决方案的名称为 MyWPFProject。
   > - 解决方案位于以下目录：`%UserProfile%\Documents\Visual Studio 2010\Projects\`。
   >
   > - 解决方案发布在以下目录：`%UserProfile%\Documents\Visual Studio 2010\Projects\publish`。
   > - 已发布应用程序文件的最新版本位于以下目录：`%UserProfile%\Documents\Visual Studio 2010\Projects\publish\Application Files\WPFApp_1_0_0_0`
   >
   > 不需要使用上述名称或目录位置。 上述名称和位置仅用于说明发布解决方案所需的步骤。

2. 在命令提示符下，将路径更改为包含已发布应用程序文件的最新版本的目录。 下面的示例演示此步骤。

   ```cmd
   cd "%UserProfile%\Documents\Visual Studio 2010\Projects\MyWPFProject\publish\Application Files\WPFApp_1_0_0_0"
   ```

3. 在命令提示符下，运行以下命令以将清单文件嵌入到应用程序的可执行文件中。

   ```cmd
   mt -manifest c:\temp\themes.manifest -outputresource:MyWPFApp.exe.deploy
   ```

## <a name="sign-the-application-and-deployment-manifests"></a>对应用程序清单和部署清单进行签名

1. 在命令提示符下，运行以下命令以从当前目录的可执行文件删除 .deploy 扩展。

   ```cmd
   ren MyWPFApp.exe.deploy MyWPFApp.exe
   ```

   > [!NOTE]
   > 该示例假设只有一个文件具有 .deploy 文件扩展。 请确保对该目录中具有 .deploy 文件扩展的所有文件进行重命名。

2. 在命令提示符下，运行以下命令以对应用程序清单进行签名。

   ```cmd
   mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx
   ```

   > [!NOTE]
   > 该示例假设使用项目的 .pfx 文件对清单进行签名。 如果未对清单进行签名，则可以省略该示例中使用的 `-cf` 参数。 如果正在对具有需要密码的证书的清单文件进行前面，请指定 `-password` 选项 (`For example: mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx - password Password`)。

3. 在命令提示符下，运行以下命令，以便将 .deploy 扩展添加到在该过程的上一步骤中重命名的文件名中。

   ```
   ren MyWPFApp.exe MyWPFApp.exe.deploy
   ```

   > [!NOTE]
   > 该示例假设只有一个文件具有 .deploy 文件扩展。 请确保对该目录中先前具有 .deploy 文件名扩展的所有文件进行重命名。

4. 在命令提示符下，运行以下命令以对部署清单进行签名。

   ```
   mage -u ..\..\MyWPFApp.application -appm MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx
   ```

   > [!NOTE]
   > 该示例假设使用项目的 .pfx 文件对清单进行签名。 如果未对清单进行签名，则可以省略该示例中使用的 `-cf` 参数。 如果正在对具有需要密码的证书的清单文件进行前面，请指定 `-password` 选项，如该示例中所述：`For example: mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx - password Password`。

   执行这些步骤后，可以将已发布的文件移动到希望最终用户安装应用程序的位置。 如果打算经常更新解决方案，则可以将这些命令移动到脚本中，并在每次发布新版本的时候运行脚本。

## <a name="see-also"></a>另请参阅

- [ClickOnce 部署中的特定错误的疑难解答](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md)
- [视觉样式概述](/windows/desktop/Controls/visual-styles-overview)
- [启用视觉样式](/windows/desktop/Controls/cookbook-overview)
- [开发人员命令提示和开发人员 PowerShell](../ide/reference/command-prompt-powershell.md)
