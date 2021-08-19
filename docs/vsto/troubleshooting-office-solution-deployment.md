---
title: 解决方案Office疑难解答
description: 了解如何解决在部署解决方案时可能会遇到的Office问题。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: troubleshooting
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ClickOnce deployment [Office development in Visual Studio], troubleshooting
- Office development in Visual Studio, troubleshooting
- deploying applications [Office development in Visual Studio], troubleshooting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 04b743d6d2a258bb117b01bc9f7d27bc7f4b7978
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122147747"
---
# <a name="troubleshoot-office-solution-deployment"></a>解决方案Office疑难解答
  本主题包含有关如何解决在部署 Office 解决方案时可能遇到的常见问题的信息。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="troubleshoot-office-solutions-by-using-the-event-viewer"></a>使用Office对解决方案进行故障排除
 你可以使用 Windows 事件查看器来查看当你安装或卸载 Office 解决方案时，由 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 捕捉到的错误消息。 你可使用事件记录器中的这些消息来解决安装和部署问题。 有关详细信息，请参阅事件[日志记录Office解决方案](../vsto/event-logging-for-office-solutions.md)。

## <a name="change-the-assembly-name-causes-conflicts"></a>更改程序集名称会导致冲突
 如果在部署解决方案后更改 **Project Designer** 的"应用程序"页中的"程序集名称"值，则发布工具将修改安装程序包，以包含一个Setup.exe文件和两个 *部署* 清单。  如果部署两个清单文件，则可能会出现以下条件：

- 如果最终用户同时安装这两个版本，则应用程序会同时加载这两个 VSTO 外接程序。

- 如果在更改程序集名称之前安装了 VSTO 外接程序，则最终用户从不会收到更新。

  若要避免这些情况，请不要在部署解决方案后更改解决方案的"程序集名称"值。

## <a name="check-for-updates-takes-a-long-time"></a>检查更新需要很长时间
 Visual Studio 2010 Tools for Office Runtime 提供了一个注册表项，管理员可以使用该注册表项设置下载清单和解决方案的超时值。

#### <a name="to-set-the-time-out-value"></a>设置超时值

1. 在注册表中，导航到以下项：

     **HKEY_CURRENT_USER\Software\Microsoft\VSTA**

2. 在 **AddInTimeout** 子项中，以毫秒为单位设置超时值。

     如果 **AddInTimeout** 子项不存在，请以 DWORD 的形式创建它。

## <a name="cant-update-or-publish-to-a-network-file-share"></a>无法更新或发布到网络文件共享
 Office发布更新时，如果解决方案的Setup.exe文件在进程中锁定，则网络文件共享上的解决方案可能在更新期间显示误导性消息。 该消息可能会显示以下内容：“无法将‘setup.exe’添加到 Web。 此 Web 中已存在文件‘setup.exe’。”

 要帮助防止文件锁定，可以将此共享设为对最终用户只读。 但是，如果文档处于共享上，则它们也会对最终用户只读。

## <a name="prerequisites-for-microsoft-office-arent-installed"></a>未安装Microsoft Office的先决条件
 可以将 .NET Framework、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]和 Office 主互操作程序集作为随 Office 解决方案部署的先决条件添加到安装程序包中。 若要了解如何安装主互操作程序集，请参阅配置计算机以[开发](../vsto/configuring-a-computer-to-develop-office-solutions.md)Office 解决方案和[如何：安装Office互操作程序集](../vsto/how-to-install-office-primary-interop-assemblies.md)。

## <a name="publish-using-localhost-can-cause-installation-problems"></a>使用 Localhost 发布可能会导致安装问题
 使用 作为文档级解决方案的发布或安装位置时，发布向导不会将 `http://localhost` 字符串转换为实际计算机名称。  在这种情况下，必须在开发计算机上安装解决方案。 要使部署的解决方案在开发计算机上使用 IIS，请对所有 HTTP/HTTPS/FTP 位置使用完全限定的名称，而不是 localhost。

## <a name="cached-assemblies-are-loaded-instead-of-updated-assemblies"></a>加载缓存的程序集，而不是更新的程序集
 当项目输出路径位于网络文件共享上、程序集使用强名称进行签名以及自定义项的程序集版本未更改时，Fusion（.NET Framework 程序集加载程序）会加载程序集的缓存副本。 如果更新的程序集符合这些条件，则更新不会在下次运行项目时出现，因为会加载缓存副本。

 可以配置 Visual Studio，以便 Fusion 在每次运行项目时下载程序集。

### <a name="to-download-assemblies-instead-of-loading-cached-copies"></a>下载程序集而不是加载缓存副本

1. 在菜单栏上，选择"Project，"_项目名称属性_**"。**

2. 在“应用程序”  页上，选择“程序集信息” 。

3. 将"程序集版本"的修订号（第三个字段）设置为通配符 \* () 。 例如，"1.0.*"。  然后选择"确定 **"** 按钮。

   更改程序集版本之后，可以继续使用强名称对程序集进行签名，Fusion 会加载自定义项的最新版本。

 [!NOTE]
