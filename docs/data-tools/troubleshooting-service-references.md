---
title: 服务引用疑难解答
description: 查看在 Visual Studio 中使用 Windows Communication Foundation (WCF) 或 WCF Data Services 引用时可能发生的常见问题。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- msvse_wcf.Err.ReferenceGroup_NamespaceConflictsOther
- msvse_wcf.Err.AddSvcRefDlg_NothingSelectedOnGo
- msvse_wcf.Err.ErrorOnOK
- msvse_wcf.cfg.ConfigurationErrorsException
helpviewer_keywords:
- service references [Visual Studio], troubleshooting
- WCF services, troubleshooting
ms.assetid: 3b531120-1325-4734-90c6-6e6113bd12ac
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 649204a074980c547fc238ba0c7db923c7ff199b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601076"
---
# <a name="troubleshoot-service-references"></a>服务引用疑难解答

本主题列出了在 Visual Studio 中使用 Windows Communication Foundation (WCF) 或 WCF Data Services 引用时可能发生的常见问题。

## <a name="error-returning-data-from-a-service"></a>从服务返回数据时出错

从服务返回 `DataSet` 或 `DataTable` 时，可能会收到“已超出传入消息的最大大小配额”异常。 默认情况下，某些绑定的 `MaxReceivedMessageSize` 属性设置为相对较小的值，以限制遭受拒绝服务攻击的程度。 可以增大此值以防止发生异常。 有关详细信息，请参阅 <xref:System.ServiceModel.HttpBindingBase.MaxReceivedMessageSize%2A>。

修复此错误的方法：

1. 在“解决方案资源管理器”中，双击“app.config”文件将其打开。

2. 找到 `MaxReceivedMessageSize` 属性，并将其更改为更大的值。

## <a name="cannot-find-a-service-in-my-solution"></a>在“我的解决方案”中找不到服务

单击“添加服务引用”对话框中的“发现”按钮时，解决方案中的一个或多个 WCF 服务库项目不会显示在服务列表中 。 如果服务库已添加到解决方案但尚未进行编译，可能会发生这种情况。

修复此错误的方法：

- 在“解决方案资源管理器”中，右键单击“WCF 服务库”项目，然后单击“生成” 。

## <a name="error-accessing-a-service-over-a-remote-desktop"></a>通过远程桌面访问服务时出错

当用户通过远程桌面连接访问 Web 托管的 WCF 服务时，如果该用户没有管理权限，则需要使用 NTLM 身份验证。 如果用户没有管理权限，则可能会收到以下错误消息：“HTTP 请求未经授权，客户端身份验证方案为‘匿名’。 从服务器收到的身份验证标头为‘NTLM’。”

修复此错误的方法：

1. 在网站项目中，打开“属性”页。

2. 在“启动选项”选项卡上，清除“NTLM 身份验证”复选框” 。

    > [!NOTE]
    > 应只对专门包含 WCF 服务的网站禁用 NTLM 身份验证。 WCF 服务的安全性通过“web.config”文件中的配置来管理。 所以也可不使用 NTLM 身份验证。

## <a name="access-level-for-generated-classes-setting-has-no-effect"></a>生成的类设置的访问级别不起作用

在“配置服务引用”对话框中将生成的类的访问级别选项设置为“内部”或“朋友”这一操作可能并不总是有效   。 即使在对话框中设置了该选项，也会生成访问级别为 `Public` 的支持类。

这是某些类型的已知限制，例如使用 <xref:System.Xml.Serialization.XmlSerializer> 序列化的类型。

## <a name="error-debugging-service-code"></a>调试服务代码时出错

当你从客户端代码单步执行到 WCF 服务的代码时，可能会收到与缺少符号相关的错误。 当移动或删除解决方案中的某一服务时，可能会发生这种情况。

首次添加对当前解决方案中的某一 WCF 服务的引用时，服务项目和服务客户端项目之间会添加显式生成依赖项。 这可确保客户端始终访问最新的服务二进制文件，这对调试方案（例如从客户端代码单步执行到服务代码）尤其重要。

如果从解决方案中删除服务项目，则此显式生成依赖项将失效。 Visual Studio 不再保证在必要时重新生成服务项目。

若要修复此错误，必须手动重新生成服务项目：

1. 在 **“工具”** 菜单上，单击 **“选项”** 。

2. 在“选项”对话框中，展开“项目和解决方案”，然后选择“常规”  。

3. 确保选中“显示高级生成配置”复选框，然后点击“确定” 。

4. 加载 WCF 服务项目。

5. 从“Configuration Manager”对话框中，将“活动解决方案配置”设置为“调试”  。 有关详细信息，请参阅[如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)。

6. 在“解决方案资源管理器”中，选择 WCF 服务项目。

7. 在“生成”菜单上，单击“重新生成”以重新生成 WCF 服务项目 。

## <a name="wcf-data-services-do-not-display-in-the-browser"></a>WCF Data Services 不显示在浏览器中

当它尝试查看 [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)] 中数据的 XML 表示形式时，Internet Explorer 可能会将数据误解释为 RSS 源。 确保已禁用显示 RSS 源的选项。

若要修复此错误，请禁用 RSS 源：

1. 在 Internet Explorer 的“工具”菜单上，单击“Internet 选项”。

2. 在“内容”选项卡上的“源”部分中，单击“设置”  。

3. 在“源设置”对话框中，清除“启用源读取视图”复选框，然后点击“确定”  。

4. 单击“确定”，关闭“Internet 选项”对话框 。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
