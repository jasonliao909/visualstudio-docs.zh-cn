---
title: 手动部署 ClickOnce 应用
description: 了解如何使用清单生成和编辑工具的命令行版本或图形版本创建 ClickOnce 部署。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Mage.exe, manual ClickOnce deployments
- MageUI.exe, manual ClickOnce deployments
- deploying applications [ClickOnce], manual ClickOnce deployments
- ClickOnce deployment, manually
- ClickOnce deployment, SDK tools
- manual ClickOnce deployments
- manifests [ClickOnce]
ms.assetid: ccee6551-a1b9-4ca2-8845-9c1cf4ac2560
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 83bc3a73bede906f23dfc2b561bc3e2e3179af81
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671802"
---
# <a name="walkthrough-manually-deploy-a-clickonce-application"></a>演练：手动部署 ClickOnce 应用程序
如果无法使用 Visual Studio 部署 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序，或者需要使用高级部署功能（例如受信任的应用程序部署），你应使用 Mage.exe 命令行工具来创建 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 清单。 本演练介绍了如何使用清单生成和编辑工具的命令行版本 (Mage.exe) 或图形版本 (MageUI.exe) 来创建 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署 。

## <a name="prerequisites"></a>先决条件
 本演练包含一些需要在生成部署之前选择的先决条件和选项。

