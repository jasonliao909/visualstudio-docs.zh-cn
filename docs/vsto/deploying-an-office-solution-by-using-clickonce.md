---
title: 使用 ClickOnce 部署 Office 解决方案
description: 如果你使用 ClickOnce，请参阅如何更少的步骤来部署 Office 解决方案。 如果发布更新，解决方案将自动检测并安装更新。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, deploying solutions
- ClickOnce deployment [Office development in Visual Studio], deploying solutions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 84c3740a1fd51863c782942a12d9863d3bf448c85379f89b82268a01847f0b44
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121297043"
---
# <a name="deploy-an-office-solution-by-using-clickonce"></a>使用 ClickOnce 部署 Office 解决方案
  如果使用 ClickOnce，则部署 Office 解决方案的步骤更少。 如果发布更新，解决方案将自动检测并安装更新。 不过，ClickOnce 需要你分别为计算机的每个用户安装解决方案。 因此，如果多个用户将在同一台计算机上运行你的解决方案，则应考虑使用 Windows Installer (*.msi*) 。

## <a name="in-this-topic"></a>本主题内容

- [发布解决方案](#Publish)

- [决定如何向解决方案授予信任](#Trust)

- [帮助用户安装解决方案](#Helping)

- [将解决方案文档置于最终用户计算机上（仅限文档级自定义项）](#Put)

- [将解决方案文档置于运行 SharePoint 的服务器上（仅限文档级自定义项）](#SharePoint)

- [创建自定义安装程序](#Custom)

- [发布更新](#Update)

- [更改解决方案的安装位置](#Location)

- [将解决方案回滚到早期版本](#Roll)

  有关如何通过创建 Windows Installer 文件来部署 Office 解决方案的详细信息，请参阅[使用 Windows Installer 部署 Office 解决方案](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)。

## <a name="publish-the-solution"></a><a name="Publish"></a> 发布解决方案
 您可以使用 **发布向导** 或 **Project 设计器** 发布您的解决方案。 在此过程中，您将使用 **Project 设计器**，因为它提供了一组完整的发布选项。 请参阅[发布向导 &#40;Visual Studio&#41;中 Office 开发](../vsto/publish-wizard-office-development-in-visual-studio.md)。

#### <a name="to-publish-the-solution"></a>发布解决方案

1. 在 **解决方案资源管理器** 中，选择为你的项目命名的节点。

2. 在菜单栏上，依次选择 " **Project**"、"*项目名称*" "**属性**"。

3. 在 **Project 设计器** 中，选择 "**发布**" 选项卡，如下图所示。

    ![项目设计器中的“发布”选项卡](../vsto/media/vsto-publishtab.png "项目设计器中的“发布”选项卡")

4. 在 "**发布文件夹位置 (ftp 服务器或文件路径)** " 框中，输入要在其中 **Project 设计器** 将解决方案文件复制到的文件夹的路径。

    可以输入以下任一类型的路径。

   - 本地路径 (例如 *C:\FolderName\FolderName*) 。

   - 统一命名约定 (网络上的文件夹的 UNC) 路径 (例如， *\\ \ServerName\FolderName*) 。

   - 相对路径 (例如 *PublishFolder \\*，默认情况下，该项目将发布到该文件夹) 。

5. 在 " **安装文件夹 URL** " 框中，输入最终用户将在其中找到解决方案的位置的完全限定路径。

    如果你不知道该位置，请不要在此字段中输入任何内容。 默认情况下，ClickOnce 将在用户从中安装解决方案的文件夹中查找更新。

6. 选择 **“系统必备”** 按钮。

7. 在 " **系统必备** " 对话框中，确保已选中 " **创建用于安装系统必备组件的安装程序** " 复选框。

8. 在 "**选择要安装的系统必备组件**" 列表中，选中 **Windows Installer 4.5** 和相应 .NET Framework 包的复选框。

    例如，如果你的解决方案面向 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] ，则选中 **Windows Installer 4.5** 和 **Microsoft .NET Framework 4.5 Full** 的复选框。

9. 如果你的解决方案面向 .NET Framework 4.5，还请选择 " **Visual Studio 2010 Tools for Office Runtime** " 复选框。

    > [!NOTE]
    > 默认情况下，不会显示此复选框。 若要显示此复选框，必须创建引导程序包。 请参阅[使用 Visual Studio 2012 为 Office 2013 VSTO 外接程序创建引导程序包](create-vsto-add-ins-for-office-by-using-visual-studio.md)。

10. 在 " **指定系统必备组件的安装位置**" 下，选择显示的选项之一，然后选择 " **确定"** 按钮。

     下表对每个选项进行了描述。

    |选项|说明|
    |------------|-----------------|
    |**从组件供应商的网站下载系统必备组件**|系统将提示用户从供应商处下载并安装这些系统必备组件。|
    |**从与我的应用程序相同的位置下载系统必备组件**|系统必备软件与解决方案一起安装。 如果选择此选项，Visual Studio 会将所有系统必备组件包为你复制到发布位置。 要让此选项正常工作，系统必备包必须位于开发计算机上。|
    |**从下列位置下载系统必备组件**|Visual Studio 将所有系统必备组件包复制到你指定的位置，并与解决方案一起安装。|

     请参阅 [先决条件对话框](../ide/reference/prerequisites-dialog-box.md)。

11. 选择 "**更新**" 按钮，指定你希望每个最终用户 VSTO 外接程序或自定义项检查更新的频率，然后选择 **"确定"** 按钮。

    > [!NOTE]
    > 如果要使用 CD 或可移动驱动器进行部署，请选择 " **从不检查更新** " 选项按钮。

     有关如何发布更新的信息，请参阅 [发布更新](#Update)。

12. 选择 " **选项** " 按钮，查看 " **选项** " 对话框中的选项，然后选择 " **确定"** 按钮。

13. 选择 " **立即发布** " 按钮。

     Visual Studio 将向你先前在此过程中指定的发布文件夹添加以下文件夹和文件。

    - **应用程序文件** 文件夹。

    - 安装程序。

    - 部署清单，指向最新版本的部署清单。

      " **应用程序文件** " 文件夹包含您发布的每个版本的子文件夹。 每个特定于版本的子文件夹均包含以下文件。

    - 应用程序清单。

    - 部署清单。

    - 自定义程序集。

      下图显示了 Outlook VSTO 外接程序的发布文件夹的结构。

      ![发布文件夹结构](../vsto/media/publishfolderstructure.png "发布文件夹结构")

    > [!NOTE]
    > ClickOnce 将 *.deploy* 扩展名追加到程序集，以便 (IIS) 的 Internet Information Services 的安全安装不会阻止文件，因为这是不安全的扩展。 当用户安装解决方案时，ClickOnce 会删除 *.deploy* 扩展。

14. 将解决方案文件复制到你先前在此过程中指定的安装位置。

## <a name="decide-how-you-want-to-grant-trust-to-the-solution"></a><a name="Trust"></a> 决定要如何向解决方案授予信任
 要让解决方案在用户计算机上运行，你必须授予信任，或用户必须在安装解决方案时响应信任提示。 要向解决方案授予信任，请使用能识别已知受信任发布者的证书为清单签名。 请参阅 [通过对应用程序清单和部署清单进行签名来信任解决方案](../vsto/granting-trust-to-office-solutions.md#Signing)。

 如果你正在部署文档级自定义项，并且想要将文档放入用户计算机上的文件夹，或使文档在 SharePoint 网站上可用，请确保 Office 信任文档的位置。 请参阅 [向文档授予信任](../vsto/granting-trust-to-documents.md)。

## <a name="help-users-install-the-solution"></a><a name="Helping"></a> 帮助用户安装解决方案
 用户可以通过运行安装程序、打开部署清单或在文档级自定义项中直接打开文档来安装解决方案。 作为最佳做法，用户应使用安装程序来安装解决方案。 其他两种方法不能确保安装了必备软件。 如果用户希望从安装位置打开文档，则必须将此文档添加到 Office 应用程序信任中心的受信任位置列表。

### <a name="opening-the-document-of-a-document-level-customization"></a>打开文档级自定义项的文档
 若要打开文档集自定义项的文档，用户可以直接将其从安装位置打开，也可以将此文档复制到本地计算机并打开副本。

 作为最佳做法，用户应打开其计算机上的文档副本，这样，多个用户不会同时尝试打开同一文档。 要实施此做法，可以将安装程序配置为将文档复制到用户计算机。 请参阅 [将解决方案文档放到最终用户的计算机上 (仅) 文档级自定义项 ](#Put)。

### <a name="install-the-solution-by-opening-the-deployment-manifest-from-an-iis-website"></a>通过从 IIS 网站打开部署清单来安装解决方案
 用户可以通过从 Web 打开部署清单来安装 Office 解决方案。 但是，Internet Information Services (IIS) 的安全安装将会阻止具有 *.vsto* 扩展名的文件。 要使用 IIS 来部署 Office 解决方案，必须在 IIS 中定义 MIME 类型。

##### <a name="to-add-the-vsto-mime-type-to-iis-60"></a>向 IIS 6.0 添加 .vsto MIME 类型

1. 在运行 iis 6.0 的服务器上，选择 "**启动**  >  **所有程序**" "  >  **管理工具**"  >   **Internet Information Services (IIS) 管理器**"。

2. 选择要配置的计算机名称、 **"网站" 文件夹或** 网站。

3. 在菜单栏上，选择 "**操作**  >  **属性**"。

4. 在 **"HTTP 标头"** 选项卡上，选择 **"MIME 类型"** 按钮。

5. 在 **"MIME 类型"** 窗口中，选择"新建 **"** 按钮。

6. 在 **"MIME 类型** "窗口中，输入 **.vsto** 作为扩展，输入 **application/x-ms-vsto** 作为 MIME 类型，然后应用新设置。

    > [!NOTE]
    > 为使更改生效，必须重新启动万维网发布服务或者等待工作进程回收。 然后，必须刷新浏览器的磁盘缓存，然后再次尝试 *打开 .vsto* 文件。

##### <a name="to-add-the-vsto-mime-type-to-iis-70"></a>向 IIS 7.0 添加 .vsto MIME 类型

1. 在运行 IIS 7.0 的服务器上，选择"**启动**  >  **所有程序**  >  **附件"。**

2. 打开命令提示符 **的快捷菜单**，然后选择"  **以管理员模式运行"。**

3. 在" **打开** "框中，输入以下路径，然后选择"确定 **"** 按钮。

    ```cmd
    %windir%\system32\inetsrv
    ```

4. 输入以下命令，然后应用新设置。

    ```cmd
    set config /section:staticContent /+[fileExtension='.vsto',mimeType='application/x-ms-vsto']
    ```

    > [!NOTE]
    > 为使更改生效，必须重新启动万维网发布服务或者等待工作进程回收。 然后，必须刷新浏览器的磁盘缓存，然后再次尝试 *打开 .vsto* 文件。

## <a name="put-the-document-of-a-solution-onto-the-end-users-computer-document-level-customizations-only"></a><a name="Put"></a> 将解决方案的文档放在最终用户的计算机上， (文档级自定义) 
 可以通过创建部署后操作，将解决方案的文档复制到最终用户的计算机上。 这样，用户安装解决方案后，就不必手动将文档从安装位置复制到其计算机。 必须创建一个类，用于定义部署后操作、生成和发布解决方案、修改应用程序清单，以及重新对应用程序和部署清单进行签名。

 以下过程假定项目名称为 **ExcelWorkbook，** 并且将解决方案发布到计算机上名为 **C：\publish** 的已创建文件夹中。

### <a name="create-a-class-that-defines-the-post-deployment-action"></a>创建定义后期部署操作的类

1. 在菜单栏上，选择"**文件**  >  **""**  >  **添加新Project"。**

2. 在"**添加新Project"** 对话框中的"已安装的模板 **"窗格中，** 选择 **Windows文件夹。**

3. 在" **模板"窗格中** ，选择" **类库"** 模板。

4. 在" **名称"** 字段中，输入 **"FileCopyPDA"，** 然后选择"确定 **"** 按钮。

5. 在 **解决方案资源管理器** 中，选择 **FileCopyPDA** 项目。

6. 在菜单栏上，选择“项目” > “添加引用”。

7. 在 **".NET"** 选项卡上，添加对 和 `Microsoft.VisualStudio.Tools.Applications.Runtime` 的引用 `Microsoft.VisualStudio.Tools.Applications.ServerDocument` 。

8. 将类重命名为 `FileCopyPDA`，然后使用代码替换文件内容。 此代码执行以下任务：

   - 将文档复制到用户桌面。

   - 将 _AssemblyLocation属性从部署清单的相对路径更改为完全限定的路径。

   - 如果用户卸载此解决方案，则删除该文件。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_excelworkbookpda/filecopypda/class1.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_excelworkbookpda/filecopypda/class1.cs" id="Snippet7":::

### <a name="build-and-publish-the-solution"></a>生成并发布解决方案

1. 在 **解决方案资源管理器** 中，打开 **FileCopyPDA** 项目的快捷菜单，然后选择"生成 **"。**

2. 打开 **ExcelWorkbook** 项目的快捷菜单，然后选择"生成 **"。**

3. 打开 **ExcelWorkbook** 项目的快捷菜单，然后选择"添加 **引用"。**

4. 在" **添加引用** "对话框中，选择" **项目** "选项卡，选择 **"FileCopyPDA"，** 然后选择"确定 **"** 按钮。

5. 在 **解决方案资源管理器** 中，选择 **ExcelWorkbook** 项目。

6. 在菜单栏上，选择 **"Project**  >  **文件夹"。**

7. 输入 **"数据**"，然后选择 **Enter** 键。

8. 在 **解决方案资源管理器"** 中，选择 **"数据"** 文件夹。

9. 在菜单栏上，选择 **"Project**  >  **添加现有项"。**

10. 在" **添加现有项** "对话框中，浏览到 **ExcelWorkbook** **项目** 的输出目录，选择ExcelWorkbook.xlsx文件，然后选择"添加 **"** 按钮。

11. 在 **解决方案资源管理器****选择ExcelWorkbook.xlsx文件**。

12. 在"**属性"** 窗口中，将"**生成操作**"属性更改为 **"内容**"，将"复制到 **输出目录"** 属性更改为 **"如果较新则复制"。**

     完成这些步骤后，项目将如下图所示。

     ![部署后操作的项目结构。](../vsto/media/vsto-postdeployment.png "部署后操作的项目结构。")

13. 发布 **ExcelWorkbook** 项目。

### <a name="modify-the-application-manifest"></a>修改应用程序清单

1. 使用 文件资源管理器 打开解决方案 **目录** **c：\publish**。

2. 打开 **"应用程序文件** "文件夹，然后打开与解决方案的最新发布版本相对应的文件夹。

3. 在 **ExcelWorkbook.dll编辑器（** 如 记事本）中打开 记事本。

4. 在 `</vstav3:update>` 元素之后添加以下代码。 对于 元素的类 `<vstav3:entryPoint>` 属性，请使用以下语法 *：NamespaceName.ClassName*。 在以下示例中，命名空间和类名称相同，因此生成的入口点名称为 `FileCopyPDA.FileCopyPDA`。

    ```xml
    <vstav3:postActions>
      <vstav3:postAction>
        <vstav3:entryPoint
          class="FileCopyPDA.FileCopyPDA">
          <assemblyIdentity
            name="FileCopyPDA"
            version="1.0.0.0"
            language="neutral"
            processorArchitecture="msil" />
        </vstav3:entryPoint>
        <vstav3:postActionData>
        </vstav3:postActionData>
      </vstav3:postAction>
    </vstav3:postActions>
    ```

### <a name="re-sign-the-application-and-deployment-manifests"></a>对应用程序清单和部署清单进行重新签名

1. 在 **%USERPROFILE%\Documents\Visual Studio 2013\Projects\ExcelWorkbook\ExcelWorkbook** 文件夹中，复制 **ExcelWorkbook_TemporaryKey.pfx** 证书文件，然后将其粘贴到 *PublishFolder* **\Application Files\ExcelWorkbook** \_ _MostRecentPublishedVersion_ 文件夹中。

2. 打开 Visual Studio 命令提示符，然后将目录更改为 **c：\publish\Application Files\ExcelWorkbook** \_ _MostRecentPublishedVersion_ 文件夹 (例如 **c：\publish\Application Files\ExcelWorkbook_1_0_0_4**) 。

3. 通过运行以下命令对修改的应用程序清单进行签名：

    ```cmd
    mage -sign ExcelWorkbook.dll.manifest -certfile ExcelWorkbook_TemporaryKey.pfx
    ```

     将出现“ExcelWorkbook.dll.manifest 已成功签名”消息。

4. 更改为 **c：\publish** 文件夹，然后通过运行以下命令更新部署清单并签名：

    ```cmd
    mage -update ExcelWorkbook.vsto -appmanifest "Application Files\Ex
    celWorkbookMostRecentVersionNumber>\ExcelWorkbook.dll.manifest" -certfile "Application Files\ExcelWorkbookMostRecentVersionNumber>\ExcelWorkbook_TemporaryKey.pfx"
    ```

    > [!NOTE]
    > 在上一示例中，将 MostRecentVersionNumber 替换为解决方案最近发布的版本的版本号 (例如 **1_0_0_4**) 。

     将出现“ExcelWorkbook.vsto 已成功签名”消息。

5. 将 *ExcelWorkbook.vsto* 文件复制到 **c：\publish\Application Files\ExcelWorkbook** \_ _MostRecentVersionNumber_ 目录。

## <a name="put-the-document-of-a-solution-onto-a-server-thats-running-sharepoint-document-level-customizations-only"></a><a name="SharePoint"></a>将解决方案的文档放在运行文档级自定义SharePoint (的服务器上) 
 可以使用 SharePoint 将文档级自定义项发布到最终用户。 当用户转到 SharePoint 站点并打开文档时，运行时会将解决方案从共享网络文件夹自动安装到用户的本地计算机。 将解决方案安装到本地后，即使将文档复制到其他位置（例如桌面），自定义项仍可正常工作。

#### <a name="to-put-the-document-on-a-server-thats-running-sharepoint"></a>将文档置于运行 SharePoint 的服务器上

1. 将解决方案文档添加到 SharePoint 站点上的某个文档库中。

2. 执行以下一种方法的步骤：

    - 使用 Office 配置工具将运行 SharePoint 的服务器添加到所有用户计算机上 Word 或 Excel 中的信任中心。

         请参阅[2010 Office中的安全策略和设置](/previous-versions/office/office-2010/cc178946(v=office.14))。

    - 确保每个用户执行以下步骤。

        1. 在本地计算机上，打开 Word 或 Excel，选择"文件 **"** 选项卡，然后选择"选项 **"** 按钮。

        2. 在" **信任中心"** 对话框中，选择" **受信任的位置"** 按钮。

        3. 选中" **允许网络上** 受信任的位置 (建议) "复选框，然后选择"添加新 **位置"** 按钮。

        4. 在 **"路径**"框中，输入SharePoint文档库的 URL，该库包含已上传 (的文档，例如 *http://SharePointServerName/TeamName/ProjectName/DocumentLibraryName*) 。

             请勿添加默认网页的名称，例如 *default.aspx* 或 *AllItems.aspx*。

        5. 选中 **"此位置的子文件夹也受信任** "复选框，然后选择"确定 **"** 按钮。

             当用户从 SharePoint 站点打开文档时，将打开文档，并安装自定义项。 用户可将文档复制到他们的桌面。 自定义项仍将运行，因为文档中的属性指向文档的网络位置。

## <a name="create-a-custom-installer"></a><a name="Custom"></a> 创建自定义安装程序
 你可以为解决方案创建自定义安装程序Office，而不是使用发布解决方案时创建的安装程序。 例如，可以使用登录脚本启动安装，或者可以使用批处理文件来安装解决方案，而无需用户交互。 如果最终用户计算机上已安装了系统必备组件，则这些方案都能顺利实现。

 作为自定义安装过程的一部分，为默认安装在以下位置的 Office 解决方案 *(VSTOInstaller.exe)* 安装程序工具：

 *%commonprogramfiles%\microsoft shared\VSTO\10.0\VSTOInstaller.exe*

 如果该工具不位于该位置，可以使用HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSTO Runtime Setup\v4\InstallerPath或 **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VSTO Runtime Setup\v4\InstallerPath注册表项** 来查找该工具的路径。

 可以将以下参数与 *VSTOinstaller.exe。*

| 参数 | 定义 |
|------------------| - |
| /Install 或 /I | 安装解决方案。 此选项必须后跟部署清单的路径。 您可以在本地计算机上指定路径，一个通用命名约定 (UNC) 文件共享。 可以指定本地路径 (*C：\FolderName\PublishFolder*) 、相对路径 (*Publish \\*) 或完全限定的位置 (*\\ \ServerName\FolderName* 或 http://<em>ServerName/FolderName</em>) 。 |
| /Uninstall 或 /U | 卸载解决方案。 此选项必须后跟部署清单的路径。 您可以指定可以在本地计算机上的路径，一个 UNC 文件共享。 可以指定本地路径 (*c：\FolderName\PublishFolder*) 、相对路径 (*Publish \\*) 或完全限定的位置 (*\\ \ServerName\FolderName* 或 http://<em>ServerName/FolderName</em>) 。 |
| /Silent 或 /S | 在不提示用户输入或不显示任何消息的情况下进行安装或卸载。 如果需要信任提示，则自定义项不会安装或更新。 |
| /Help 或 /? | 显示帮助信息。 |

 运行 *VSTOinstaller.exe* 时，可能会出现以下错误代码。

|错误代码|定义|
|----------------|----------------|
|0|已成功安装或卸载解决方案，或者显示 VSTOInstaller 帮助。|
|-100|一个或多个命令行选项无效或已设置多次。 有关详细信息，请输入"vstoinstaller /？" 或参阅[为解决方案 创建自定义ClickOnce Office安装程序](/previous-versions/bb772078(v=vs.110))。|
|-101|一个或多个命令行选项无效。 有关详细信息，请输入“vstoinstaller /?”。|
|-200|部署清单 URI 无效。 有关详细信息，请输入“vstoinstaller /?”。|
|-201|无法安装解决方案，因为部署清单无效。 请参阅[部署清单，了解Office解决方案](../vsto/deployment-manifests-for-office-solutions.md)。|
|-202|无法安装解决方案，因为Visual Studio Tools for Office清单的 "Visual Studio Tools for Office"部分无效。 有关[解决方案，请参阅Office清单](../vsto/application-manifests-for-office-solutions.md)。|
|-203|由于发生下载错误，无法安装解决方案。 检查部署清单的 URI 或网络文件位置，然后重试。|
|-300|由于发生安全异常，无法安装解决方案。 请参阅[安全Office解决方案](../vsto/securing-office-solutions.md)。|
|-400|无法安装解决方案。|
|-401|无法卸载解决方案。|
|-500|由于未能安装或卸载解决方案，或者未能下载部署清单，操作已取消。|

## <a name="publish-an-update"></a><a name="Update"></a> 发布更新
 若要更新解决方案，可以使用"Project或发布向导"再次发布它，然后将更新的解决方案复制到安装位置。 将文件复制到安装位置时，请确保覆盖先前文件。

 解决方案下次检查更新时，会自动查找并加载新版本。

## <a name="change-the-installation-location-of-a-solution"></a><a name="Location"></a> 更改解决方案的安装位置
 可以在发布解决方案后添加或更改安装路径。 你可能需要出于以下一个或多个原因更改安装路径：

- 在编译安装程序时，安装路径未知。

- 已将解决方案文件复制到其他位置。

- 托管安装文件的服务器已具有新名称或位置。

  若要更改解决方案的安装路径，必须更新安装程序，用户随后必须运行安装程序。 对于文档级自定义项，用户还必须更新其文档中的属性以指向新位置。

> [!NOTE]
> 如果不希望要求用户更新其文档属性，可以要求用户从安装位置获取更新的文档。

#### <a name="to-change-the-installation-path-in-the-setup-program"></a>更改安装程序中的安装路径

1. 打开命令 **提示符** 窗口，然后将目录更改为安装文件夹。

2. 运行安装程序并包括 `/url` 参数，该参数采用字符串形式的新安装路径。

    以下示例演示如何将安装路径更改为 Fabrikam 网站上的位置，你也可以使用你需要的路径替换此 URL：

   ```cmd
   setup.exe /url="http://www.fabrikam.com/newlocation"
   ```

   > [!NOTE]
   > 如果显示消息，表明可执行文件的签名将无效，用于对解决方案进行签名的证书将不再有效，并且发布者未知。 因此，用户需要先确认他们信任解决方案的源，才能安装解决方案。

   > [!NOTE]
   > 若要显示 URL 的当前值，请运行 `setup.exe /url`。

   对于文档级自定义项，用户必须打开文档，然后更新其_AssemblyLocation属性。 下面的步骤描述用户如何执行此任务。

#### <a name="to-update-the-_assemblylocation-property-in-a-document"></a>更新文档中的 _AssemblyLocation 属性

1. 在" **文件"** 选项卡上，选择" **信息**"，如下图所示。

     ![Excel 中的信息选项卡](../vsto/media/vsto-infotab.png "Excel 中的信息选项卡")

2. 在" **属性"** 列表中，选择"高级 **属性**"，如下图所示。

     ![Excel 中的高级属性。](../vsto/media/vsto-advanceddocumentproperties.png "Excel 中的高级属性。")

3. 在" **属性** " **列表中的"自定义** "选项卡上，_AssemblyLocation，如下图所示。

     ![AssemblyLocation 属性。](../vsto/media/vsto-assemblylocationproperty.png "AssemblyLocation 属性。")

     " **值** "框包含部署清单标识符。

4. 在标识符之前，输入文档的完全限定路径，后跟一个栏，格式为"路径标识符 |  ("，例如 *File://ServerName/FolderName/FileName|74744e4b-e4d6-41eb-84f7-ad20346fe2d9。*

     若要详细了解如何设置此标识符的格式，请参阅 [自定义文档属性概述](../vsto/custom-document-properties-overview.md)。

5. 选择" **确定** "按钮，然后保存并关闭文档。

6. 不带 /url 参数运行安装程序，以便在指定的位置中安装解决方案。

## <a name="roll-back-a-solution-to-an-earlier-version"></a><a name="Roll"></a> 将解决方案回滚到早期版本
 在回滚解决方案时，会将用户还原到此解决方案的早期版本。

#### <a name="to-roll-back-a-solution"></a>回滚解决方案

1. 打开解决方案的安装位置。

2. 在顶级发布文件夹中，删除 *.vsto* (中的部署清单) 。

3. 找到要回滚到的版本的子文件夹。

4. 将相应部署清单从该子文件夹复制到顶级发布文件夹。

     例如，若要将名为 **OutlookAddIn1** 的解决方案从版本 1.0.0.1 回滚到版本 1.0.0.0，请从 **OutlookAddIn1_1_0_0_0** 文件夹复制 **文件 OutlookAddIn1.vsto。** 将文件粘贴到顶级发布文件夹中，覆盖已存在的 **OutlookAddIn1_1_0_0_1版本特定的** 部署清单。

     下图显示了此示例中的发布文件夹结构。

     ![发布文件夹结构](../vsto/media/publishfolderstructure.png "发布文件夹结构")

     用户下次打开应用程序或自定义文档时，系统将检测到此部署清单更改。 此 Office 解决方案的早期版本会从 ClickOnce 缓存运行。

> [!NOTE]
> 仅为解决方案的一个早期版本保存本地数据。 如果回滚两个版本，则不保留本地数据。 有关本地数据详细信息，请参阅访问应用程序 中的本地和[ClickOnce数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)。

## <a name="see-also"></a>另请参阅

- [部署Office解决方案](../vsto/deploying-an-office-solution.md)
- [发布Office解决方案](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [如何：使用 Office 发布 ClickOnce](/previous-versions/bb386095(v=vs.110))
- [如何：安装ClickOnce Office解决方案](/previous-versions/bb608592(v=vs.110))
- [如何：使用 Office 将文档级 SharePoint 解决方案发布到 ClickOnce](/previous-versions/bb608595(v=vs.110))
- [为 office 解决方案ClickOnce安装程序](/previous-versions/bb772078(v=vs.110))