---
title: 创建产品清单 | Microsoft Docs
description: 了解如何使用包含单个产品清单的包和每个区域设置的包清单，部署 ClickOnce 应用程序的必备组件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- product files [ClickOnce]
- product files [Windows Installer]
- prerequisites, custom bootstrapper package
- dependencies, custom bootstrapper package
ms.assetid: 2d316aaa-8bc0-4ce5-90ab-23b3eac0b5dd
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: e58dbabb15b0d0a3643b38693d614aaf16a4a60c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665611"
---
# <a name="how-to-create-a-product-manifest"></a>如何：创建产品清单
若要部署应用程序的必备组件，可以创建引导程序包。 引导程序包包含单个产品清单文件，但每个区域设置都有一个包清单。 包清单包含包的本地化特定方面。 这包括字符串、最终用户许可协议和语言包。

 有关包清单的详细信息，请参阅[如何：创建包清单](../deployment/how-to-create-a-package-manifest.md)。

## <a name="create-the-product-manifest"></a>创建产品清单

#### <a name="to-create-the-product-manifest"></a>创建产品清单的步骤

1. 为引导程序包创建目录。 此示例使用 C:\package。

2. 在 Visual Studio 中，创建一个名为“product.xml”的新 XML 文件，并将其保存到 C:\package 文件夹中 。

3. 添加以下 XML 来描述包的 XML 命名空间和产品代码。 将产品代码替换为包的唯一标识符。

    ```xml
    <Product
    xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"
    ProductCode="Custom.Bootstrapper.Package">
    ```

4. 添加 XML 以指定包具有依赖项。 此示例使用 Microsoft Windows Installer 3.1 的依赖项。

    ```xml
    <RelatedProducts>
        <DependsOnProduct Code="Microsoft.Windows.Installer.3.1" />
      </RelatedProducts>
    ```

5. 添加 XML 以列出引导程序包中的所有文件。 此示例使用包文件名 CorePackage.msi。

    ```xml
    <PackageFiles>
        <PackageFile Name="CorePackage.msi"/>
    </PackageFiles>
    ```

6. 将 CorePackage.msi 文件复制或移动到 C:\package 文件夹 。

7. 添加 XML 以使用引导程序命令安装包。 引导程序会自动将 /qn 标记添加到 .msi 文件，该文件将以静默方式安装。 如果该文件是 .exe，引导程序将使用 shell 运行 .exe 文件 。 以下 XML 不显示 CorePackage.msi 的任何参数，但你可将命令行参数放入 `Arguments` 属性中。

    ```xml
    <Commands>
        <Command PackageFile="CorePackage.msi" Arguments="">
    ```

8. 添加以下 XML 以检查是否安装了此引导程序包。 将产品代码替换为可再发行组件的 GUID。

    ```xml
    <InstallChecks>
        <MsiProductCheck
            Property="IsMsiInstalled"
            Product="{XXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}"/>
    </InstallChecks>
    ```

9. 添加 XML 以更改引导程序行为，具体取决于是否已安装引导程序组件。 如果组件已安装，则引导程序包不会运行。 以下 XML 检查当前用户是否为管理员，因为此组件需要管理权限。

    ```xml
    <InstallConditions>
        <BypassIf
           Property="IsMsiInstalled"
           Compare="ValueGreaterThan" Value="0"/>
        <FailIf Property="AdminUser"
            Compare="ValueNotEqualTo" Value="True"
            String="NotAnAdmin"/>
    </InstallConditions>
    ```

10. 添加 XML 以设置安装成功时和需要重新启动时的退出代码。 以下 XML 演示 Fail 和 FailReboot 退出代码，它们表示引导程序将不会继续安装包。

    ```xml
    <ExitCodes>
        <ExitCode Value="0" Result="Success"/>
        <ExitCode Value="1641" Result="SuccessReboot"/>
        <ExitCode Value="3010" Result="SuccessReboot"/>
        <DefaultExitCode Result="Fail" String="GeneralFailure"/>
    </ExitCodes>
    ```

11. 添加以下 XML 以结束引导程序命令部分。

    ```xml
        </Command>
    </Commands>
    ```

12. 将 C:\package 文件夹移动到 Visual Studio 引导程序目录。 对于 Visual Studio 2010，则为 \Program Files\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages 目录。

## <a name="example"></a>示例
 产品清单包含自定义必备组件的安装说明。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Product
  xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"
  ProductCode="Custom.Bootstrapper.Package">

  <RelatedProducts>
    <DependsOnProduct Code="Microsoft.Windows.Installer.3.1" />
  </RelatedProducts>

  <PackageFiles>
    <PackageFile Name="CorePackage.msi"/>
  </PackageFiles>

  <InstallChecks>
    <MsiProductCheck Product="IsMsiInstalled"
      Property="{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}"/>
  </InstallChecks>

  <Commands>
    <Command PackageFile="CorePackage.msi" Arguments="">

      <InstallConditions>
        <BypassIf Property="IsMsiInstalled"
          Compare="ValueGreaterThan" Value="0"/>
        <FailIf Property="AdminUser"
          Compare="ValueNotEqualTo" Value="True"
         String="NotAnAdmin"/>
      </InstallConditions>

      <ExitCodes>
        <ExitCode Value="0" Result="Success"/>
        <ExitCode Value="1641" Result="SuccessReboot"/>
        <ExitCode Value="3010" Result="SuccessReboot"/>
        <DefaultExitCode Result="Fail" String="GeneralFailure"/>
      </ExitCodes>
    </Command>
  </Commands>
</Product>
```

## <a name="see-also"></a>另请参阅
- [产品和包架构引用](../deployment/product-and-package-schema-reference.md)