> 从 Visual Studio 2017 开始，如果尝试在程序集版本中使用通配符，则会发生生成错误。  这是因为程序集版本中的通配符将中断MSBuild确定性功能。 将指示从程序集版本中删除通配符，或禁用确定性。  若要详细了解确定性功能，请参阅：常见MSBuild[属性和](../msbuild/common-msbuild-project-properties.md)[自定义生成](../msbuild/customize-your-build.md)

## <a name="installation-fails-when-the-uri-has-characters-that-arent-us-ascii"></a>当 URI 包含非 US-ASCII 的字符时，安装失败
 将 Office 解决方案发布到 HTTP/HTTPS/FTP 位置时，路径不能包含不属于 US-ASCII 的任何 Unicode 字符。 这类字符会导致安装程序中出现不一致的行为。 请对安装路径使用 US-ASCII 字符。

## <a name="prompt-to-manually-uninstall-appears-when-you-publish-and-install-a-solution-on-the-development-computer"></a>在开发计算机上发布和安装解决方案时，会显示手动卸载提示
 生成 Office 解决方案时，会自动注册生成的版本。 如果以前已将相同解决方案发布并安装到开发计算机，则在下一次生成、重新生成或发布解决方案之后， [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 会检测到已发布版本和生成版本的安装路径不同。 错误消息显示“由于当前已安装另一个版本的自定义项且无法从该位置升级，无法安装该自定义项。” 只要重新生成解决方案，便会更新注册表项。 因此，必须在发布、调试或运行新版本之前卸载以前的版本。

 要防止出现该消息，请在开发计算机上创建另一个用户帐户以测试部署。 作为替代方法，可以在下次发布、调试或重新生成解决方案之前，从计算机上的已安装程序列表中卸载该版本。

## <a name="uncaught-exception-or-method-not-found-error-when-you-install-a-solution"></a>安装解决方案时出现未捕获的异常或找不到方法错误
 通过打开 *.vsto* (文件) 、Office 应用程序、文档或工作簿的部署清单来安装 Office 解决方案时，可能会出现以下条件的错误消息：

- 找不到方法。

- MissingMethodException。

- 未捕获的异常。

  要防止出现这些错误消息，请通过运行安装程序来安装解决方案。

  在不运行安装程序的情况下安装解决方案时，安装程序不会检查或安装先决条件。 安装程序会检查是否存在正确版本的先决条件并根据需要安装它们。

## <a name="manifest-registry-keys-for-add-ins-change-after-an-installshield-limited-edition-project-is-built"></a>生成 InstallShield Limited Edition 项目后，外接程序的清单注册表项会更改
 生成 InstallShield Limited Edition 项目时，VSTO外接程序安装程序的清单注册表项有时会从 *.vsto* 更改到 *.dll.manifest。*

 要解决此问题，请在另一个解决方案中创建 InstallShield Limited Edition 项目，或使用 CompanyName.AddinName 作为包含 VSTO 外接程序名称的注册表项的值。

## <a name="the-clickonce-installer-for-your-office-solution-doesnt-install-the-primary-interop-assemblies"></a>ClickOnce解决方案Office安装程序不会安装主互操作程序集
 运行 ClickOnce 为 Office 解决方案创建的安装程序时，Office 主互操作程序集 (PIA) 的安装程序仅当尚未安装任何 PIA 时才会运行。

 如果安装程序未正确安装 PIA，请通过从安装目录运行名为o2007pia.msi安装程序文件来手动安装它们。 

## <a name="reinstall-office-solutions-causes-an-argument-out-of-range-exception"></a>重新安装Office导致参数范围外异常
 重新安装 Office 解决方案时， <xref:System.ArgumentOutOfRangeException> 异常可能会出现，并显示以下错误消息：指定的参数已超出有效值的范围。

 如果安装位置 URL 的大小写不同，则会出现这种情况。 例如，如果第一次安装 Office，然后第二次使用，则 `http://fabrikam.com/ExcelSolution.vsto` 会出现 `http://fabrikam.com/excelsolution.vsto` 此错误。

 要防止出现该消息，请在安装 Office 解决方案时使用相同的大小写。

## <a name="cant-install-a-clickonce-solution-by-opening-the-deployment-manifest-from-the-web"></a>无法通过从 web ClickOnce部署清单来安装部署解决方案
 用户可以通过从 Web 打开部署清单来安装 Office 解决方案。 但是，某些 IIS Internet Information Services (安装) *阻止 .vsto* 文件扩展名。 必须先在 IIS 中定义 MIME 类型，然后才能使用它来部署Office解决方案。

 若要了解如何在 IIS 7 中定义 MIME 类型，请参阅[在 IIS7 (MIME) 。 ](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc725608(v=ws.10))

 将扩展名设置为 **.vsto** ，并将 MIME 类型设置为 **application/x-ms-vsto**。

## <a name="see-also"></a>请参阅

- [ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
- [Visual Studio 故障排除](/troubleshoot/visualstudio/welcome-visual-studio/)