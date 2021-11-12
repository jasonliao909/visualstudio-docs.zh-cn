---
title: 配置 ClickOnce 信任提示行为 | Microsoft Docs
description: 了解如何配置 ClickOnce 信任提示，以控制终端用户是否可以选择安装 ClickOnce 应用程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, install without prompting
- deploying applications [ClickOnce], trust prompt
- ClickOnce applications, install without prompting
- ClickOnce applications, trust prompt
- ClickOnce deployment, trust prompt
ms.assetid: cc04fa75-012b-47c9-9347-f4216be23cf2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 13c408cb4a95daba3676275ffceb032d3a772fbc
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665614"
---
# <a name="how-to-configure-the-clickonce-trust-prompt-behavior"></a>如何：配置 ClickOnce 信任提示行为
可以配置 ClickOnce 信任提示，以控制终端用户是否可以选择安装 ClickOnce 应用程序，例如 Windows 窗体应用程序、Windows Presentation Foundation 应用程序、控制台应用程序、WPF 浏览器应用程序以及 Office 解决方案。 通过在每个最终用户的计算机上设置注册表项来配置信任提示。

 下表显示了可应用于这五个区域（Internet、UntrustedSites、MyComputer、LocalIntranet 和 TrustedSites）的每个区域的配置选项。

|选项|注册表设置值|说明|
|------------|----------------------------|-----------------|
|启用信任提示。|`Enabled`|将显示 ClickOnce 信任提示，以便最终用户可授予对 ClickOnce 应用程序的信任。|
|限制信任提示。|`AuthenticodeRequired`|只有当使用标识发布者的证书为 ClickOnce 应用程序签名时，才会显示 ClickOnce 信任提示。|
|禁用信任提示。|`Disabled`|对于没有使用显式受信任证书签名的任何 ClickOnce 应用程序，都不会显示 ClickOnce信任提示。|

 下表显示了每个区域的默认行为。 “应用程序”列是指 Windows 窗体应用程序、Windows Presentation Foundation 应用程序、WPF 浏览器应用程序和控制台应用程序。

|区域|应用程序|Office 解决方案|
|----------|------------------|----------------------|
|`MyComputer`|`Enabled`|`Enabled`|
|`LocalIntranet`|`Enabled`|`Enabled`|
|`TrustedSites`|`Enabled`|`Enabled`|
|`Internet`|`Enabled`|`AuthenticodeRequired`|
|`UntrustedSites`|`Disabled`|`Disabled`|

 可通过启用、限制或禁用 ClickOnce 信任提示来替代这些设置。

## <a name="enable-the-clickonce-trust-prompt"></a>启用 ClickOnce 信任提示
 当想向最终用户显示安装和运行来自该区域的任何 ClickOnce 应用程序时，请为区域启用信任提示。

#### <a name="to-enable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>使用注册表编辑器启用 ClickOnce 信任提示

1. 打开注册表编辑器：

    1. 单击 **“启动”** ，再单击 **“运行”** 。

    2. 在“打开”框中键入 `regedit`，然后单击“确定” 。

2. 查找以下注册表项：

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     如果不存在此项，则创建它。

3. 如果以下子项已不存在，则将它们添加为“字符串值”，其关联值如下表所示。

    |字符串值子项|值|
    |-------------------------|-----------|
    |`Internet`|`Enabled`|
    |`UntrustedSites`|`Disabled`|
    |`MyComputer`|`Enabled`|
    |`LocalIntranet`|`Enabled`|
    |`TrustedSites`|`Enabled`|

     对于Office 解决方案，`Internet` 具有默认值 `AuthenticodeRequired`，而 `UntrustedSites` 具有默认值 `Disabled`。 对于所有其他解决方案，`Internet` 具有默认值 `Enabled`。

#### <a name="to-enable-the-clickonce-trust-prompt-programmatically"></a>以编程的方式启用 ClickOnce 信任提示

1. 在 Visual Studio 中创建 Visual Basic 或 Visual C# 控制台应用程序。

