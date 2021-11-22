---
title: 指定要发布的文件 (ClickOnce)
description: 了解如何排除文件，将文件标记为数据文件或系统必备组件，以及为 ClickOnce 应用程序的条件安装创建组。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- Microsoft.VisualStudio.Publish.BaseProvider.Dialog.File
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, file exclusion
- files, publishing via ClickOnce
ms.assetid: 579c134a-d50f-4e0c-8e05-2a4ff654896a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: c6fbe8b1543fdff870a0a5557c313080acd390c8
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664137"
---
# <a name="how-to-specify-which-files-are-published-by-clickonce"></a>如何：指定通过 ClickOnce 发布的文件
在发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，会将项目中的所有非代码文件与应用程序一起部署。 在某些情况下，你可能不希望或不需要发布某些文件，或者你可能想要根据条件安装某些文件。 Visual Studio 提供了一些功能，可用于排除文件，将文件标记为数据文件或系统必备组件，以及为条件安装创建文件组。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的文件是在“应用程序文件”对话框中管理的，可以从“项目设计器”的“发布”页进行访问  。

 最初，只有一个名为“(必需)”的文件组。 你可以创建其他文件组并向其分配文件。 对于应用程序运行所需的文件，不能更改“下载组”。 例如，应用程序的 .exe 或标记为数据文件的文件必须属于“(必需)”组。

 文件的默认发布状态值用“(自动)”进行标记。 例如，默认情况下，应用程序的 .exe 的发布状态为“包含(自动)”。

 “生成操作”属性设置为“内容”的文件被指定为应用程序文件，并且默认将被标记为“已包含”。  它们可以被包含、排除，或被标记为数据文件。 下面列出了例外情况：

- 数据文件，如 SQL 数据库（.mdf 和 .mdb）文件和 XML 文件将被默认标记为数据文件。 

- 对程序集（.dll 文件）的引用在你添加引用时被指定如下：如果“本地复制”为“False”，它默认被标记为系统必备程序集（“系统必备(自动)”），在安装应用程序之前必须存在于 GAC 中。   如果“本地复制”为“True”，则默认情况下，程序集被标记为应用程序的程序集（“包含(自动)”），并将在安装时被复制到应用程序文件夹中。   只有当一个 COM 引用的“独立”属性被设置为“True”时，它才会出现在“应用程序文件”对话框中（作为一个 .ocx 文件）。  默认情况下，它将被包括在内。

### <a name="to-add-files-to-the-application-files-dialog-box"></a>将文件添加到“应用程序文件”对话框

1. 在“解决方案资源管理器”中，选择一个数据文件。

2. 在“属性”窗口中，将“生成操作”属性更改为“Content”值。 。

### <a name="to-exclude-files-from-clickonce-publishing"></a>从 ClickOnce 发布中排除文件

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击“应用程序文件”按钮以打开“应用程序文件”对话框 。

4. 在“应用程序文件”对话框中，选择要排除的文件。

5. 在“发布状态”字段的下拉列表中，选择“排除”。 

### <a name="to-mark-files-as-data-files"></a>将文件标记为数据文件

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击“应用程序文件”按钮以打开“应用程序文件”对话框 。

4. 在“应用程序文件”对话框中，选择要标记为数据的文件。

5. 在“发布状态”字段的下拉列表中，选择“数据文件”。 

### <a name="to-mark-files-as-prerequisites"></a>将文件标记为系统必备组件

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击“应用程序文件”按钮以打开“应用程序文件”对话框 。

4. 在“应用程序文件”对话框中，选择要标记为系统必备组件的应用程序程序集（.dll 文件）。 请注意，应用程序必须具有对应用程序程序集的引用，才能使其显示在列表中。

5. 在“发布状态”字段的下拉列表中，选择“必备组件”。 

### <a name="to-add-a-new-file-group"></a>添加新的文件组

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击“应用程序文件”按钮以打开“应用程序文件”对话框 。

4. 在“应用程序文件”对话框中，选择要包含在新组中的文件的“组”字段。 

    > [!NOTE]
    > 在文件名出现在“应用程序文件”对话框中之前，文件的“生成操作”属性必需设置为“Content”。  

5. 在“下载组”字段的下拉列表中，选择“\<New...>”。 

6. 在“新建组”对话框中，输入组的名称，然后单击“确定”。 

### <a name="to-add-a-file-to-a-group"></a>向组中添加文件

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击“应用程序文件”按钮以打开“应用程序文件”对话框 。

4. 在“应用程序文件”对话框中，选择要包含在新组中的文件的“组”字段。 

5. 在“下载组”字段的下拉列表中，选择一个组。

    > [!NOTE]
    > 对于应用程序运行所需的文件，不能更改“下载组”。

## <a name="see-also"></a>另请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)