- 安装 Mage.exe 和 MageUI.exe 。

   Mage.exe 和 MageUI.exe 是 [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] 的一部分 。 必须安装了 [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] 或 Visual Studio 附带的 [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] 版本。 有关详细信息，请参阅 MSDN 上的 [Windows SDK](https://www.microsoft.com/download/details.aspx?id=8279)。

- 提供要部署的应用程序。

   本演练假设有一个可供部署的 Windows 应用程序。 此应用程序将称为 AppToDeploy。

- 确定部署的分发方式。

   分发选项包括：Web、文件共享或 CD。 有关详细信息，请参阅 [ClickOnce Security and Deployment](../deployment/clickonce-security-and-deployment.md)。

- 确定应用程序是否需要更高级别的信任。

   如果应用程序需要完全信任（例如对用户系统的完全访问权限），可以使用 Mage.exe 的 `-TrustLevel` 选项进行设置。 如果要为应用程序定义自定义权限集，可以从另一个清单复制 Internet 或 Intranet 权限部分，修改它以满足你的需要，然后使用文本编辑器或 MageUI.exe 将其添加到应用程序清单。 有关详细信息，请参阅[受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。

- 获取验证码证书。

   应使用验证码证书对部署进行签名。 可使用 Visual Studio、MageUI.exe 或 MakeCert.exe 以及 Pvk2Pfx.exe 工具生成测试证书，也可以从证书颁发机构 (CA) 获取证书  。 如果选择使用受信任的应用程序部署，还必须在所有客户端计算机上一次性安装证书。 有关详细信息，请参阅 [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md)。

  > [!NOTE]
  > 也可使用可从证书颁发机构获取的 CNG 证书对部署进行签名。

- 确保应用程序没有包含 UAC 信息的清单。

   需要确定应用程序是否包含带有用户帐户控制 (UAC) 信息（例如 `<dependentAssembly>` 元素）的清单。 若要检查应用程序清单，可以使用 Windows Sysinternals [Sigcheck](/sysinternals/downloads/sigcheck) 实用工具。

   如果应用程序包含带有 UAC 详细信息的清单，你必须重新生成不含 UAC 信息的清单。 对于 Visual Studio 中的 C# 项目，打开“项目”属性并选择“应用程序”选项卡。在“清单”下拉列表中，选择“创建没有清单的应用程序” 。 对于 Visual Studio 中的 Visual Basic 项目，打开“项目”属性，选择“应用程序”选项卡，然后单击“查看 UAC 设置”。 在打开的清单文件中，删除单个 `<asmv1:assembly>` 元素中的所有元素。

- 确定应用程序是否需要针对客户端计算机的先决条件。

   从 Visual Studio 部署的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序可在部署中包含先决条件安装引导程序 (setup.exe)。 本演练创建了 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署所需的两个清单。 可以使用 [GenerateBootstrapper 任务](../msbuild/generatebootstrapper-task.md)来创建先决条件引导程序。

### <a name="to-deploy-an-application-with-the-mageexe-command-line-tool"></a>使用 Mage.exe 命令行工具部署应用程序

1. 创建一个用于存储 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署文件的目录。

2. 在刚刚创建的部署目录中，创建一个版本子目录。 如果这是第一次部署应用程序，请将版本子目录命名为 1.0.0.0。

   > [!NOTE]
   > 部署版本可与应用程序版本不同。

3. 将所有应用程序文件（包括可执行文件、程序集、资源和数据文件）复制到版本子目录。 如有必要，可以创建包含其他文件的其他子目录。

4. 打开 [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] 或 Visual Studio 命令提示符并对版本子目录进行更改。

5. 通过调用 Mage.exe 创建应用程序清单。 以下语句为编译为在 Intel x86 处理器上运行的代码创建应用程序清单。

   ```cmd
   mage -New Application -Processor x86 -ToFile AppToDeploy.exe.manifest -name "My App" -Version 1.0.0.0 -FromDirectory .
   ```

   > [!NOTE]
   > 请确保在 `-FromDirectory` 选项后添加句点 (.)，它表示当前目录。 如果不添加句点，则必须指定应用程序文件的路径。

6. 使用验证码证书对应用程序清单进行签名。 将 mycert.pfx 替换为证书文件的路径。 将 passwd 替换为证书文件的密码。

   ```cmd
   mage -Sign AppToDeploy.exe.manifest -CertFile mycert.pfx -Password passwd
   ```

   从随 Visual Studio 和 Windows SDK 一起分发的 .NET Framework 4.6.2 SDK 开始，mage.exe 使用 CNG 和验证码证书对清单进行签名。 使用与验证码证书相同的命令行参数。

7. 更改为部署目录的根目录。

8. 通过调用 Mage.exe 生成部署清单。 默认情况下，Mage.exe 会将 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署标记为已安装的应用程序，以便它可以联机和脱机运行。 若要使应用程序仅在用户联机时可用，请使用值为 `false` 的 `-Install` 选项。 如果使用默认值，并且用户将从网站或文件共享安装应用程序，请确保 `-ProviderUrl` 选项的值指向 Web 服务器或共享上的应用程序清单的位置。

   ```cmd
   mage -New Deployment -Processor x86 -Install true -Publisher "My Co." -ProviderUrl "\\myServer\myShare\AppToDeploy.application" -AppManifest 1.0.0.0\AppToDeploy.exe.manifest -ToFile AppToDeploy.application
   ```

9. 使用验证码或 CNG 证书对部署清单进行签名。

    ```cmd
    mage -Sign AppToDeploy.application -CertFile mycert.pfx -Password passwd
    ```

10. 将部署目录中的所有文件复制到部署目标或介质。 这可以是网站或 FTP 站点上的文件夹、文件共享或 CD-ROM。

11. 为用户提供安装应用程序所需的 URL、UNC 或物理介质。 如果提供了 URL 或 UNC，则必须为用户提供部署清单的完整路径。 例如，如果 AppToDeploy 部署到 AppToDeploy 目录中的 http://webserver01/ ，则完整的 URL 路径将为 http://webserver01/AppToDeploy/AppToDeploy.application 。

### <a name="to-deploy-an-application-with-the-mageuiexe-graphical-tool"></a>使用 MageUI.exe 图形工具部署应用程序

1. 创建一个用于存储 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署文件的目录。

2. 在刚刚创建的部署目录中，创建一个版本子目录。 如果这是第一次部署应用程序，请将版本子目录命名为 1.0.0.0。

   > [!NOTE]
   > 部署版本可能与应用程序版本不同。

3. 将所有应用程序文件（包括可执行文件、程序集、资源和数据文件）复制到版本子目录。 如有必要，可以创建包含其他文件的其他子目录。

4. 启动 MageUI.exe 图形工具。

   ```cmd
   MageUI.exe
   ```

5. 从菜单中依次选择“文件”、“新建”、“应用程序清单”，创建新的应用程序清单  。

6. 在默认的“名称”选项卡上，键入此部署的名称和版本号。 另需指定为应用程序构建的处理器，例如 x86。

7. 选择“文件”选项卡，然后选择“应用程序目录”文本框旁边的省略号 (...) 按钮  。 将显示“浏览文件夹”对话框。

8. 选择包含应用程序文件的版本子目录，然后选择“确定”。

9. 如果将从 Internet Information Services (IIS) 部署，请选中“在填充时将 .deploy 扩展名添加到任何不带该扩展名的文件”复选框。

10. 转到“填充”按钮，将所有应用程序文件添加到文件列表中。 如果应用程序包含多个可执行文件，请从“文件类型”下拉列表中选择“入口点”，将此部署的主要可执行文件标记为启动应用程序 。 （如果应用程序仅包含一个可执行文件，MageUI.exe 会标记该文件。）

11. 选择“所需的权限”选项卡并选择需要应用程序断言的信任级别。 默认值为 FullTrust，适用于大多数应用程序。

12. 从菜单中依次选择“文件”、“另存为” 。 系统将出现一个“签名选项”对话框，提示你对应用程序清单进行签名。

13. 如果将证书作为文件存储在文件系统上，请使用“使用证书文件签名”选项，然后使用省略号 (…) 按钮从文件系统中选择证书 。 然后键入证书密码。

     -或-

     如果证书保存在可从计算机访问的证书存储中，请选择“使用存储的证书签名”选项，然后从提供的列表中选择证书。

14. 选择“确定”以对应用程序清单进行签名。 将显示 **“另存为”** 对话框。

15. 在“另存为”对话框中，指定版本目录，然后选择“保存” 。

16. 从菜单中依次选择“文件”、“新建”、“部署清单”，以创建部署清单  。

17. 在“名称”选项卡上，为此部署指定名称和版本号（在本示例中为 1.0.0.0） 。 另需指定为应用程序构建的处理器，例如 x86。

18. 选择“说明”选项卡，并指定“发布者”和“产品”的值  。 （当应用程序安装在客户端计算机上以供脱机使用时，“产品”是在 Windows“开始”菜单上为应用程序指定的名称。）

19. 选择“部署选项”选项卡，然后在“开始位置”文本框中，指定应用程序清单在 Web 服务器或共享上的位置 。 例如 \\\myServer\myShare\AppToDeploy.application。

20. 如果在上一步中添加了 .deploy 扩展名，还需在此处选择“使用 .deploy 文件扩展名”。

21. 选择“更新选项”选项卡，并指定希望此应用程序更新的频率。 如果应用程序使用 <xref:System.Deployment.Application.UpdateCheckInfo> 自行检查更新，请清除“此应用程序应检查更新”复选框。

22. 选择“应用程序引用”选项卡，然后转到“选择清单”按钮 。 此时会出现“打开”对话框。

23. 选择之前创建的应用程序清单，然后选择“打开”。

24. 从菜单中依次选择“文件”、“另存为” 。 系统将出现一个“签名选项”对话框，提示你对部署清单进行签名。

25. 如果将证书作为文件存储在文件系统上，请使用“使用证书文件签名”选项，然后使用省略号 (…) 按钮从文件系统中选择证书 。 然后键入证书密码。

     -或-

     如果证书保存在可从计算机访问的证书存储中，请选择“使用存储的证书签名”选项，然后从提供的列表中选择证书。

26. 转到“确定”以对部署清单进行签名。 将显示 **“另存为”** 对话框。

27. 在“另存为”对话框中，将一个目录上移到部署的根目录，然后选择“保存” 。

28. 将部署目录中的所有文件复制到部署目标或介质。 这可以是网站或 FTP 站点上的文件夹、文件共享或 CD-ROM。

29. 为用户提供安装应用程序所需的 URL、UNC 或物理介质。 如果提供了 URL 或 UNC，则必须为用户提供部署清单的完整路径。 例如，如果 AppToDeploy 部署到 AppToDeploy 目录中的 http://webserver01/ ，则完整的 URL 路径将为 http://webserver01/AppToDeploy/AppToDeploy.application 。

## <a name="next-steps"></a>后续步骤
 当需要部署新版本的应用程序时，创建一个以新版本（例如 1.0.0.1）命名的新目录，并将新的应用程序文件复制到新目录中。 接下来，需要按照前面的步骤创建和签名新的应用程序清单，并更新和签名部署清单。 务必要在 Mage.exe `-New` 和 `-Update` 调用中指定相同的最新版本，因为 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 仅更新最新的版本，以版本号最左边的整数为准。 如果使用的是 MageUI.exe，则可以通过以下方式更新部署清单：打开部署清单，选择“应用程序引用”选项卡，转到“选择清单”按钮，然后选择更新后的应用程序清单 。

## <a name="see-also"></a>另请参阅
- [Mage.exe（清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [MageUI.exe（图形化客户端中的清单生成和编辑工具）](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