2. 打开“Program.vb”或“Program.cs”文件以编辑并添加以下代码 。

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "Enabled")
    key.SetValue("LocalIntranet", "Enabled")
    key.SetValue("Internet", "Enabled")
    key.SetValue("TrustedSites", "Enabled")
    key.SetValue("UntrustedSites", "Disabled")
    key.Close()
    ```

    ```csharp
    Microsoft.Win32.RegistryKey key;
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\\MICROSOFT\\.NETFramework\\Security\\TrustManager\\PromptingLevel");
    key.SetValue("MyComputer", "Enabled");
    key.SetValue("LocalIntranet", "Enabled");
    key.SetValue("Internet", "AuthenticodeRequired");
    key.SetValue("TrustedSites", "Enabled");
    key.SetValue("UntrustedSites", "Disabled");
    key.Close();
    ```

3. 生成并运行应用程序。

## <a name="restrict-the-clickonce-trust-prompt"></a>限制 ClickOnce 信任提示
 限制信任提示，确保在提示用户做出信任决策前必须使用具有已知标识的验证码证书对解决方案进行签名。

#### <a name="to-restrict-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>使用注册表编辑器限制 ClickOnce 信任提示

1. 打开注册表编辑器：

    1. 单击 **“启动”** ，再单击 **“运行”** 。

    2. 在“打开”框中键入 `regedit`，然后单击“确定” 。

2. 查找以下注册表项：

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     如果不存在此项，则创建它。

3. 如果以下子项已不存在，则将它们添加为“字符串值”，其关联值如下表所示。

    |字符串值子项|值|
    |-------------------------|-----------|
    |`UntrustedSites`|`Disabled`|
    |`Internet`|`AuthenticodeRequired`|
    |`MyComputer`|`AuthenticodeRequired`|
    |`LocalIntranet`|`AuthenticodeRequired`|
    |`TrustedSites`|`AuthenticodeRequired`|

#### <a name="to-restrict-the-clickonce-trust-prompt-programmatically"></a>以编程的方式限制 ClickOnce 信任提示

1. 在 Visual Studio 中创建 Visual Basic 或 Visual C# 控制台应用程序。

2. 打开“Program.vb”或“Program.cs”文件以编辑并添加以下代码 。

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "AuthenticodeRequired")
    key.SetValue("LocalIntranet", "AuthenticodeRequired")
    key.SetValue("Internet", "AuthenticodeRequired")
    key.SetValue("TrustedSites", "AuthenticodeRequired")
    key.SetValue("UntrustedSites", "Disabled")
    key.Close()
    ```

    ```csharp
    Microsoft.Win32.RegistryKey key;
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\\MICROSOFT\\.NETFramework\\Security\\TrustManager\\PromptingLevel");
    key.SetValue("MyComputer", "AuthenticodeRequired");
    key.SetValue("LocalIntranet", "AuthenticodeRequired");
    key.SetValue("Internet", "AuthenticodeRequired");
    key.SetValue("TrustedSites", "AuthenticodeRequired");
    key.SetValue("UntrustedSites", "Disabled");
    key.Close();
    ```

3. 生成并运行应用程序。

## <a name="disable-the-clickonce-trust-prompt"></a>禁用 ClickOnce 信任提示
 可以禁用信任提示，使最终用户不能选择安装其安全策略中尚未受信任的解决方案。

#### <a name="to-disable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>使用注册表编辑器禁用 ClickOnce 信任提示

1. 打开注册表编辑器：

    1. 单击 **“启动”** ，再单击 **“运行”** 。

    2. 在“打开”框中键入 `regedit`，然后单击“确定” 。

2. 查找以下注册表项：

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     如果不存在此项，则创建它。

3. 如果以下子项已不存在，则将它们添加为“字符串值”，其关联值如下表所示。

    |字符串值子项|值|
    |-------------------------|-----------|
    |`UntrustedSites`|`Disabled`|
    |`Internet`|`Disabled`|
    |`MyComputer`|`Disabled`|
    |`LocalIntranet`|`Disabled`|
    |`TrustedSites`|`Disabled`|

#### <a name="to-disable-the-clickonce-trust-prompt-programmatically"></a>以编程的方式禁用 ClickOnce 信任提示

1. 在 Visual Studio 中创建 Visual Basic 或 Visual C# 控制台应用程序。

2. 打开“Program.vb”或“Program.cs”文件以编辑并添加以下代码 。

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "Disabled")
    key.SetValue("LocalIntranet", "Disabled")
    key.SetValue("Internet", "Disabled")
    key.SetValue("TrustedSites", "Disabled")
    key.SetValue("UntrustedSites", "Disabled")
    key.Close()
    ```

    ```csharp
    Microsoft.Win32.RegistryKey key;
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\\MICROSOFT\\.NETFramework\\Security\\TrustManager\\PromptingLevel");
    key.SetValue("MyComputer", "Disabled");
    key.SetValue("LocalIntranet", "Disabled");
    key.SetValue("Internet", "Disabled");
    key.SetValue("TrustedSites", "Disabled");
    key.SetValue("UntrustedSites", "Disabled");
    key.Close();

    ```

3. 生成并运行应用程序。

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
- [如何：为应用程序和部署清单重新签名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)
