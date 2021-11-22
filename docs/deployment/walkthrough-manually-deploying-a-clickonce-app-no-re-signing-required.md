---
title: 手动部署 ClickOnce 应用并保留署名
description: 了解如何创建将由客户部署的 ClickOnce 应用程序，而无需生成新的部署清单，并可使用客户署名。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- branding
- preserved branding information
- ClickOnce deployment, manually
- multiple ClickOnce deployment and branding
- ClickOnce deployment, SDK tools
- customer deployments
- manual ClickOnce deployments
- manifests [ClickOnce]
- ClickOnce applications, deployed by others
ms.assetid: c21822fb-d4ee-42e4-b72d-41ee9786efe5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: edcba59250fad70c2b18b35a8a14a3b95c8db251
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671803"
---
# <a name="walkthrough-manually-deploy-a-clickonce-application-that-does-not-require-re-signing-and-that-preserves-branding-information"></a>演练：手动部署不需要重新签名并保留署名信息的 ClickOnce 应用程序
当你创建 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序并将其提供给客户进行发布和部署时，客户通常必须更新部署清单并对其进行重新签名。 虽然这在大多数情况下仍是首选方法，但 .NET Framework 3.5 使你可以创建可由客户部署的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署，而无需重新生成新的部署清单。 有关详细信息，请参阅[在不重新签名的情况下为测试服务器和生产服务器部署 ClickOnce 应用程序](../deployment/deploying-clickonce-applications-for-testing-and-production-without-resigning.md)。

 当你创建 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序，然后将其分配给客户进行发布和部署时，应用程序可以使用客户的署名或保留你自己的署名。 例如，如果应用程序是单个专用应用程序，你可能想要保留你自己的署名。 如果应用程序是针对每个客户高度自定义的，那么你可能希望使用客户署名。 通过 .NET Framework 3.5，你可以在将应用程序提供给组织进行部署时保留你自己的署名、出版商信息和安全签名。 有关详细信息，请参阅[创建供其他人部署的 ClickOnce 应用程序](../deployment/creating-clickonce-applications-for-others-to-deploy.md)。

