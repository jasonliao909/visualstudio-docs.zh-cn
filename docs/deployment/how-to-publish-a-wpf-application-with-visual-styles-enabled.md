---
title: 发布启用了视觉样式的 WPF 应用
description: 了解如何发布启用了视觉样式的 WPF 应用程序，从而允许控件的外观根据用户选择的主题更改。
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

视觉样式允许根据用户选择的主题更改常见控件的外观。 默认情况下，对于 WPF 应用程序，Windows Presentation Foundation (视觉) ，因此必须手动启用它们。 但是，为 WPF 应用程序启用视觉样式，然后发布解决方案会导致错误。 本主题介绍如何解决此错误，以及发布启用了视觉样式的 WPF 应用程序的过程。 有关视觉样式详细信息，请参阅 [视觉样式概述](/windows/desktop/Controls/visual-styles-overview)。 有关错误消息的详细信息，请参阅排查部署[中的ClickOnce错误](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md)。

 若要解决此错误并发布解决方案，必须执行以下任务：

- [在未启用视觉样式的情况下发布解决方案](#publish-the-solution-without-visual-styles-enabled)。

- [创建清单文件](#create-a-manifest-file)。

- [将清单文件嵌入已发布解决方案 的可执行文件中](#embed-the-manifest-file-into-the-executable-file-of-the-published-solution)。

- [对应用程序和部署清单进行签名](#sign-the-application-and-deployment-manifests)。

  然后，可以将已发布的文件移动到希望最终用户安装应用程序的位置。

## <a name="publish-the-solution-without-visual-styles-enabled"></a>在未启用视觉样式的情况下发布解决方案

1. 确保项目未启用视觉样式。 首先，检查项目的清单文件，了解以下 XML。 然后，如果存在 XML，请用注释标记将 XML 括起来。

     默认情况下，不会启用视觉样式。

    ```xml
    <dependency>
        <dependentAssembly>
            <assemblyIdentity type="win32" name="Microsoft.Windows.Common-Controls" version="6.0.0.0" processorArchitecture="*" publicKeyToken="6595b64144ccf1df" language="*" />
        </dependentAssembly>
    </dependency>
    ```

     以下过程显示如何打开与项目关联的清单文件。

    **在项目内打开清单Visual Basic文件**

    1. 在菜单栏上，选择 **"Project""***项目名称***属性**"，其中 *"ProjectName"* 是 WPF 项目的名称。

         将显示 WPF 项目的属性页。

    2. 在"应用程序 **"选项卡** 上，选择"**查看Windows 设置"。**

         app.manifest 文件将在代码编辑器 **中打开**。

    **在 C# 项目中打开清单文件**

    1. 在菜单栏上，选择 **"Project""***项目名称***属性**"，其中 *"ProjectName"* 是 WPF 项目的名称。

         将显示 WPF 项目的属性页。

    2. 在 **"应用程序** "选项卡上，记下清单字段中显示的名称。 这是与项目关联的清单的名称。

        > [!NOTE]
        > 如果在 **清单字段中显示"使用默认设置** 嵌入清单"或"创建没有清单的应用程序"，则不启用视觉样式。  如果清单文件的名称出现在清单字段中，请继续执行此过程的下一步。

    3. 在“解决方案资源管理器”中，选择“显示所有文件”。

         此按钮显示所有项目项，包括已排除的项目项和通常隐藏的项目项。 清单文件显示为项目项。

2. 生成并发布解决方案。 若要详细了解如何发布解决方案，请参阅如何：使用发布ClickOnce[发布应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

## <a name="create-a-manifest-file"></a>创建清单文件

1. 将以下 XML 粘贴到记事本文件中。

     此 XML 描述包含支持视觉样式的控件的程序集。

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

2. 在记事本，单击 **"文件"，** 然后单击"**另存为"。**

3. 在"**另存为**"对话框的"**另存** 为类型"下拉列表中，选择"所有 **文件"。**

4. 在 **"文件名"** 框中，为文件命名，将 *.manifest* 追加到文件名的末尾。 例如 *：themes.manifest*。

5. 选择"**浏览文件夹"** 按钮，选择任意文件夹，然后单击"保存 **"。**

    > [!NOTE]
    > 其余过程假定此文件的名称为 *themes.manifest，* 并且该文件已保存到计算机的 *C：\temp* 目录中。

## <a name="embed-the-manifest-file-into-the-executable-file-of-the-published-solution"></a>将清单文件嵌入已发布解决方案的可执行文件中

1. 打开 **Visual Studio 的开发人员命令提示**。

    若要详细了解如何打开 开发人员命令提示 Visual Studio，请参阅 开发人员命令提示[和开发人员 PowerShell。](../ide/reference/command-prompt-powershell.md)

   > [!NOTE]
   > 其余步骤对解决方案做出以下假设：
   >
   > - 解决方案的名称为 **MyWPFProject**。
   > - 解决方案位于以下目录中 `%UserProfile%\Documents\Visual Studio 2010\Projects\` ：。
   >
   > - 解决方案发布到以下目录 `%UserProfile%\Documents\Visual Studio 2010\Projects\publish` ：。
   > - 已发布应用程序文件的最新版本位于以下目录中： `%UserProfile%\Documents\Visual Studio 2010\Projects\publish\Application Files\WPFApp_1_0_0_0`
   >
   > 不需要使用上述名称或目录位置。 上述名称和位置仅用于说明发布解决方案所需的步骤。

2. 在命令提示符下，更改包含已发布应用程序文件的最新版本的目录的路径。 下面的示例演示了此步骤。

   ```cmd
   cd "%UserProfile%\Documents\Visual Studio 2010\Projects\MyWPFProject\publish\Application Files\WPFApp_1_0_0_0"
   ```

3. 在命令提示符下，运行以下命令，将清单文件嵌入应用程序的可执行文件中。

   ```cmd
   mt -manifest c:\temp\themes.manifest -outputresource:MyWPFApp.exe.deploy
   ```

## <a name="sign-the-application-and-deployment-manifests"></a>对应用程序和部署清单进行签名

1. 在命令提示符下，运行以下命令，从当前目录中的可执行文件中删除 *.deploy* 扩展。

   ```cmd
   ren MyWPFApp.exe.deploy MyWPFApp.exe
   ```

   > [!NOTE]
   > 此示例假定只有一个文件具有 *.deploy* 文件扩展名。 请确保重命名此目录中具有 *.deploy* 文件扩展名的所有文件。

2. 在命令提示符下，运行以下命令对应用程序清单进行签名。

   ```cmd
   mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx
   ```

   > [!NOTE]
   > 此示例假定使用项目的 *.pfx* 文件对清单进行签名。 如果未对清单进行签名，可以省略 `-cf` 本示例中使用的 参数。 如果使用需要密码的证书对清单进行签名，请指定 `-password` `For example: mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx - password Password` () 。

3. 在命令提示符下，运行以下命令，将 *.deploy* 扩展名添加到在此过程的上一步中重命名的文件的名称。

   ```
   ren MyWPFApp.exe MyWPFApp.exe.deploy
   ```

   > [!NOTE]
   > 此示例假定只有一个文件具有 *.deploy* 文件扩展名。 请确保重命名此目录中以前扩展名 *为 .deploy* 的所有文件。

4. 在命令提示符下，运行以下命令对部署清单进行签名。

   ```
   mage -u ..\..\MyWPFApp.application -appm MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx
   ```

   > [!NOTE]
   > 此示例假定使用项目的 *.pfx* 文件对清单进行签名。 如果未对清单进行签名，可以省略 `-cf` 本示例中使用的 参数。 如果要使用需要密码的证书对清单进行签名，请指定 选项 `-password` ，如以下示例所示 `For example: mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx - password Password` ：。

   执行这些步骤后，可以将已发布的文件移动到希望最终用户安装应用程序的位置。 如果打算经常更新解决方案，可以将这些命令移动到脚本中，并每次发布新版本时运行该脚本。

## <a name="see-also"></a>另请参阅

- [ClickOnce 部署中的特定错误的疑难解答](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md)
- [视觉样式概述](/windows/desktop/Controls/visual-styles-overview)
- [启用视觉样式](/windows/desktop/Controls/cookbook-overview)
- [开发人员命令提示和开发人员 PowerShell](../ide/reference/command-prompt-powershell.md)
