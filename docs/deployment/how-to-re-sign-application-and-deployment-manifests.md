---
title: 对应用程序和部署清单重新签名 | Microsoft Docs
description: 了解在更改部署属性后，如何使用证书对应用程序清单和部署清单进行重新签名。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Office applications, signing manifests
- deploying applications [ClickOnce], signing manifests
- deploying applications, signing manifests
- ClickOnce deployment, signing manifests
- Office development in Visual Studio, signing manifests
ms.assetid: d53bceb9-4d3b-4c22-b909-8f370e7231fb
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 9eccc8cb2e56a227548102d1aa342d9399a489bd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671813"
---
# <a name="how-to-re-sign-application-and-deployment-manifests"></a>如何：为应用程序和部署清单重新签名
更改 Windows 窗体应用程序、Windows Presentation Foundation 应用程序 (xbap) 或 Office 解决方案的应用程序清单中的部署属性后，必须使用证书对应用程序清单和部署清单进行重新签名。 此过程有助于确保不会在最终用户计算机上安装经过篡改的文件。

 可能需要对清单重新签名的另一种情况是当客户希望使用他们自己的证书对应用程序和部署清单签名时。

## <a name="re-sign-the-application-and-deployment-manifests"></a>对应用程序清单和部署清单重新签名
 此过程假定你已对应用程序清单文件 (.manifest) 进行了更改。 有关详细信息，请参阅[如何：更改部署属性](/previous-versions/cc442869(v=vs.110))。

#### <a name="to-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>使用 Mage.exe 对应用程序清单和部署清单进行重新签名

1. 打开“Visual Studio 命令提示符”窗口。

2. 将目录更改为包含要签名的清单文件的文件夹。

3. 键入以下命令，对应用程序清单文件进行签名。 将 ManifestFileName 替换为你的清单文件的名称，加上扩展名。 将 Certificate 替换为证书文件的相对路径或完全限定的路径，并将 Password 替换为证书的密码 。

    ```cmd
    mage -sign ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     例如，可以运行以下命令对加载项、Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序的应用程序清单进行签名。 不建议将 Visual Studio 创建的临时证书部署到生产环境中。

    ```cmd
    mage -sign WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -sign ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -sign WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

4. 键入以下命令以更新部署清单文件并对其签名，如前一步骤所示替换占位符名称。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     例如，可以运行以下命令对 Excel 加载项、Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序的部署清单进行更新和签名。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. （可选）将主部署清单 (*publish\\\<appname>.application*) 复制到版本部署目录 (*publish\Application Files\\\<appname>_\<version>* )。

## <a name="update-and-re-sign-the-application-and-deployment-manifests"></a>对应用程序清单和部署清单进行更新和重新签名
 此过程假定你已对应用程序清单文件 (.manifest) 进行了更改，但还有其他文件已更新。 更新文件时，还必须更新表示该文件的哈希。

#### <a name="to-update-and-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>使用 Mage.exe 对应用程序清单和部署清单进行更新和重新签名

1. 打开“Visual Studio 命令提示符”窗口。

2. 将目录更改为包含要签名的清单文件的文件夹。

3. 从发布输出文件夹的文件中删除 .deploy 文件扩展名。

4. 键入以下命令，使用更新的文件的新哈希更新应用程序清单，并对应用程序清单文件进行签名。 将 ManifestFileName 替换为你的清单文件的名称，加上扩展名。 将 Certificate 替换为证书文件的相对路径或完全限定的路径，并将 Password 替换为证书的密码 。

    ```cmd
    mage -update ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     例如，可以运行以下命令对加载项、Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序的应用程序清单进行签名。 不建议将 Visual Studio 创建的临时证书部署到生产环境中。

    ```cmd
    mage -update WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. 键入以下命令以更新部署清单文件并对其签名，如前一步骤所示替换占位符名称。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     例如，可以运行以下命令对 Excel 加载项、Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序的部署清单进行更新和签名。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

6. 将 .deploy 文件扩展名添加回文件（应用程序和部署清单文件除外）。

7. （可选）将主部署清单 (*publish\\\<appname>.application*) 复制到版本部署目录 (*publish\Application Files\\\<appname>_\<version>* )。

## <a name="see-also"></a>另请参阅
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce 和 Authenticode](../deployment/clickonce-and-authenticode.md)
- [受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)
- [如何：启用 ClickOnce 安全设置](../deployment/how-to-enable-clickonce-security-settings.md)
- [如何：为 ClickOnce 应用程序设置安全区域](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [如何：设置 ClickOnce 应用程序的自定义权限](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [如何：使用受限权限对 ClickOnce 应用程序进行调试](securing-clickonce-applications.md)
- [如何：为 ClickOnce 应用程序向客户端计算机添加一个受信任的发行者](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [如何：配置 ClickOnce 信任提示行为](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)