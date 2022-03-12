---
title: 网络或代理错误的疑难解答
description: 为在防火墙或代理服务器后安装或使用 Visual Studio 时可能会遇到的网络或代理相关错误查找解决方案。
ms.date: 09/16/2020
ms.topic: troubleshooting
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
- list of domains, locations, URLs, Visual Studio
- proxy errors, Visual Studio
ms.assetid: ''
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 533053594a6a185905070070c7b610c2603f6c9b
ms.sourcegitcommit: 596b3ec674f5848fe0711da5ccc23c01b58e508c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2022
ms.locfileid: "139793243"
---
# <a name="troubleshoot-network-related-errors-when-you-install-or-use-visual-studio"></a>安装或使用 Visual Studio 时与网络相关错误的疑难解答

对于你在防火墙或代理服务器后面安装或使用 Visual Studio 时，可能会遇到的最典型的与网络或代理相关的错误，我们已经有了解决方案。

## <a name="error-proxy-authorization-required"></a>错误：“所需的代理身份验证”

当用户通过代理服务器连接到 Internet，而代理服务器阻止 Visual Studio 对某些网络资源进行的调用时，通常会发生此错误。

### <a name="to-fix-this-proxy-error"></a>修复此代理错误

- 重新启动 Visual Studio。 这时会出现一个代理身份验证对话框。 出现提示时，在对话框中输入你的凭据。

- 如果重启 Visual Studio 未能解决问题，这可能是由于你的代理服务器不提示需要提供 http:&#47;&#47;go.microsoft.com 地址的凭据，而是提示需要 &#42;.visualStudio.microsoft.com 地址的凭据。 对于这些服务器，请考虑将以下 URL 添加到允许列表，以取消对 Visual Studio 中所有登录场景的阻止：

  - &#42;.windows.net

  - &#42;.microsoftonline.com

  - &#42;.visualstudio.microsoft.com

  - &#42;.microsoft.com

  - &#42;.live.com

- 否则，可以从允许列表中删除 http:&#47;&#47;go.microsoft.com 地址，以便在重启 Visual Studio 时出现代理身份验证对话框，以提供 http:&#47;&#47;go.microsoft.com 地址和服务器终结点。

  \- 或 -

- 如果你想通过代理使用默认凭据，则可以执行以下操作：

::: moniker range="vs-2017"

  1. 查找 devenv.exe.config（devenv.exe 配置文件），查找位置为：%ProgramFiles%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE 或 %ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE    。

  2. 在配置文件中查找 `<system.net>` 块，然后添加这个代码：

      ```xml
      <defaultProxy enabled="true" useDefaultCredentials="true">
          <proxy bypassonlocal="True" proxyaddress="http://<yourproxy:port#>"/>
      </defaultProxy>
      ```

      你必须在 `proxyaddress="<http://<yourproxy:port#>` 中为你的网络插入正确的代理地址。

     > [!NOTE]
     > 有关详细信息，请参阅[&lt;defaultProxy&gt; 元素（网络设置）](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings/)和 [proxy&lt;&gt; 元素（网络设置）](/dotnet/framework/configure-apps/file-schema/network/proxy-element-network-settings)页。

::: moniker-end

::: moniker range=">=vs-2019"

  1. 查找 devenv.exe.config（devenv.exe 配置文件），查找位置为：%ProgramFiles%\Microsoft Visual Studio\2019\Enterprise\Common7\IDE 或 %ProgramFiles(x86)%\Microsoft Visual Studio\2019\Enterprise\Common7\IDE    。

  2. 在配置文件中查找 `<system.net>` 块，然后添加这个代码：

      ```xml
      <defaultProxy enabled="true" useDefaultCredentials="true">
          <proxy bypassonlocal="True" proxyaddress="http://<yourproxy:port#>"/>
      </defaultProxy>
      ```

      你必须在 `proxyaddress="<http://<yourproxy:port#>` 中为你的网络插入正确的代理地址。

     > [!NOTE]
     > 有关详细信息，请参阅[&lt;defaultProxy&gt; 元素（网络设置）](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings/)和 [proxy&lt;&gt; 元素（网络设置）](/dotnet/framework/configure-apps/file-schema/network/proxy-element-network-settings)页。

::: moniker-end

## <a name="error-disconnected-from-visual-studio-when-attempting-to-report-a-problem"></a>错误：尝试报告问题时发生“与 Visual Studio 的连接断开”错误

