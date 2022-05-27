---
title: 使用 Windows Installer 部署 VSTO 解决方案
description: 了解如何使用 Visual Studio Installer 项目部署 Microsoft Visual Studio Tools for Office (VSTO) 加载项或文档级解决方案。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 08/18/2010
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, setup project
- Office development in Visual Studio, MSI
- deploying applications [Office development in Visual Studio], setup project
- deploying applications [Office development in Visual Studio], MSI
- ClickOnce deployment [Office development in Visual Studio], MSI
- publishing Office solutions [Office development in Visual Studio], setup project
- Office applications [Office development in Visual Studio], MSI
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 6a9b72877adcc055f87547ddbb38e5a2523919cb
ms.sourcegitcommit: 4264e57e45dede8bf55ddf0f7e81738a42580081
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2022
ms.locfileid: "145183484"
---
# <a name="deploying-a-vsto-solution-using-windows-installer"></a>使用 Windows Installer 部署 VSTO 解决方案

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

## <a name="summary"></a>摘要

了解如何使用 Visual Studio Installer 项目部署 Microsoft Visual Studio Tools for Office (VSTO) 加载项或文档级解决方案。

Wouter van Vugt， Code Counsel

泰德·帕蒂森，泰德·帕蒂森集团

本文由 Microsoft 通过原始作者的权限进行更新。

**适用于：** Visual Studio Tools for Office、Microsoft Office、Microsoft Visual Studio。

## <a name="overview"></a>概述

可以使用 Windows Installer 包开发 VSTO 解决方案并部署解决方案。 此讨论包括部署简单 Office 外接程序的步骤。

## <a name="deployment-methods"></a>部署方法

ClickOnce 可以轻松用于为加载项和解决方案创建设置。 但是，它无法安装需要管理权限的外接程序，例如计算机级外接程序。

可以使用 Windows Installer 安装需要管理权限的加载项，但它确实需要更多精力来创建安装程序。

有关如何使用 ClickOnce 部署 VSTO 解决方案的概述，请参阅 [使用 ClickOnce 部署 Office 解决方案](deploying-an-office-solution-by-using-clickonce.md)。

## <a name="deploying-office-solutions-that-target-the-vsto-runtime"></a>部署面向 VSTO 运行时的 Office 解决方案

在安装 Office 解决方案时，ClickOnce 和 Windows Installer 包需要执行相同的基本的任务。

1. 在用户计算机上安装必备组件。
2. 部署解决方案的特定组件。
3. 对于外接程序，请创建注册表项。
4. 信任解决方案以允许其执行。

### <a name="required-prerequisite-components-on-the-target-computer"></a>目标计算机上的必需先决条件组件

下面是必须安装在计算机上才能运行 VSTO 解决方案的软件列表：

- Microsoft Office 2010 或更高版本。
- Microsoft .NET Framework 4 或更高版本。
- Microsoft Visual Studio 2010 Tools for Office Runtime。
  运行时提供管理加载项和文档级解决方案的环境。 运行时版本确实随 Microsoft Office 一起提供，但你可能希望使用加载项重新分发特定版本。
- 如果你未使用嵌入式互操作类型，则 Microsoft Office 的主要互操作程序集。
- 项目引用的任何实用程序程序集。

### <a name="specific-components-for-the-solution"></a>解决方案的特定组件

安装程序包必须将这些组件安装到用户的计算机上：

- 如果创建文档级解决方案，Microsoft Office 文档。
- 自定义程序集及其所需的任何程序集。
- 其他组件，例如配置文件。
- 应用程序清单 (.manifest) 。
- 部署清单 (.vsto) 。

### <a name="registry-entries-for-add-ins"></a>加载项的注册表项

Microsoft Office 使用注册表项来查找和加载外接程序。应在部署过程中创建这些注册表项。 有关这些注册表项的详细信息，请参阅 [VSTO 外接程序的注册表项](registry-entries-for-vsto-add-ins.md)。

