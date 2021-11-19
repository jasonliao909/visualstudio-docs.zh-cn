---
title: '按需下载程序集 (ClickOnce API) '
description: 了解如何将应用程序中的某些程序集标记为ClickOnce可选程序集，并下载它们（当公共语言运行时需要它们时）。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- assemblies, downloading [ClickOnce]
- ClickOnce deployment, on-demand download
- on-demand assemblies, ClickOnce
ms.assetid: d20e2789-8621-4806-b5b7-841122da1456
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 046d6932e1bfcbc6f0a4b3c60fab96806b4473fd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664648"
---
# <a name="walkthrough-download-assemblies-on-demand-with-the-clickonce-deployment-api"></a>演练：使用 ClickOnce API 按需下载程序集
默认情况下，应用程序中包含的所有程序集在首次运行时 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 下载。 但是，你可能拥有一小部分用户使用的应用程序部分。 在这种情况下，你希望仅当创建其类型之一时才下载程序集。 下面的演练演示如何将应用程序中的某些程序集标记为“可选”，以及如何在公共语言运行时 (CLR) 需要它们时使用 <xref:System.Deployment.Application> 命名空间中的类下载它们。

> [!NOTE]
> 应用程序必须在完全信任下运行才能使用此过程。

## <a name="prerequisites"></a>先决条件
 需要以下组件之一才能完成本演练：

- Windows SDK。 可以从Windows下载中心下载该 SDK。

- Visual Studio。

## <a name="create-the-projects"></a>创建项目

#### <a name="to-create-a-project-that-uses-an-on-demand-assembly"></a>创建使用按需程序集的项目

1. 创建名为 ClickOnceOnDemand 的目录。

2. 打开 Windows SDK 命令提示符或 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 命令提示符。

3. 更改为 ClickOnceOnDemand 目录。

4. 使用下列命令生成公钥/私钥对：

   ```cmd
   sn -k TestKey.snk
   ```

5. 使用记事本或其他文本编辑器，使用名为 的单个属性 `DynamicClass` 定义名为 的类 `Message` 。

    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceLibrary/VB/Class1.vb" id="Snippet1":::
    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceLibrary/CS/Class1.cs" id="Snippet1":::

6. 将文本另存为名为 *ClickOnceLibrary.cs* 或 *ClickOnceLibrary.vb* 的文件，具体取决于你使用的语言，保存到 *ClickOnceOnDemand* 目录。

7. 将文件编译为程序集。

   ```csharp
   csc /target:library /keyfile:TestKey.snk ClickOnceLibrary.cs
   ```

   ```vb
   vbc /target:library /keyfile:TestKey.snk ClickOnceLibrary.vb
   ```

8. 若要获取程序集的公钥令牌，请使用以下命令：

   ```cmd
   sn -T ClickOnceLibrary.dll
   ```

9. 使用文本编辑器创建新文件并输入以下代码。 此代码创建一Windows窗体应用程序，该应用程序在需要时下载 ClickOnceLibrary 程序集。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceOnDemandCmdLine/CS/Form1.cs" id="Snippet1":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceOnDemandCmdLine/VB/Form1.vb" id="Snippet1":::

10. 在代码中，找到对 的调用 <xref:System.Reflection.Assembly.LoadFile%2A> 。

11. 将 `PublicKeyToken` 设置为之前检索到的值。

12. 将文件另存为 *Form1.cs* 或 *Form1.vb*。

13. 使用下列命令将文件编译为可执行文件。

    ```csharp
    csc /target:exe /reference:ClickOnceLibrary.dll Form1.cs
    ```

    ```vb
    vbc /target:exe /reference:ClickOnceLibrary.dll Form1.vb
    ```

## <a name="mark-assemblies-as-optional"></a>将程序集标记为可选

#### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-mageuiexe"></a>使用 MageUI.exe 在 ClickOnce 应用程序中将程序集标记为可选MageUI.exe

1. 使用 *MageUI.exe，* 根据演练：手动部署应用程序 中所述创建ClickOnce [清单](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。 对应用程序清单使用以下设置：

    - 将应用程序清单命名 `ClickOnceOnDemand` 。

    - 在"**文件"** 页 *的"ClickOnceLibrary.dll"* 行中，将"**文件类型"列** 设置为"无 **"。**

    - 在" **文件** "页 *的"ClickOnceLibrary.dll"* 行 `ClickOnceLibrary.dll` 中，键入" **组"** 列。

2. 使用 *MageUI.exe，* 创建部署清单，如演练：手动部署 ClickOnce [应用程序中所述](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。 对部署清单使用以下设置：

    - 将部署清单命名 `ClickOnceOnDemand` 。

## <a name="testing-the-new-assembly"></a>测试新程序集

#### <a name="to-test-your-on-demand-assembly"></a>测试按需程序集

1. Upload [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署到 Web 服务器。

2. 通过输入部署清单的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] URL，从 Web 浏览器启动使用 部署的应用程序。 如果调用应用程序 ，并将其上传到 adatum.com 的根目录， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `ClickOnceOnDemand` 则 URL 将如下所示：

   ```
   http://www.adatum.com/ClickOnceOnDemand/ClickOnceOnDemand.application
   ```

3. 在主窗体显示时按 <xref:System.Windows.Forms.Button>。 应在消息框窗口中看到一个显示为“Hello, World!”的字符串。

## <a name="see-also"></a>另请参阅
- <xref:System.Deployment.Application.ApplicationDeployment>