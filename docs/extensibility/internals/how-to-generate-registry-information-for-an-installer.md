---
title: 如何：为安装程序生成注册表信息 |Microsoft Docs
description: 了解如何使用 Visual Studio 中的 RegPkg.exe 实用工具生成用于合并 Windows 安装程序安装包的 VSPackage 注册表信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
- VSPackages, registration manifests
ms.assetid: b1b41012-a777-4ccf-81a6-3b41f0e96583
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 092421db5e1ee4d38193b32b07650929aadbab4e6941b57950028640b1af1ad7
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448034"
---
# <a name="how-to-generate-registry-information-for-an-installer"></a>如何：为安装程序生成注册表信息

*RegPkg.exe* 实用工具可用于为托管 VSPackage 生成注册清单。 清单可以合并到 Windows Installer 安装包中。 RegPkg 还可以生成一个文件，该文件可以包含在基于[Windows Installer XML 工具集](https://wixtoolset.org/)的安装程序源文件中。

> [!IMPORTANT]
> RegPkg 生成特定于您的开发系统的路径名称，因此，每次使用 RegPkg 时，必须编辑输出，以使用适当的 Windows Installer 格式属性。 例如， `InprocServer32` 应 *\<SystemFolder\>mscoree.dll* 值并且路径应使用 *\<#filekey\>* 和 *\<$componentkey\>* 。 以这种方式调整输出支持 Windows 计算机安装在不同的驱动器上，或者安装在不同的目录、本地化的目录名称以及用户可以选择的路径中。 有关详细信息，请参阅 Windows Installer SDK 中的[格式设置](https://msdn.microsoft.com/library?url=/library/msi/setup/formatted.asp)。 如果你遵循开发系统路径的 RegPkg 约定（例如 *File_ \<filename\>* 格式的文件 id），则需要进行更少的更改。

## <a name="to-create-a-registration-manifest"></a>创建注册清单

- 在 **/regfile** 开关上运行 RegPkg。 提供任何其他开关、输出文件的名称和 VSPackage 的路径。

     例如，在命令提示符下，键入如下所示的内容：

    ```
    <Visual Studio SDK installation path>\VisualStudioIntegration\Tools\Bin\RegPkg /regfile:MyRegFile.reg MyPackage.dll
    ```

## <a name="to-view-a-registration-manifest"></a>查看注册清单

- 在任何文本编辑器中打开注册清单。

     以下示例是 RegPkg 为 IronPython 语言服务创建的注册清单：

    ```
    REGEDIT4

    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\CodeExpansions]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\CodeExpansions\Python]
    @="{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}"
    "DisplayName"="131"
    "IndexPath"="C:\\VSSDK80\\2006.07\\VisualStudioIntegration\\Samples\\IronPythonIntegration\\bin\\Release\\CodeSnippets\\SnippetsIndex.xml"
    "LangStringId"="python"
    "Package"="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}"
    "ShowRoots"=dword:00000000
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\CodeExpansions\Python\ForceCreateDirs]
    "Python"="C:\\VSSDK80\\2006.07\\VisualStudioIntegration\\Samples\\IronPythonIntegration\\bin\\Release\\CodeSnippets\\Snippets\\;%MyDocs%\Code Snippets\Python\My Code Snippets\"
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\CodeExpansions\Python\Paths]
    "Python"="C:\\VSSDK80\\2006.07\\VisualStudioIntegration\\Samples\\IronPythonIntegration\\bin\\Release\\CodeSnippets\\Snippets\\;%MyDocs%\Code Snippets\Python\My Code Snippets\"
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Packages]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Packages\{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}]
    @="Microsoft.Samples.VisualStudio.IronPythonLanguageService.PythonPackage, IronPython.LanguageService, Version=1.0.2373.36479, Culture=neutral, PublicKeyToken=null"
    "InprocServer32"="C:\\WINNT\\system32\\mscoree.dll"
    "Class"="Microsoft.Samples.VisualStudio.IronPythonLanguageService.PythonPackage"
    "Assembly"="IronPython.LanguageService, Version=1.0.2373.36479, Culture=neutral, PublicKeyToken=null"
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\File Extensions]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\File Extensions\.py]
    @="{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}"
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\Language Services]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Languages\Language Services\Python]
    @="{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}"
    "Package"="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}"
    "LangResID"=dword:00000064
    "ShowMatchingBrace"=dword:00000001
    "CodeSense"=dword:00000001
    "MatchBraces"=dword:00000001
    "EnableCommenting"=dword:00000001
    "ShowCompletion"=dword:00000001
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Packages]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Packages\{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}]
    "ID"=dword:00000001
    "MinEdition"="standard"
    "ProductVersion"="1.0"
    "ProductName"="Visual Studio Integration of IronPython Language Service"
    "CompanyName"="Microsoft Corporation"
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Services]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Services\{923b4811-26e4-4347-ac8a-244762798e1c}]
    @="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}"
    "Name"="IPythonLibraryManager"
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Services]
    [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Services\{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}]
    @="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}"
    "Name"="Python"

    ```

## <a name="to-create-a-windows-installer-xml-toolset-include-file"></a>创建 Windows Installer XML 工具集包含文件

- 在 **/wixfile** 开关上运行 RegPkg。 提供任何其他开关、输出文件的名称和 VSPackage 的路径。

     例如，在命令提示符下，键入如下所示的内容：

    ```
    <Visual Studio SDK installation path>\VisualStudioIntegration\Tools\Bin\RegPkg /codebase /wixfile:IronPython.LanguageService.wxi ..\bin\Release\IronPython.LanguageService.dll
    ```

## <a name="to-view-a-windows-installer-xml-toolset-include-file"></a>查看 Windows Installer 的 XML 工具集包含文件

- 在任意文本编辑器中打开 Windows Installer XML 工具集包含文件。

     以下示例是 RegPkg 为 IronPython 语言服务创建的包含文件：

    ```xml
    <Include>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Languages\IntellisenseProviders\IronPythonCodeProvider">
        <Registry Name="GUID" Value="{9c1807ea-d222-4775-afa8-c092c580e451}" Type="string" />
        <Registry Name="AddItemLanguageName" Value="Iron Python" Type="string" />
        <Registry Name="DefaultExtension" Value=".py" Type="string" />
        <Registry Name="ShortLanguageName" Value="IronPython;Python" Type="string" />
        <Registry Name="TemplateFolderName" Value="IronPython" Type="string" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Languages\CodeExpansions\Python" Value="{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}" Type="string">
        <Registry Name="DisplayName" Value="131" Type="string" />
        <Registry Name="IndexPath" Value="C:\\VSSDK80\\2006.08\\VisualStudioIntegration\\Samples\\IronPythonIntegration\\Setup\\[$ComponentPath]\\CodeSnippets\\SnippetsIndex.xml" Type="string" />
        <Registry Name="LangStringId" Value="python" Type="string" />
        <Registry Name="Package" Value="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}" Type="string" />
        <Registry Name="ShowRoots" Value="0" Type="integer" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Languages\CodeExpansions\Python\ForceCreateDirs">
        <Registry Name="Python" Value="C:\\VSSDK80\\2006.08\\VisualStudioIntegration\\Samples\\IronPythonIntegration\\Setup\\[$ComponentPath]\\CodeSnippets\\Snippets\\;%MyDocs%\Code Snippets\Python\My Code Snippets\" Type="string" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Languages\CodeExpansions\Python\Paths">
        <Registry Name="Python" Value="C:\\VSSDK80\\2006.08\\VisualStudioIntegration\\Samples\\IronPythonIntegration\\Setup\\[$ComponentPath]\\CodeSnippets\\Snippets\\;%MyDocs%\Code Snippets\Python\My Code Snippets\" Type="string" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Languages\File Extensions\.py" Value="{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}" Type="string" />

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Languages\Language Services\Python" Value="{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}" Type="string">
        <Registry Name="Package" Value="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}" Type="string" />
        <Registry Name="LangResID" Value="100" Type="integer" />
        <Registry Name="ShowCompletion" Value="1" Type="integer" />
        <Registry Name="ShowMatchingBrace" Value="1" Type="integer" />
        <Registry Name="CodeSense" Value="1" Type="integer" />
        <Registry Name="MatchBraces" Value="1" Type="integer" />
        <Registry Name="EnableCommenting" Value="1" Type="integer" />
        <Registry Name="DefaultToInsertSpaces" Value="1" Type="integer" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Packages\{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}" Value="Microsoft.Samples.VisualStudio.IronPythonLanguageService.PythonPackage, IronPython.LanguageService, Version=1.0.2394.27719, Culture=neutral, PublicKeyToken=null" Type="string">
        <Registry Name="InprocServer32" Value="[SystemFolder]mscoree.dll" Type="string" />
        <Registry Name="Class" Value="Microsoft.Samples.VisualStudio.IronPythonLanguageService.PythonPackage" Type="string" />
        <Registry Name="CodeBase" Value="[#File_IronPython.LanguageService.dll]" Type="string" />
        <Registry Name="ID" Value="1" Type="integer" />
        <Registry Name="MinEdition" Value="standard" Type="string" />
        <Registry Name="ProductVersion" Value="1.0" Type="string" />
        <Registry Name="ProductName" Value="Visual Studio Integration of IronPython Language Service" Type="string" />
        <Registry Name="CompanyName" Value="Microsoft Corporation" Type="string" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\CLSID\{9c1807ea-d222-4775-afa8-c092c580e451}" Value="Microsoft.Samples.VisualStudio.IronPythonLanguageService.PythonIntellisenseProvider" Type="string">
        <Registry Name="InprocServer32" Value="[SystemFolder]mscoree.dll" Type="string" />
        <Registry Name="Class" Value="Microsoft.Samples.VisualStudio.IronPythonLanguageService.PythonIntellisenseProvider" Type="string" />
        <Registry Name="CodeBase" Value="[#File_IronPython.LanguageService.dll]" Type="string" />
        <Registry Name="ThreadingModel" Value="Both" Type="string" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Services\{923b4811-26e4-4347-ac8a-244762798e1c}" Value="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}" Type="string">
        <Registry Name="Name" Value="IPythonLibraryManager" Type="string" />
      </Registry>

      <Registry Root="HKLM" Key="Software\Microsoft\VisualStudio\8.0\Services\{ae8ce01a-b3ff-4c19-8c80-54669c197f2c}" Value="{1b05e2b4-7c21-4f63-910e-29fe55eb5f8b}" Type="string">
        <Registry Name="Name" Value="Python" Type="string" />
      </Registry>
    </Include>
    ```

## <a name="see-also"></a>另请参阅

- [注册 Vspackage](../../extensibility/registering-and-unregistering-vspackages.md)
- [VSPackages](../../extensibility/internals/vspackages.md)