显示自定义窗体区域的 Outlook 外接程序需要其他注册表项，这些注册表项允许标识窗体区域。 有关注册表项的详细信息，请参阅 [Outlook 窗体区域的注册表项](registry-entries-for-vsto-add-ins.md#OutlookEntries)。

文档级解决方案不需要任何注册表项。 相反，文档中的属性用于查找自定义项。 有关这些属性的详细信息，请参阅 [自定义文档属性概述](custom-document-properties-overview.md)。

### <a name="trusting-the-vsto-solution"></a>信任 VSTO 解决方案

若要运行自定义项，计算机必须信任解决方案。 可以通过使用证书对清单进行签名、创建与包含列表的信任关系，或将其安装到计算机上的受信任位置来信任加载项。

有关如何获取用于签名的证书的详细信息，请参阅 [ClickOnce 部署和验证码](../deployment/clickonce-and-authenticode.md)。 有关信任解决方案的详细信息，请参阅 [使用包含列表信任 Office 解决方案](trusting-office-solutions-by-using-inclusion-lists.md)。 可以在 Windows Installer 文件中添加包含列表项和自定义操作。 有关启用包含列表的详细信息，请参阅 [如何：配置包含列表安全性](how-to-configure-inclusion-list-security.md)。

如果未使用任一选项，则会向用户显示信任提示，让他们决定是否信任解决方案。

有关与文档级解决方案相关的安全性的详细信息，请参阅 [授予对文档的信任](granting-trust-to-documents.md)。

## <a name="creating-a-basic-installer"></a>创建基本安装程序

安装程序和部署项目模板包含在可供下载的 [Microsoft Visual Studio 安装程序项目](https://marketplace.visualstudio.com/items?itemName=visualstudioclient.MicrosoftVisualStudio2017InstallerProjects) 扩展中。

若要为 Office 解决方案创建安装程序，必须完成以下任务：

- 添加将部署的 Office 解决方案的组件。
- 对于应用程序级外接程序，请配置注册表项。
- 配置必备组件，以便可以在最终用户计算机上安装这些组件。
- 配置启动条件以验证所需的必备组件是否可用。 如果未安装所有必需的先决条件，则可以使用启动条件阻止安装。

第一步是创建安装项目。

### <a name="to-create-the-addin-setup-project"></a>创建 AddIn 安装程序项目

1. 打开要部署的 Office AddIn 项目。 在本示例中，我们使用一个名为 ExcelAddIn 的 Excel 外接程序。
2. 打开 Office 项目后，在 **“文件”** 菜单上展开“ **添加** ”，然后单击“ **新建项目** ”添加新项目。
::: moniker range="=vs-2017"
3. 在“**添加新项目**”对话框中，展开 **“项目类型”窗格中的其他项目类型**，然后展开 **“设置”和“部署**”，然后选择 **“Visual Studio 安装程序**”。
4. 在 **“模板**”窗格中，从 **Visual Studio 安装的** 模板组中选择 **“安装项目**”。
::: moniker-end
::: moniker range="=vs-2019"
3. 在“ **添加新项目** ”对话框中，选择 **“安装项目** ”模板。
4. 单击“下一步”。
::: moniker-end

5. 在 **“名称”** 框中，键入 **OfficeAddInSetup**。
::: moniker range="=vs-2017"
6. 单击“ **打开** ”创建新的安装项目。
::: moniker-end
::: moniker range="=vs-2019"
6. 单击“ **创建** ”以创建新的安装项目。
::: moniker-end

Visual Studio 打开新安装项目的文件系统资源管理器。 文件系统资源管理器允许将文件添加到安装项目。

   ![安装程序项目的文件系统资源管理器的屏幕截图](media/setup-project-figure-1.png)

   **图 1：安装项目的文件系统资源管理器**

安装项目需要部署 ExcelAddIn。 可以通过将 ExcelAddIn 项目输出添加到安装项目来配置此任务的安装项目。

### <a name="to-add-the-exceladdin-project-output"></a>添加 ExcelAddIn 项目输出

1. 在 **解决方案资源管理器** 中，右键单击 **OfficeAddInSetup**，单击“ **添加”** ，然后单击 **“项目输出**”。
2. 在 **“添加项目输出组** ”对话框中，从项目列表中选择 **ExcelAddIn** ，然后选择 **“主输出**”。
3. 单击 **“确定** ”将项目输出添加到安装项目。

    ![“设置项目添加项目输出组”对话框的屏幕截图](media/setup-project-figure-2.png)

    **图 2：“设置项目添加项目输出组”对话框**

安装项目需要部署部署清单和应用程序清单。 将这两个文件作为 ExcelAddIn 项目的输出文件夹中的独立文件添加到安装程序项目中。

### <a name="to-add-the-deployment-and-application-manifests"></a>添加部署和应用程序清单

1. 在 **解决方案资源管理器** 中，右键单击 **OfficeAddInSetup**，单击“ **添加**”，然后单击“ **文件**”。
2. 在“ **添加文件** ”对话框中，导航到 **ExcelAddIn** 输出目录。 通常，输出目录是项目根目录的 **bin\\发布** 子文件夹，具体取决于所选生成配置。
3. 选择 **ExcelAddIn.vsto** 和 **ExcelAddIn.dll.manifest** 文件，然后单击“ **打开** ”将这两个文件添加到安装项目。

    ![解决方案资源管理器中应用程序和部署清单的屏幕截图](media/setup-project-figure-3.jpg)

    **图 3：解决方案资源管理器中加载项的应用程序和部署清单**

引用 ExcelAddIn 包括 ExcelAddIn 需要的所有组件。 必须使用必备包排除和部署这些组件，以便正确注册这些组件。 此外，在安装开始之前，必须显示并接受软件许可条款。

### <a name="to-exclude-the-exceladdin-project-dependencies"></a>排除 ExcelAddIn 项目依赖项

1. 在 **解决方案资源管理器** 的 **OfficeAddInSetup** 节点中，选择 **“检测到的依赖项**”项下的所有依赖项项，但 **Microsoft .NET Framework** 或任何以 **\*.Utilities.dll** 结尾的程序集除外。 实用工具程序集旨在与应用程序一起部署。
2. 右键单击该组，然后选择“ **属性**”。
3. 在 **“属性”** 窗口中，将 **Exclude** 属性更改为 **True** ，以从安装项目中排除依赖程序集。 请确保不排除任何实用工具程序集。

    ![显示要排除的依赖项的解决方案资源管理器屏幕截图](media/setup-project-figure-4.jpg)

    **图 4：排除依赖项**

可以通过添加安装程序（也称为引导程序）来配置 Windows Installer 包以安装必备组件。 此安装程序可以安装必备组件（称为引导过程）。

对于 **ExcelAddIn**，必须先安装这些先决条件，然后加载项才能正常运行：

- Office解决方案面向的 Microsoft .NET Framework 版本。
- Microsoft Visual Studio 2010 Tools for Office Runtime。

将依赖组件配置为先决条件

1. 在 **解决方案资源管理器** 中，右键单击 **OfficeAddInSetup** 项目，然后选择“**属性**”。
2. 此时会显示 **“OfficeAddInSetup 属性页** ”对话框。
3. 单击“ **先决条件** ”按钮。
4. 在“先决条件”对话框中，选择.NET Framework的正确版本和用于Office运行时的Microsoft Visual Studio工具。

    ![“先决条件”对话框的屏幕截图](media/setup-project-figure-5.png)

    **图 5：“先决条件”对话框**

    > [!NOTE]
    >Visual Studio安装程序Project中配置的某些先决条件包依赖于所选生成配置。 必须为每个使用的生成配置选择适当的先决条件组件。

Microsoft Office使用注册表项查找外接程序。 HKEY\_CURRENT\_USER hive 中的密钥用于注册每个用户的外接程序。 HKEY\_LOCAL\_MACHINE hive 下的密钥用于注册计算机的所有用户的外接程序。 有关注册表项的详细信息，请参阅 [VSTO 外接程序的注册表项](registry-entries-for-vsto-add-ins.md)。

### <a name="to-configure-the-registry"></a>配置注册表

1. 在 **解决方案资源管理器** 中，右键单击 **OfficeAddInSetup**。
2. 展开 **视图**。
3. 单击 **“注册表** ”打开注册表编辑器窗口。
4. 在 **注册表 (OfficeAddInSetup)** 编辑器中，展开 **HKEY\_LOCAL\_MACHINE** ，然后展开 **软件**。
5. 删除 **HKEY\_LOCAL\_MACHINE\\Software** 下找到的 **\[制造商\]** 密钥。
6. 展开 **HKEY\_CURRENT\_USER** ，然后展开 **软件**。
7. 删除 **HKEY\_CURRENT\_USER\\Software** 下找到 **的\[制造商\]** 密钥。
8. 若要为外接程序安装添加注册表项，请右键单击 **“用户/计算机 Hive** ”密钥，选择“ **新建密钥**”。 将文本 **软件** 用于新密钥的名称。 右键单击新创建的 **软件** 密钥，并使用 **Microsoft** 文本创建新密钥。
9. 使用类似的过程创建加载项注册所需的整个密钥层次结构：

    **User/Machine Hive\\Software\\Microsoft\\ Office\\ Excel\\ Addins\\SampleCompany.ExcelAddIn**

    公司名称通常用作外接程序名称的前缀，以提供唯一性。

10. 右键单击 **SampleCompany.ExcelAddIn** 键，选择“ **新建**”，然后单击“ **字符串”值**。 使用名称的文本 **说明** 。
11. 使用此步骤添加另外三个值：
    - **String** 类型的 **FriendlyName**
    - **DWORD** 类型的 **LoadBehavior**
    - **字符串** 类型的 **清单**

12. 右键单击注册表编辑器中的 **“说明** ”值，然后单击“ **属性”窗口**。 在 **“属性”窗口中**，输入“值”属性 **Excel Demo AddIn**。
13. 在注册表编辑器中选择 **FriendlyName** 键。 在 **“属性”窗口中**，将 **Value** 属性更改为 **Excel Demo AddIn**。
14. 在注册表编辑器中选择 **LoadBehavior** 密钥。 在 **“属性”窗口中**，将 **Value** 属性更改为 **3。** LoadBehavior 的值 3 指示外接程序应在主机应用程序的启动时加载。 有关加载行为的详细信息，请参阅 [VSTO 外接程序的注册表项](registry-entries-for-vsto-add-ins.md)。

15. 在注册表编辑器中选择 **清单** 密钥。 在 **“属性”窗口中**，将 **Value** 属性更改为 **file:///[TARGETDIR]ExcelAddIn.vsto|vstolocal**

    ![注册表编辑器的屏幕截图](media/setup-project-figure-6.png)

    **图 6：设置注册表项**

      VSTO 运行时使用此注册表项查找部署清单。 [TARGETDIR] 宏将替换为安装加载项的文件夹。 宏将包含尾随 \ 字符，因此部署清单的文件名应为 ExcelAddIn.vsto，而不带 \ 字符。
      **vstolocal** 后缀告知 VSTO 运行时外接程序应从此位置加载，而不是ClickOnce缓存。 删除此后缀将导致运行时将自定义项复制到ClickOnce缓存中。

   >[!WARNING]
   >Visual Studio中的注册表编辑器应非常小心。 例如，如果意外为错误的键设置了 DeleteAtUninstall，则可以删除注册表的活动部分，使用户计算机处于不一致甚至更糟的状态。

64 位版本的Office将使用 64 位注册表配置单元查找加载项。若要在 64 位注册表配置单元下注册外接程序，安装程序项目的目标平台必须仅设置为 64 位。

1. 在解决方案资源管理器中选择 **OfficeAddInSetup** 项目。
2. 转到 **“属性** ”窗口，并将 **TargetPlatform** 属性设置为 **x64**。

为 32 位和 64 位版本的 Office 安装外接程序需要创建两个单独的 MSI 包。 一个用于 32 位，一个用于 64 位。

  ![“属性”窗口的屏幕截图，其中显示了用于向 64 位Office注册外接程序的目标平台](media/setup-project-figure-7.jpg)

  **图 7：使用 64 位Office注册外接程序的目标平台**

如果 MSI 包用于安装外接程序或解决方案，则它可能会安装，而无需安装所需的先决条件。 可以使用 MSI 中的启动条件阻止外接程序安装（如果未安装先决条件）。

### <a name="configure-a-launch-condition-to-detect-the-vsto-runtime"></a>配置启动条件以检测 VSTO 运行时

1. 在 **解决方案资源管理器** 中，右键单击 **OfficeAddInSetup**。
2. 展开 **视图**。
3. 单击“ **启动条件**”。
4. 在 **“启动条件” (OfficeAddInSetup)** 编辑器中，右键单击 **目标计算机上的“要求**”，然后单击“ **添加注册表启动条件**”。 此搜索条件可以搜索注册表，查找 VSTO 运行时安装的密钥。 然后，键的值可通过命名属性对安装程序的各个部分可用。 启动条件使用搜索条件定义的属性来检查特定值。
5. 在 **“启动条件” (OfficeAddInSetup)** 编辑器中，选择 **“搜索 RegistryEntry1”** 搜索条件，右键单击条件，然后选择“ **属性”窗口**。

6. 在 **“属性”** 窗口中，设置以下属性：
   1. 将 **(名称)** 的值设置为 **搜索 VSTO 2010 运行时**。
   2. 将 **属性** 的值更改为 **VSTORUNTIMEREDIST**。
   3. 将 **RegKey** 的值设置为 **SOFTWARE\\Microsoft\\VSTO Runtime Setup\\v4R**
   4. 将 **Root** 属性设置为 **vsdrrHKLM**。
   5. 将 **Value** 属性更改为 **Version**。

7. 在 **“启动条件” (OfficeAddInSetup)** 编辑器中，选择 **Condition1** 启动条件，右键单击条件，然后选择“ **属性”窗口**。
8. 在“属性”窗口中，设置以下属性：
   1. 将 **(名称)** 设置为 **验证 VSTO 2010 运行时可用性**。
   2. 将 **条件** 的值更改为 **VSTORUNTIMEREDIST\>=“10.0.30319”**
   3. 将 **InstallURL** 属性留空。
   4. 未将 **消息** 设置为Visual Studio **2010 Tools for Office Runtime。请运行Setup.exe安装外接程序**。

        ![验证运行时可用性启动条件的属性窗口的屏幕截图](media/setup-project-figure-8.jpg)

        **图 8：验证运行时可用性启动条件的属性窗口**

 上述启动条件在引导程序包安装 VSTO 运行时时显式检查是否存在。

### <a name="configure-a-launch-condition-to-detect-the-vsto-runtime-installed-by-office"></a>配置启动条件以检测Office安装的 VSTO 运行时

1. 在 **“启动条件” (OfficeAddInSetup)** 编辑器中，右键单击 **“搜索目标计算机**”，然后单击“ **添加注册表搜索**”。
2. 选择 **“搜索 RegistryEntry1”** 搜索条件，右键单击该条件，然后选择“ **属性”窗口**。
3. 在 **“属性”** 窗口中，设置以下属性：
    1. 将 **(名称)** 的值设置为 **搜索Office VSTO 运行时**。
    2. 将 **属性** 的值更改为 **OfficeRuntime**。
    3. 将 **RegKey** 的值设置为 **SOFTWARE\\Microsoft\\VSTO 运行时安装程序\\v4**。
    4. 将 **Root** 属性保留为 **vsdrrHKLM**。
    5. 将 **Value** 属性更改为 **Version**。

4. 在 **“启动条件 (OfficeAddInSetup)** 编辑器中，选择前面定义的 **验证 VSTO 2010 运行时可用性** 启动条件，右键单击该条件，然后选择” **属性窗口**”。

5. 将 **Condition** 属性的值更改为 **VSTORUNTIMEREDIST \>=“10.0.30319” OR OFFICERUNTIME\>=“10.0.21022”。** 版本号可能因外接程序所需的运行时版本而异。

    ![启动条件的属性Windows屏幕截图](media/setup-project-figure-9.jpg)
  
    **图 9：通过 Redist 或Office启动条件验证运行时可用性的属性Windows**

如果外接程序面向 .NET Framework 4 或更高版本，则可以将引用的主互操作程序集中的类型 (PIA) 嵌入到 VSTO 程序集中。

若要通过执行以下步骤来检查互操作类型是否嵌入到外接程序中：

1. 在 解决方案资源管理器 中展开引用节点
2. 选择其中一个 PIA 引用，例如 **，Office**。
3. 通过点击 F4 或从“程序集”上下文菜单中选择“属性”来查看属性窗口。
4. 检查属性 **嵌入互操作类型** 的值。

如果该值设置为 **True**，则类型将嵌入，你可以跳到“ [**生成安装项目**](#to-build-the-setup-project) ”部分。

有关详细信息，请参阅 [类型等效性和嵌入式互操作类型](/dotnet/framework/interop/type-equivalence-and-embedded-interop-types)

### <a name="to-configure-launch-conditions-to-detect-that-for-office-pias"></a>配置启动条件以检测Office PIA

1. 在 **“启动条件” (OfficeAddInSetup)** 编辑器中，右键单击 **目标计算机上的“要求**”，**然后单击“添加Windows安装程序启动条件**”。 此启动条件通过搜索特定组件 ID 来搜索Office PIA。
2. 右键单击 **“搜索 Component1** ”，然后单击“ **属性”窗口** 以显示启动条件的属性。
3. 在 **“属性”窗口中**，设置以下属性：

    1. 将 **(Name)** 属性的值更改为 **“搜索Office共享 PIA**”
    2. 将 **ComponentID** 的值更改为所使用的Office组件的组件 ID。 可以在下表中找到组件 ID 列表，例如 **{64E2917E-AA13-4CA4-BFFE-EA6EDA3AFCB4}**。
    3. 将 **Property** 属性的值更改为 **HASSHAREDPIA**。

4. 在 **“启动条件” (OfficeAddInSetup)** 编辑器中，右键单击 **“Condition1** ”，然后单击“ **属性窗口** ”以显示启动条件的属性。

5. 更改 **Condition1** 的以下属性：

    1. 更改 **(名称)** 以 **验证共享 PIA 可用性Office**。
    2. 将 **条件** 更改为 **HASSHAREDPIA**。
    3. 将 **InstallUrl** 留空。
    4. 将 **消息** 更改为 **与Excel交互所需的组件不可用。请运行setup.exe**。

    ![“验证Office共享 PIA 启动条件”的属性窗口的屏幕截图](media/setup-project-figure-10.jpg)
  
    **图 10：验证Office共享 PIA 启动条件的属性窗口**

### <a name="component-ids-of-the-primary-interop-assemblies-for-microsoft-office"></a>用于Microsoft Office的主互操作程序集的组件 ID

|主互操作程序集|Office 2010|Office 2013|Office 2013 (64 位) |Office 2016|Office 2016 (64 位) |
|------------------------|------------------------|------------------------|------------------------|------------------------|------------------------|
|Excel|{EA7564AC-C67D-4868-BE5C-26E4FC2223FF}|{C8A65ABE-3270-4FD7-B854-50C8082C8F39}|{E3BD1151-B9CA-4D45-A77E-51A6E0ED322A}|{C845E028-E091-442E-8202-21F596C559A0}|{C4ACE6DB-AA99-401F-8BE6-8784BD09F003}|
|InfoPath|{4153F732-D670-4E44-8AB7-500F2B576BDA}|{0F825A16-25B2-4771-A497-FC8AF3B355D8}|{C5BBD36E-B320-47EF-A512-556B99CB7E41}|-|-|
|Outlook|{1D844339-3DAE-413E-BC13-62D6A52816B2}|{F9F828D5-9F0B-46F9-9E3E-9C59F3C5E136}|{7824A03F-28CC-4371-BC54-93D15EFC1E7F}|{2C6C511D-4542-4E0C-95D0-05D4406032F2}|{7C6D92EF-7B45-46E5-8670-819663220E4E}|
|PowerPoint|{EECBA6B8-3A62-44AD-99EB-8666265466F9}|{813139AD-6DAB-4DDD-8C6D-0CA30D073B41}|{05758318-BCFD-4288-AD8D-81185841C235}|{9E73CEA4-29D0-4D16-8FB9-5AB17387C960}|{E0A76492-0FD5-4EC2-8570-AE1BAA61DC88}|
|Visio|{3EA123B5-6316-452E-9D51-A489E06E2347}|{C1713368-12A8-41F1-ACA1-934B01AD6EEB}|{2CC0B221-22D2-4C15-A9FB-DE818E51AF75}|{A4C55BC1-B94C-4058-B15C-B9D4AE540AD1}|{2D4540EC-2C88-4C28-AE88-2614B5460648}|
|Word|{8B74A499-37F8-4DEA-B5A0-D72FC501CEFA}|{9FE736B7-B1EE-410C-8D07-082891C3DAC8}|{13C07AF5-B206-4A48-BB5B-B8022333E3CA}|{30CAC893-3CA4-494C-A5E9-A99141352216}|{DC5CCACD-A7AC-4FD3-9F70-9454B5DE5161}|
|Microsoft Forms 2.0|{B2279272-3FD2-434D-B94E-E4E0F8561AC4}|{B2279272-3FD2-434D-B94E-E4E0F8561AC4}|{A5A30117-2D2A-4C5C-B3C8-8897AC32C2AC}|-|-|
|Microsoft Graph|{011B9112-EBB1-4A6C-86CB-C2FDC9EA7B0E}|{52DA4B37-B8EB-4B7F-89C1-824654CE4C70}|{24706F33-F0CE-4EB4-BC91-9E935394F510}|-|-|
|智能标记 (Smart Tag)|{7102C98C-EF47-4F04-A227-FE33650BF954}|{487A7921-EB3A-4262-BB5B-A5736B732486}|{74EFC1F9-747D-4867-B951-EFCF29F51AF7}|-|-|
|共享Office|{64E2917E-AA13-4CA4-BFFE-EA6EDA3AFCB4}|{6A174BDB-0049-4D1C-86EF-3114CB0C4C4E}|{76601EBB-44A7-49EE-8DE3-7B7B9D7EBB05}|{68477CB0-662A-48FB-AF2E-9573C92869F7}|{625F5772-C1B3-497E-8ABE-7254EDB00506}|
|Project|{957A4EC0-E67B-4E86-A383-6AF7270B216A}|{1C50E422-24FA-44A9-A120-E88280C8C341}|{706D7F44-8231-489D-9B25-3025ADE9F114}|{0B6EDA1D-4A15-4F88-8B20-EA6528978E4E}|{107BCD9A-F1DC-4004-A444-33706FC10058}|

  ![最终启动条件的屏幕截图](media/setup-project-figure-11.jpg)

  **图 11：最终启动条件**

可以进一步优化 ExcelAddIn 安装的启动条件。 例如，检查是否安装了实际目标Office应用程序可能很有用。

### <a name="to-build-the-setup-project"></a>生成安装项目

1. 在 **解决方案资源管理器** 中，右键单击 **OfficeAddInSetup** 项目，然后单击“**生成**”。
2. 使用 **Windows资源管理器**，导航到 **OfficeAddInSetup** 项目的输出目录，并转到“发布”或“调试”文件夹，具体取决于所选生成配置。 将所有文件从文件夹复制到用户可以访问的位置。

测试 ExcelAddIn 设置

1. 导航到将 **OfficeAddInSetup** 复制到的位置。
2. 双击setup.exe文件以安装 **OfficeAddInSetup** 加载项。 接受显示的任何软件许可条款，并完成安装向导以在用户计算机上安装加载项。

Excel Office解决方案应从安装期间指定的位置安装和运行。

## <a name="additional-requirements-for-document-level-solutions"></a>文档级解决方案的其他要求

部署文档级解决方案需要在 Windows Installer 安装项目中执行几个不同的配置步骤。

下面是部署文档级解决方案所需的基本步骤列表：

- 创建Visual Studio安装程序Project。
- 添加文档级解决方案的主输出。 主输出还包括Microsoft Office文档。
- 将部署和应用程序清单添加为松散文件。
- 从安装程序包中排除依赖组件 (除任何实用工具程序集) 除外。
- 配置必备包。
- 配置启动条件。
- 生成安装项目并将结果复制到部署位置。
- 通过执行安装程序，在用户计算机上部署文档级解决方案。
- 如果需要，请更新自定义文档属性。

### <a name="changing-the-location-of-the-deployed-document"></a>更改已部署文档的位置

Office文档中的属性用于查找文档级别解决方案。 如果文档安装到 VSTO 程序集所在的同一文件夹中，则无需更改。 但是，如果它安装到不同的文件夹，则需要在安装过程中更新这些属性。

有关这些文档属性的详细信息，请参阅 [自定义文档属性概述](custom-document-properties-overview.md)。

若要更改这些属性，需要在设置过程中使用自定义操作。

以下示例使用名为 ExcelWorkbookProject 的文档级解决方案和名为 ExcelWorkbookSetup 的设置项目。 ExcelWorkbookSetup 项目使用上述相同步骤进行配置，但设置注册表项除外。

将自定义操作项目添加到Visual Studio解决方案

1. 通过右键单击 **解决方案资源管理器中的Office文档部署Project**，将新的 .NET 控制台项目添加到解决方案
2. 展开 **“添加**”并单击“**新建Project**”。
3. 选择控制台应用模板，并将项目命名 **为 AddCustomizationCustomAction**。

    ![解决方案资源管理器的屏幕截图 - AddCustomizationCustomAction](media/setup-project-figure-15.jpg)
  
    **图 12：解决方案资源管理器 - AddCustomizationCustomAction**

4. 添加对这些程序集的引用：
    1. System.ComponentModel
    2. System.Configuration.Install
    3. Microsoft.VisualStudio.Tools.Applications
    4. Microsoft.VisualStudio.Tools.Applications.ServerDocument

5. 将此代码复制到 Program.cs 或 Program.vb

```csharp
    using System;
    using System.IO;
    using System.Collections;
    using System.ComponentModel;
    using System.Configuration.Install;
    using Microsoft.VisualStudio.Tools.Applications;
    using Microsoft.VisualStudio.Tools.Applications.Runtime;

    namespace AddCustomizationCustomAction
    {
        [RunInstaller(true)]
        public class AddCustomizations : Installer
        {
            public AddCustomizations() : base() { }

            public override void Install(IDictionary savedState)
            {
                base.Install(savedState);

                //Get the CustomActionData Parameters
                string documentLocation = Context.Parameters.ContainsKey("documentLocation") ? Context.Parameters["documentLocation"] : String.Empty;
                string assemblyLocation = Context.Parameters.ContainsKey("assemblyLocation") ? Context.Parameters["assemblyLocation"] : String.Empty;
                string deploymentManifestLocation = Context.Parameters.ContainsKey("deploymentManifestLocation") ? Context.Parameters["deploymentManifestLocation"] : String.Empty;
                Guid solutionID = Context.Parameters.ContainsKey("solutionID") ? new Guid(Context.Parameters["solutionID"]) : new Guid();

                string newDocLocation = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments), Path.GetFileName(documentLocation));

                try
                {
                    //Move the file and set the Customizations
                    if (Uri.TryCreate(deploymentManifestLocation, UriKind.Absolute, out Uri docManifestLocationUri))
                    {
                        File.Move(documentLocation, newDocLocation);
                        ServerDocument.RemoveCustomization(newDocLocation);
                        ServerDocument.AddCustomization(newDocLocation, assemblyLocation,
                                                        solutionID, docManifestLocationUri,
                                                        true, out string[] nonpublicCachedDataMembers);
                    }
                    else
                    {
                        LogMessage("The document could not be customized.");
                    }
                }
                catch (ArgumentException)
                {
                    LogMessage("The document could not be customized.");
                }
                catch (DocumentNotCustomizedException)
                {
                    LogMessage("The document could not be customized.");
                }
                catch (InvalidOperationException)
                {
                    LogMessage("The customization could not be removed.");
                }
                catch (IOException)
                {
                    LogMessage("The document does not exist or is read-only.");
                }
            }

            public override void Rollback(IDictionary savedState)
            {
                base.Rollback(savedState);
                DeleteDocument();
            }
            public override void Uninstall(IDictionary savedState)
            {
                base.Uninstall(savedState);
                DeleteDocument();
            }
            private void DeleteDocument()
            {
                string documentLocation = Context.Parameters.ContainsKey("documentLocation") ? Context.Parameters["documentLocation"] : String.Empty;

                try
                {
                    File.Delete(Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments), Path.GetFileName(documentLocation)));
                }
                catch (Exception)
                {
                    LogMessage("The document doesn't exist or is read-only.");
                }
            }
            private void LogMessage(string Message)
            {
                if (Context.Parameters.ContainsKey("LogFile"))
                {
                    Context.LogMessage(Message);
                }
            }

            static void Main() { }
            }
    }
```

若要向文档添加自定义项，需要具有 VSTO 文档级解决方案的解决方案 ID。 此值是从Visual Studio项目文件中检索的。

检索解决方案 ID

1. 在 **“生成** ”菜单上，单击“ **生成解决方案** ”以生成文档级解决方案，并将解决方案 ID 属性添加到项目文件。
2. 在 **解决方案资源管理器** 中，右键单击文档级项目 **ExcelWorkbookProject**
3. 单击 **UnloadProject** 从Visual Studio内部访问项目文件。

    ![解决方案资源管理器卸载Excel文档解决方案的屏幕截图](media/setup-project-figure-16.jpg)

    **图 13：卸载文档解决方案Excel**

4. 在 **解决方案资源管理器** 中，右键单击 ExcelWorkbookProject，然后单击 **EditExcelWorkbookProject.vbproj** 或 **Edit ExcelWorkbookProject.csproj**。
5. 在 **ExcelWorkbookProject** 编辑器中，找到 **PropertyGroup** 元素内的 **SolutionID** 元素。
6. 复制此元素的 GUID 值。

    ![检索 SolutionID](media/setup-project-figure-17.jpg)

    **图 14：检索 SolutionID**

7. 在 **解决方案资源管理器** 中，右键单击 **ExcelWorkbookProject** 并单击 **“重新加载”Project**。
8. 在出现的对话框中单击 **“是** ”以关闭 **ExcelWorkbookProject** 编辑器。
9. **解决方案 ID** 将在安装自定义操作中使用。

最后一步是为 **安装和****卸载** 步骤配置自定义操作。

### <a name="to-configure-the-setup-project"></a>配置安装项目

1. 在 **解决方案资源管理器** 中，右键单击 **ExcelWorkbookSetup**，展开 **“添加**”并单击“**Project输出**”。
2. 在 **“添加Project输出组**”对话框中的 **Project** 列表中，单击 **“AddCustomizationCustomAction**”。
3. 选择 **“主输出** ”，然后单击“ **确定** ”关闭对话框，并将包含自定义操作的程序集添加到安装项目。

    ![“文档清单自定义操作 - 添加Project输出组”窗口的屏幕截图](media/setup-project-figure-18.jpg)

    **图 15：文档清单自定义操作 - 添加Project输出组**

4. 在 **解决方案资源管理器** 中，右键单击 **ExcelWorkbookSetup**。
5. 展开 **“视图** ”，然后单击“ **自定义操作**”。
6. 在 **ExcelWorkbookSetup) 编辑器的“自定义操作 (”中** ，右键单击 **“自定义操作** ”，然后单击“ **添加自定义操作**”。
7. 在Project对话框中的 **“****查找** 项”列表中，单击“**应用程序文件夹**”。 **从 AddCustomizationCustomAction (活动) 中选择主输出**，然后单击“**确定**”将自定义操作添加到“安装”步骤。
8. 在 **“安装”节点** 下，右键单击 **AddCustomizationCustomAction (Active) 的主输出**，然后单击“ **重命名**”。 将自定义操作 **“复制文档”命名为“我的文档”并附加自定义** 项。
9. 在 **“卸载”节点** 下，右键单击 **AddCustomizationCustomAction (Active) 的主输出** ，然后单击“ **重命名**”。 将自定义操作命名 **为“从文档”文件夹中删除文档**。

    ![“文档清单自定义操作”窗口的屏幕截图](media/setup-project-figure-19.jpg)

    **图 16：文档清单自定义操作**

10. 在 **ExcelWorkbookSetup) 编辑器 (自定义操作** 中，右键单击 **“将文档复制到我的文档”并附加自定义** 项，然后单击“ **属性”窗口**。
11. 在 **CustomActionData** **属性** 窗口中，输入自定义 DLL、部署清单和Microsoft Office文档的位置。 还需要 SolutionID。
12. 如果要将任何安装错误记录到文件中，请包含 LogFile 参数。
s
    ``` text
    /assemblyLocation="[INSTALLDIR]ExcelWorkbookProject.dll" /deploymentManifestLocation="[INSTALLDIR]ExcelWorkbookProject.vsto" /documentLocation="[INSTALLDIR]ExcelWorkbookProject.xlsx" /solutionID="Your Solution ID" /LogFile="[TARGETDIR]Setup.log"
    ```

    ![将文档复制到我的文档的自定义操作的屏幕截图属性窗口](media/setup-project-figure-20.jpg)

    **图 17：将文档复制到“我的文档”的自定义操作**

13. 卸载的自定义操作需要文档的名称，可以通过在 **CustomActionData** 中使用同一 documentLocation 参数来提供该名称

    ``` text
    /documentLocation="[INSTALLDIR]ExcelWorkbookProject.xlsx"
    ```

14. 编译并部署 **ExcelWorkbookSetup** 项目。
15. 在 **“我的文档”** 文件夹中查找并打开ExcelWorkbookProject.xlsx文件。

## <a name="additional-resources"></a>其他资源

[如何：安装Visual Studio Tools for Office运行时](how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)

[Office Primary Interop Assemblies](office-primary-interop-assemblies.md)

[VSTO 外接程序的注册表项](registry-entries-for-vsto-add-ins.md)

[Custom Document Properties Overview](custom-document-properties-overview.md)

[在Windows注册表中指定窗体区域](/office/vba/outlook/concepts/creating-form-regions/specifying-form-regions-in-the-windows-registry)

[Granting Trust to Documents](granting-trust-to-documents.md)

## <a name="about-the-authors"></a>关于作者

Wouter van Vugt 是具有 Office Open XML 技术的 Microsoft MVP，是一位独立顾问，专注于使用 SharePoint、Microsoft Office 和相关 .NET 技术) 创建 Office Business Applications (OBA。
Wouter 是开发人员社区网站（如 [MSDN](/previous-versions/office/developer/office-2007/bb879915(v=office.12))）的频繁参与者。 他出版了几篇白皮书和文章，以及一本名为 Open XML 的在线书籍：解释电子书。
Wouter 是代码律师的创始人，该公司是荷兰公司，专注于通过各种渠道交付尖端技术内容。 你可以阅读他的博客来了解有关 Wouter 的更多信息。

泰德·帕蒂森是 SharePoint MVP、作者、教练员和泰德·帕蒂森集团的创始人。 2005年秋季，Ted 被 Microsoft 开发人员平台福音派组织聘请，创作 Windows SharePoint Services 3.0 和 Microsoft Office SharePoint Server 2007 的 Ascend 开发人员培训课程。 此后，Ted 一直专注于在 SharePoint 2007 技术上教育专业开发人员。 Ted 已完成撰写一本名为“内部 Windows SharePoint Services 3.0”的 Microsoft Press 书籍，重点介绍如何将 SharePoint 用作构建业务解决方案的开发平台。 Ted 还为名为 Office Space 的 MSDN 杂志编写了一个以开发人员为中心的专栏。
