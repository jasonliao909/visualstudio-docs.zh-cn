---
title: 如何：配置包含列表安全性
description: 配置ClickOnce信任提示，以控制是否向最终用户提供安装 Office 解决方案的选项，只需将信任决策保存到包含列表。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- permissions [Office development in Visual Studio
- inclusion lists [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: adde40770aad2d665ad482b72189abda2d6d4176
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122148176"
---
# <a name="how-to-configure-inclusion-list-security"></a>如何：配置包含列表安全性
  如果具有管理员权限，可以配置信任提示，以控制是否向最终用户提供安装 Office 解决方案的选项，只需将信任决策保存到 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 包含列表。 有关包含列表的信息，请参阅使用[包含Office信任解决方案](../vsto/trusting-office-solutions-by-using-inclusion-lists.md)。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 对于五个区域中每个区域的解决方案，可以设置以下选项：

- 启用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] "信任提示密钥"和包含列表。 可以允许最终用户向使用任何证书Office的解决方案授予信任。

- 限制 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 信任提示密钥和包含列表。 可以允许最终用户安装Office证书签名但尚未受信任的证书的解决方案。

- 禁用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 信任提示键和包含列表。 可以阻止最终用户安装任何未Office显式受信任的证书进行签名的解决方案。

## <a name="enable-the-inclusion-list"></a>启用包含列表
 当希望向最终用户显示安装和运行来自该区域的任何 Office解决方案的选项时，请启用区域包含列表。

### <a name="to-enable-the-inclusion-list-by-using-the-registry-editor"></a>使用注册表编辑器启用包含列表

1. 打开注册表编辑器：

    1. 单击 **“启动”** ，再单击 **“运行”** 。

    2. 在"**打开"** 框中 **，regedt32.exe**，然后单击"确定 **"。**

2. 查找以下注册表项：

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     如果密钥不存在，请创建它。

3. 将以下子项添加为 **字符串值**（如果它们不存在）以及关联的值。

    |字符串值子项|值|
    |-------------------------|-----------|
    |**Internet**|**AuthenticodeRequired**|
    |**UntrustedSites**|**已禁用**|
    |**MyComputer**|**Enabled**|
    |**LocalIntranet**|**Enabled**|
    |**TrustedSites**|**Enabled**|

     默认情况下 **，Internet** 具有值 **AuthenticodeRequired，UntrustedSites** 具有值 **Disabled**。 

### <a name="to-enable-the-inclusion-list-programmatically"></a>以编程方式启用包含列表

1. 创建Visual Basic Visual C# 控制台应用程序。

2. 打开 *Program.vb* 或 *Program.cs* 文件进行编辑并添加以下代码。

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "Enabled")
    key.SetValue("LocalIntranet", "Enabled")
    key.SetValue("Internet", "AuthenticodeRequired")
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

## <a name="restrict-the-inclusion-list"></a>限制包含列表
 限制包含列表，以便解决方案必须使用具有已知标识的 Authenticode 证书进行签名，然后提示用户做出信任决策。

### <a name="to-restrict-the-inclusion-list"></a>限制包含列表

1. 打开注册表编辑器：

    1. 单击 **“启动”** ，再单击 **“运行”** 。

    2. 在"**打开"** 框中 **，regedt32.exe**，然后单击"确定 **"。**

2. 查找以下注册表项：

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     如果密钥不存在，请创建它。

3. 将以下子项添加为 **字符串值**（如果它们不存在）以及关联的值。

    |字符串值子项|值|
    |-------------------------|-----------|
    |**UntrustedSites**|**已禁用**|
    |**Internet**|**AuthenticodeRequired**|
    |**MyComputer**|**AuthenticodeRequired**|
    |**LocalIntranet**|**AuthenticodeRequired**|
    |**TrustedSites**|**AuthenticodeRequired**|

     默认情况下 **，Internet** 具有值 **AuthenticodeRequired，UntrustedSites** 具有值 **Disabled**。 

### <a name="to-restrict-the-inclusion-list-programmatically"></a>以编程方式限制包含列表

1. 创建Visual Basic Visual C# 控制台应用程序。

2. 打开 *Program.vb* 或 *Program.cs* 文件进行编辑并添加以下代码。

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

## <a name="disable-the-inclusion-list"></a>禁用包含列表
 可以禁用包含列表，以便最终用户只能安装使用受信任的已知证书签名的解决方案。

### <a name="to-disable-the-inclusion-list"></a>禁用包含列表

1. 打开注册表编辑器：

    1. 单击 **“启动”** ，再单击 **“运行”** 。

    2. 在"**打开"** 框中 **，regedt32.exe**，然后单击"确定 **"。**

2. 如果注册表项不存在，请创建以下注册表项：

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

3. 将以下子项添加为 **字符串值**（如果它们不存在）以及关联的值。

    |字符串值子项|值|
    |-------------------------|-----------|
    |**UntrustedSites**|**已禁用**|
    |**Internet**|**已禁用**|
    |**MyComputer**|**已禁用**|
    |**LocalIntranet**|**已禁用**|
    |**TrustedSites**|**已禁用**|

### <a name="to-disable-the-inclusion-list-programmatically"></a>以编程方式禁用包含列表

1. 创建Visual Basic Visual C# 控制台应用程序。

2. 打开 *Program.vb* 或 *Program.cs* 文件进行编辑并添加以下代码。

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
- [使用Office信任解决方案](../vsto/trusting-office-solutions-by-using-inclusion-lists.md)
- [安全Office解决方案](../vsto/securing-office-solutions.md)