> [!NOTE]
> 在本演练中，你将使用命令行工具 Mage.exe 或图形工具 MageUI.exe 手动创建部署。 有关手动部署的详细信息，请参阅[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。

## <a name="prerequisites"></a>先决条件
 若要执行本演练中的步骤，需要以下各项：

- 准备部署的 Windows 窗体应用程序。 此应用程序将称为 WindowsFormsApp1。

- Visual Studio 或 Windows SDK。

### <a name="to-deploy-a-clickonce-application-with-multiple-deployment-and-branding-support-using-mageexe"></a>使用 Mage.exe 部署具有多个部署和署名支持的 ClickOnce 应用程序

1. 打开 Visual Studio 命令提示符或 [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] 命令提示符，然后更改到要存储 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 文件的目录。

2. 创建一个以当前部署版本命名的目录。 如果这是你首次部署应用程序，则可能会选择“1.0.0.0”。

   > [!NOTE]
   > 部署版本可能与应用程序版本文件不同。

3. 创建名为 bin 的子目录，并复制此处的所有应用程序文件（包括可执行文件、程序集、资源和数据文件）。

4. 通过调用 Mage.exe 生成应用程序清单。

   ```cmd
   mage -New Application -ToFile 1.0.0.0\WindowsFormsApp1.exe.manifest -Name "Windows Forms App 1" -Version 1.0.0.0 -FromDirectory 1.0.0.0\bin -UseManifestForTrust true -Publisher "A. Datum Corporation"
   ```

5. 使用数字证书对应用程序清单进行签名。

   ```cmd
   mage -Sign WindowsFormsApp1.exe.manifest -CertFile mycert.pfx
   ```

6. 通过调用 Mage.exe 生成部署清单。 默认情况下，Mage.exe 会将 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署标记为已安装的应用程序，以便它可以联机和脱机运行。 若要使应用程序仅在用户联机时可用，请使用值为 `f` 的 `-i` 参数。 由于此应用程序将利用多个部署功能，因此请排除 Mage.exe 的 `-providerUrl` 参数。 （在版本 3.5 之前的 .NET Framework 版本中，排除脱机应用程序的 `-providerUrl` 将导致错误。）

   ```cmd
   mage -New Deployment -ToFile WindowsFormsApp1.application -Name "Windows Forms App 1" -Version 1.0.0.0 -AppManifest 1.0.0.0\WindowsFormsApp1.manifest
   ```

7. 请不要签署部署清单。

8. 将所有文件提供给客户，客户将在其网络上部署应用程序。

9. 此时，客户必须用自己的自行生成证书对部署清单进行签名。 例如，如果客户在一家名为 Adventure Works 的公司工作，则他可以使用 MakeCert.exe 工具生成自签名证书。 接下来，使用 Pvk2pfx.exe 工具将 MakeCert.exe 创建的文件合并到可传递到 Mage.exe 的 PFX 文件中。

    ```cmd
    makecert -r -pe -n "CN=Adventure Works" -sv MyCert.pvk MyCert.cer
    pvk2pfx.exe -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx
    ```

10. 接下来，客户使用此证书对部署清单进行签名。

    ```cmd
    mage -Sign WindowsFormsApp1.application -CertFile MyCert.pfx
    ```

11. 客户向其用户部署应用程序。

### <a name="to-deploy-a-clickonce-application-with-multiple-deployment-and-branding-support-using-mageuiexe"></a>使用 MageUI.exe 部署具有多个部署和署名支持的 ClickOnce 应用程序

1. 打开 Visual Studio 命令提示符或 [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] 命令提示符，然后导航到要存储 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 文件的目录。

2. 创建名为 bin 的子目录，并复制此处的所有应用程序文件（包括可执行文件、程序集、资源和数据文件）。

3. 创建一个以当前部署版本命名的子目录。 如果这是你首次部署应用程序，则可能会选择“1.0.0.0”。

   > [!NOTE]
   > 部署版本可能与应用程序版本文件不同。

4. 将 \\bin 目录移动到步骤 2 中创建的目录中。

5. 启动图形工具 MageUI.exe。

   ```cmd
   MageUI.exe
   ```

6. 从菜单中依次选择“文件”、“新建”、“应用程序清单”，创建新的应用程序清单。

7. 在默认的“名称”选项卡上，输入此部署的名称和版本号。 此外，为 Publisher 提供一个值，该值将用作部署时“开始”菜单中应用程序快捷方式链接的文件夹名称。

8. 选择“应用程序选项”选项卡，然后单击“使用应用程序清单以获取信任信息”。 这将为此 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序启用第三方署名。

9. 选择“文件”选项卡，然后单击“应用程序目录”文本框旁边的“浏览”按钮。

10. 选择包含在步骤 2 中创建的应用程序文件的目录，然后在“文件夹选择”对话框中单击“确定”。

11. 单击“填充”按钮，将所有应用程序文件添加到文件列表中。 如果应用程序包含多个可执行文件，请从“文件类型”下拉列表中选择“入口点”，将此部署的主要可执行文件标记为启动应用程序。 （如果应用程序仅包含一个可执行文件，则 MageUI.exe 会标记该文件。）

12. 选择“所需的权限”选项卡并选择需要应用程序断言的信任级别。 默认值为 Full Trust，适用于大多数应用程序。

13. 从菜单中选择“文件”、“保存”，然后保存应用程序清单。 保存应用程序清单时，系统将提示你对应用程序清单进行签名。

14. 如果将证书作为文件存储在文件系统上，请使用“签署为证书文件”选项，然后使用省略号 (…) 按钮从文件系统中选择证书。

     -或-

     如果证书保存在可从计算机访问的证书存储中，请选择“使用存储的证书签名”选项，然后从提供的列表中选择证书。

15. 从菜单中选择“文件”、“新建”、“部署清单”以创建部署清单，然后在“名称”选项卡上，提供名称和版本号（本例中为 1.0.0.0）。

16. 切换到“更新”选项卡，并指定希望此应用程序更新的频率。 如果应用程序使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署 API 自行检查更新，请清除标记为“此应用程序应检查更新”的复选框。

17. 切换到“应用程序引用”选项卡。你可以通过单击“选择清单”按钮，然后选择在前面步骤中创建的应用程序清单，预先填充此选项卡上的所有值。

18. 选择“保存”，并将部署清单保存到磁盘。 保存应用程序清单时，系统将提示你对应用程序清单进行签名。 单击“取消”可保存清单，而无需对其进行签名。

19. 向客户提供所有应用程序文件。

20. 此时，客户必须用自己的自行生成证书对部署清单进行签名。 例如，如果客户在一家名为 Adventure Works 的公司工作，则他可以使用 MakeCert.exe 工具生成自签名证书。 接下来，使用 Pvk2pfx.exe 工具将 MakeCert.exe 创建的文件合并到可传递到 MageUI.exe 的 PFX 文件中。

    ```cmd
    makecert -r -pe -n "CN=Adventure Works" -sv MyCert.pvk MyCert.cer
    pvk2pfx.exe -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx
    ```

21. 生成证书后，客户现在会通过在 MageUI.exe 中打开部署清单并保存它来签署部署清单。 当出现签名对话框时，客户选择“签署为证书文件”选项，然后选择已保存在磁盘上的 PFX 文件。

22. 客户向其用户部署应用程序。

## <a name="see-also"></a>另请参阅
- [Mage.exe（清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [MageUI.exe（图形化客户端中的清单生成和编辑工具）](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)
- [MakeCert](/windows/desktop/SecCrypto/makecert)
