---
title: 手动部署ClickOnce应用&保持品牌
description: 了解如何创建ClickOnce部署的应用程序，而无需生成新的部署清单，并且可以使用客户品牌。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122073729"
---
# <a name="walkthrough-manually-deploy-a-clickonce-application-that-does-not-require-re-signing-and-that-preserves-branding-information"></a>演练：手动部署ClickOnce签名且保留品牌信息的应用程序
创建应用程序，然后将其授予客户进行发布和部署时，客户传统上必须更新部署清单并 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 重新签名。 虽然在大多数情况下，这仍是首选方法，但 .NET Framework 3.5 使你能够创建客户可以部署的部署，而无需 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 重新生成新的部署清单。 有关详细信息，请参阅[在不ClickOnce的情况下为测试和生产服务器部署应用程序](../deployment/deploying-clickonce-applications-for-testing-and-production-without-resigning.md)。

 创建一个应用程序，然后将其授予客户进行发布和部署时，该应用程序可以使用客户的品牌，也可以 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 保留你的品牌。 例如，如果应用程序是单个专有应用程序，可能需要保留品牌。 如果应用程序是高度自定义的，则你可能想要使用客户的品牌。 使用 .NET Framework 3.5，可以在向组织提供要部署的应用程序时保留品牌、发布者信息和安全签名。 有关详细信息，请参阅[创建ClickOnce应用程序供其他人部署](../deployment/creating-clickonce-applications-for-others-to-deploy.md)。

> [!NOTE]
> 在此演练中，你将使用命令行工具或图形工具或Mage.exe手动 *创建MageUI.exe。*  有关手动部署的信息，请参阅[演练：手动](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)部署ClickOnce应用程序。

## <a name="prerequisites"></a>必备条件
 若要执行本演练中的步骤，需要以下各项：

- 一Windows准备部署的窗体应用程序。 此应用程序将称为 *WindowsFormsApp1。*

- Visual Studio或 Windows SDK。

### <a name="to-deploy-a-clickonce-application-with-multiple-deployment-and-branding-support-using-mageexe"></a>使用 ClickOnce 部署具有多个部署和品牌支持的 Mage.exe