当用户通过代理服务器连接到 Internet，而代理服务器阻止 Visual Studio 对某些网络资源进行的调用时，通常会发生此错误。

### <a name="to-fix-this-proxy-error"></a>修复此代理错误

1. 在以下位置查找 feedback.exe.config（feedback.exe 配置文件）：%ProgramFiles(x86)%\Microsoft Visual Studio\Installer 或 %ProgramFiles%\Microsoft Visual Studio\Installer  。

2. 在配置文件中，检查是否存在以下代码：如果不存在，请将其添加到最后的 `</configuration>` 行之前。

   ```xml
   <system.net>
       <defaultProxy useDefaultCredentials="true" />
   </system.net>
   ```

## <a name="error-the-underlying-connection-was-closed"></a>错误：“基础连接已关闭”

如果在有防火墙的专用网络中使用 Visual Studio，则 Visual Studio 可能无法连接到某些网络资源。 这些资源可能会包括用于登录和授权的 Azure DevOps Services、NuGet 和 Azure 服务。 如果 Visual Studio 无法连接到上述某个资源，则可能出现以下错误消息：

  **基础连接已关闭：发送时出现意外错误**

Visual Studio 使用传输层安全性 (TLS) 1.2 协议连接到网络资源。 Visual Studio 使用 TLS 1.2 时，某些专用网络上的安全设备会阻止某些服务器连接。

### <a name="to-fix-this-connection-error"></a>修复此连接错误

对以下 URL 启用连接：

- https:&#47;&#47;management.core.windows.net

- https:&#47;&#47;app.vssps.visualstudio.com

- https:&#47;&#47;login.microsoftonline.com

- https:&#47;&#47;login.live.com

- https:&#47;&#47;go.microsoft.com

- https:&#47;&#47;graph.windows.net

- https:&#47;&#47;app.vsspsext.visualstudio.com

- &#42;.azurewebsites.net（用于 Azure 连接）

- &#42;.visualstudio.microsoft.com

- cdn.vsassets.io（主机内容分发网络或 CDN、内容）

- &#42;.gallerycdn.vsassets.io（托管 Azure DevOps Services 扩展）

- static2.sharepointonline.com（Visual Studio 在字体等 Office UI Fabric 工具包中使用的主机资源）

- &#42;.nuget.org（用于 NuGet 连接）

  > [!NOTE]
  > 此列表可能未包含私人拥有的 NuGet 服务器 URL。 你可以检查在 %APPData%\Nuget\NuGet.Config 中使用的 NuGet 服务器。

## <a name="error-failed-to-parse-id-from-parent-process"></a>错误：“无法从父进程分析 ID”

在网络驱动器上使用 Visual Studio 引导程序和 response.json 文件时，可能会遇到此错误消息。 错误的来源是 Windows 中的用户帐户控制 (UAC)。

下面是可能出现此错误的原因：映射的网络驱动器或 [UNC](/dotnet/standard/io/file-path-formats#unc-paths) 共享已链接到用户的访问令牌。 启用 UAC 后，将创建两个用户[访问令牌](/windows/win32/secauthz/access-tokens)：一个具有管理员访问权限，另一个不具有管理员访问权限 。 创建网络驱动器或共享后，用户的当前访问令牌会链接到它们。 因为必须以管理员身份运行引导程序，所以如果驱动器或共享未链接到具有管理员访问权限的用户访问令牌，则无法访问网络驱动器或共享。

### <a name="to-fix-this-error"></a>修复此错误的方法

可以使用 `net use` 命令，也可以更改 UAC 组策略设置。 有关这些解决方法以及如何实现它们的详细信息，请参阅以下 Microsoft 支持文章：

* [在 Windows 中将 UAC 配置为“提示输入凭据”时，在权限提升的提示符下无法获取映射的驱动器](https://support.microsoft.com/help/3035277/mapped-drives-are-not-available-from-an-elevated-prompt-when-uac-is-co)
* [在 Windows 操作系统中打开用户帐户控制后，程序可能无法访问某些网络位置](https://support.microsoft.com/en-us/help/937624/programs-may-be-unable-to-access-some-network-locations-after-you-turn)

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>另请参阅

* [在防火墙或代理服务器后面安装和使用 Visual Studio](install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)
* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
* [安装 Visual Studio](install-visual-studio.md)
