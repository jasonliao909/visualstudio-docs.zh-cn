---
title: 在 Windows 窗体中创建一个简单的 WCF 服务
description: 在本演练中，请在 Visual Studio 中创建 Windows Communication Foundation (WCF) 服务，对其进行测试，然后从 Windows 窗体应用程序访问该服务。
ms.date: 11/04/2016
ms.custom: SEO-VS-2020
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- WCF, walkthrough [Visual Studio]
- WCF, Visual Studio tools for
- WCF services
- WCF services, walkthrough
ms.assetid: 5fef1a64-27a4-4f10-aa57-29023e28a2d6
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 7ccb7f38e3d459a445b7bb7712e705d1af6f3ada
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601058"
---
# <a name="walkthrough-create-a-simple-wcf-service-in-windows-forms"></a>演练：在 Windows 窗体中创建简单 WCF 服务

本演练演示如何创建一个简单的 Windows Communication Foundation (WCF) 服务，对其进行测试，然后从 Windows 窗体应用程序访问该服务。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="create-a-service"></a>创建服务

1. 打开 Visual Studio。

::: moniker range="vs-2017"

2. 在“文件”菜单上，选择“新建”>“项目”。

3. 在 "**新建 Project** " 对话框中，展开 " **Visual Basic** " 或 " **Visual c #** " 节点，然后选择 " **wcf**"，然后选择 " **wcf 服务库**"。

4. 单击“确定”以创建该项目。

   ![“WCF 服务库”项目](../data-tools/media/wcf1.png)

::: moniker-end

::: moniker range=">=vs-2019"

2. 在“开始”窗口上，选择“创建新项目”  。

3. 在 "**创建新项目**" 页上的 "搜索" 框中键入 " **wcf 服务库**"。 选择 " **WCF 服务库**" 的 "c #" 或 "Visual Basic" 模板，然后单击 "**下一步**"。

   ![在 Visual Studio 2019 中创建新的 WCF 服务库项目](media/vs-2019/create-new-wcf-service-library.png)

   > [!TIP]
   > 如果看不到任何模板，可能需要安装 Visual Studio 的 **Windows Communication Foundation** 组件。 选择 "**安装更多工具和功能**" 以打开 Visual Studio 安装程序。 选择 "**单个组件**" 选项卡，向下滚动到 "**开发活动**"，然后选择 " **Windows Communication Foundation**"。 单击“修改”。

4. 在 " **配置新项目** " 页上，单击 " **创建**"。

::: moniker-end

   > [!NOTE]
   > 这将创建可以测试和访问的工作服务。 以下两个步骤演示您可以如何修改使用不同数据类型的默认方法。 在实际应用中，您还会向服务中添加您自己的函数。

5. 在 **解决方案资源管理器** 中，双击 " **IService1** " 或 " **IService1**"。

   ![IService1 文件](../data-tools/media/wcf2.png)

   查找以下行：

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/iservice1_2.cs" id="Snippet4":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/iservice1_2.vb" id="Snippet4":::

   将参数的类型更改 `value` 为 string：

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/iservice1.cs" id="Snippet1":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/iservice1.vb" id="Snippet1":::

   在上面的代码中，请注意`<OperationContract()>`或`[OperationContract]`属性。 这些属性是由服务公开的任何方法所必需的。

6. 在 **解决方案资源管理器** 中，双击 " **Service1** " 或 " **Service1**"。

   ![Service1 文件](../data-tools/media/wcf3.png)

   查找以下行：

   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/service1_2.vb" id="Snippet5":::
   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/service1_2.cs" id="Snippet5":::

   将参数的类型更改 `value` 为 string：

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/service1.cs" id="Snippet2":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/service1.vb" id="Snippet2":::

## <a name="test-the-service"></a>测试服务

1. 按 F5 运行该服务。 **WCF 测试客户端** 窗体随即出现并加载服务。

2. 在“WCF 测试客户端”窗体中，双击 IService1 下的 GetData() 方法。 此时会显示 **"工作"** 选项卡。

     ![工作方式&#40;&#41; 方法](../data-tools/media/wcf4.png)

3. 在“请求”框中，选择“值”字段，并键入 `Hello`。

     ![“值”字段](../data-tools/media/wcf5.png)

4. 单击“调用”按钮。 如果出现 " **安全警告** " 对话框，请单击 **"确定"**。 结果将显示在 **响应** 框中。

     ![“响应”框中的结果](../data-tools/media/wcf6.png)

5. 在“文件”菜单上单击“退出”，关闭测试窗体。

## <a name="access-the-service"></a>访问服务

### <a name="reference-the-wcf-service"></a>引用 WCF 服务

1. 在 "**文件**" 菜单上，指向 "**添加**"，然后单击 "**新建 Project**"。

2. 在 "**新建 Project** " 对话框中，展开 " **Visual Basic** " 或 " **Visual c #** " 节点，选择 " **Windows**"，然后选择 " **Windows 窗体应用程序**"。 单击“确定”，打开项目。

     ![Windows 窗体应用程序项目](../data-tools/media/wcf7.png)

3. 右键单击 WindowsApplication1，然后单击“添加服务引用”。 此时将出现“添加服务引用”对话框。

4. 在 **“添加服务引用”** 对话框中，单击 **“发现”**。

     ![“添加服务引用”对话框](../data-tools/media/wcf8.png)

     **Service1** 显示在 " **服务** " 窗格中。

5. 单击“确定”，添加服务引用。

### <a name="build-a-client-application"></a>生成客户端应用程序

1. 在解决方案资源管理器中，双击 Form1.vb 或 Form1.cs，打开 Windows 窗体设计器（如果尚未打开）。

2. 从工具箱把 `TextBox` 控件、`Label` 控件和 `Button` 控件拖到窗体中。

     ![将控件添加到窗体](../data-tools/media/wcf9.png)

3. 双击 `Button` 并将下面的代码添加到 `Click` 事件处理程序：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/form1.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/form1.vb" id="Snippet3":::

4. 在解决方案资源管理器中，右键单击 WindowsApplication1，然后单击“设为启动项目”。

5. 按 **F5** 运行项目。 输入一些文本，然后单击按钮。 此标签显示 "您输入的内容："，并显示您输入的文本。

     ![显示结果的表单](../data-tools/media/wcf10.png)

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