1. 打开Visual Studio命令提示符或命令提示符，并更改为要存储文件的 [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 目录。

2. 创建以当前部署版本命名的目录。 如果这是首次部署应用程序，可能会选择 **1.0.0.0。**

   > [!NOTE]
   > 部署版本可能不同于应用程序文件的版本。

3. 创建名为 **bin** 的子目录，并在此处复制所有应用程序文件，包括可执行文件、程序集、资源和数据文件。

4. 通过调用应用程序清单来生成Mage.exe。

   ```cmd
   mage -New Application -ToFile 1.0.0.0\WindowsFormsApp1.exe.manifest -Name "Windows Forms App 1" -Version 1.0.0.0 -FromDirectory 1.0.0.0\bin -UseManifestForTrust true -Publisher "A. Datum Corporation"
   ```

5. 使用数字证书对应用程序清单进行签名。

   ```cmd
   mage -Sign WindowsFormsApp1.exe.manifest -CertFile mycert.pfx
   ```

6. 通过调用 生成部署 *清单Mage.exe。* 默认情况下 *，Mage.exe* 将部署标记为已安装的应用程序， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 以便它可以联机和脱机运行。 若要使应用程序仅在用户联机时可用，请使用 值为 `-i` 的 参数 `f` 。 由于此应用程序将利用多个部署功能，因此请从 中排除 `-providerUrl` *Mage.exe。*  (在版本 3.5 .NET Framework版本之前的版本中，排除脱机应用程序将导致 `-providerUrl` 错误。) 

   ```cmd
   mage -New Deployment -ToFile WindowsFormsApp1.application -Name "Windows Forms App 1" -Version 1.0.0.0 -AppManifest 1.0.0.0\WindowsFormsApp1.manifest
   ```

7. 不要对部署清单进行签名。

8. 将应用程序部署到其网络的客户提供所有文件。

9. 此时，客户必须使用自己的自生成证书对部署清单进行签名。 例如，如果客户为名为 Adventure Works 的公司工作，则他可以使用MakeCert.exe生成 *自签名* 证书。 接下来，使用 *Pvk2pfx.exe* 工具将MakeCert.exe创建的文件合并到可以传递给Mage.exe的 PFX *文件中*。

    ```cmd
    makecert -r -pe -n "CN=Adventure Works" -sv MyCert.pvk MyCert.cer
    pvk2pfx.exe -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx
    ```

10. 客户接下来使用此证书对部署清单进行签名。

    ```cmd
    mage -Sign WindowsFormsApp1.application -CertFile MyCert.pfx
    ```

11. 客户将应用程序部署到其用户。

### <a name="to-deploy-a-clickonce-application-with-multiple-deployment-and-branding-support-using-mageuiexe"></a>使用 ClickOnce 部署具有多个部署和品牌支持的 MageUI.exe

1. 打开Visual Studio命令提示符或命令提示符，并导航到要存储文件的 [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 目录。

2. 创建名为 **bin** 的子目录，并在此处复制所有应用程序文件，包括可执行文件、程序集、资源和数据文件。

3. 创建以当前部署版本命名的子目录。 如果这是首次部署应用程序，可能会选择 **1.0.0.0。**

   > [!NOTE]
   > 部署版本可能不同于应用程序文件的版本。

4. 将 \\ **bin** 目录移动到在步骤 2 中创建的目录中。

5. 启动图形工具 *MageUI.exe。*

   ```cmd
   MageUI.exe
   ```

6. 通过从菜单中选择"文件"、"**新建"和****"应用程序清单"来** 创建新的应用程序清单。 

7. 在默认" **名称"** 选项卡上，输入此部署的名称和版本号。 此外，为 Publisher **，该值** 将用作应用程序在部署时"开始"菜单快捷方式链接的文件夹名称。

8. 选择"**应用程序选项"** 选项卡，然后单击 **"将应用程序清单用于信任信息"。** 这将为此应用程序启用第三方 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 品牌。

9. 选择" **文件"** 选项卡 **，然后单击"** 应用程序目录"文本框 **旁边的"浏览"** 按钮。

10. 选择包含在步骤 2 中创建的应用程序文件的目录，然后单击文件夹选择对话框中的"确定"。

11. 单击" **填充** "按钮，将所有应用程序文件添加到文件列表。 如果应用程序包含多个可执行文件，请从"文件类型"下拉列表中选择"入口点"，将此部署的主要可执行文件标记为启动应用程序。   (如果应用程序仅包含一个可执行 *文件，MageUI.exe* 会将其标记为) 

12. 选择 **"所需权限"** 选项卡，然后选择应用程序需要断言的信任级别。 默认值为 **"完全信任**"，这适用于大多数应用程序。

13. 从 **菜单中** 选择 **"文件"，"** 保存"，然后保存应用程序清单。 保存时，系统会提示对应用程序清单进行签名。

14. 如果证书存储为文件系统中的文件，请使用"签名为证书文件"选项，然后使用省略号"..."按钮从文件系统 (**证书)** 证书。

     -或-

     如果证书保存在可以从计算机访问的证书存储中，请选择"使用存储 **的** 证书签名"选项，然后从提供的列表中选择该证书。

15. 从 **菜单中** 选择 **"** 文件"、"新建"和"部署清单"以创建部署清单，然后在"名称"选项卡上，提供名称和版本号 (**1.0.0.0（** 此示例中为) ）。

16. 切换到" **更新"** 选项卡，并指定希望此应用程序更新多久一次。 如果应用程序使用部署 API 来检查更新本身，请清除标记为" [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] **此应用程序应检查更新"的复选框**。

17. 切换到"应用程序 **引用"** 选项卡。可以预填充此选项卡上的所有值，方法是单击"选择清单"按钮，然后选择在先前步骤中创建的应用程序清单。

18. 选择 **"保存** "，将部署清单保存到磁盘。 保存时，系统会提示对应用程序清单进行签名。 单击 **"** 取消"以保存清单而不对清单进行签名。

19. 为客户提供所有应用程序文件。

20. 此时，客户必须使用自己的自生成证书对部署清单进行签名。 例如，如果客户为名为 Adventure Works 的公司工作，则他可以使用MakeCert.exe生成 *自签名* 证书。 接下来，使用 *Pvk2pfx.exe* 工具将MakeCert.exe创建的文件合并到可以传递给MageUI.exe的 PFX *文件中*。

    ```cmd
    makecert -r -pe -n "CN=Adventure Works" -sv MyCert.pvk MyCert.cer
    pvk2pfx.exe -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx
    ```

21. 生成证书后，客户现在通过打开中的部署清单来签署部署清单 *MageUI.exe，然后* 保存它。 出现签名对话框时，客户选择"签名 **为** 证书文件"选项，然后选择他保存在磁盘上的 PFX 文件。

22. 客户将应用程序部署到其用户。

## <a name="see-also"></a>请参阅
- [Mage.exe（清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [MageUI.exe（图形化客户端中的清单生成和编辑工具）](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)
- [MakeCert](/windows/desktop/SecCrypto/makecert)
