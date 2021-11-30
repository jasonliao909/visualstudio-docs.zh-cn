---
title: 将 Visual Studio 订阅迁移到新协议 | Microsoft Docs
author: evanwindom
ms.author: amast
manager: shve
ms.assetid: 80e3b300-f2fc-40d4-bbb2-c831a2fa5d34
ms.date: 09/28/2021
ms.topic: how-to
description: 本文介绍管理员如何将分配的订阅从一个协议迁移到另一个协议。
ms.openlocfilehash: ab5d73e76c9b05f702f844020532f7bac69dec39
ms.sourcegitcommit: 28168514c0c9472e852de35cceb4f95837669da6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "133256498"
---
# <a name="migrate-subscriptions-from-one-agreement-to-another"></a>将订阅从一个协议迁移到另一个协议
如果你已将 Visual Studio 订阅作为协议的一部分分配给订阅者，并且你的公司购买了新协议，则你可能需要将订阅者从当前协议迁移到新协议。 本文介绍如何将分配的订阅移动到新协议。  

将订阅者移动到新协议时，会发生以下情况：
- 他们获取新的订阅 GUID。
- 他们所享受的权限会重置。 例如，如果他们之前已享用训练权益，将会收到该权益的新实例。 
- 如果他们在旧订阅中使用的是 Azure 个人额度，则需要激活新订阅，并将其 Azure 资产传输到该订阅。 

将订阅者移动到新协议的过程包括三个步骤：
1. 从旧协议导出当前订阅分配。 
2. 准备订阅列表以上传到新协议。 
3. 将订阅列表上传到新协议。

> [!IMPORTANT]
> 在开始此过程之前，请留意以下注意事项：
> - 如果你的经销商选择了在购买新协议时自动将订阅者传输到新协议的方案，则可能需在提交协议的 48-72 小时后才可能看到更改。 在继续执行手动移动订阅者的过程之前，请先咨询你的经销商。  
> - 你可以使用 Azure Active Directory (Azure AD) 组来简化将订阅者移动到新协议的过程。 有关详细信息，请参阅[使用 Azure AD 组分配订阅](assign-azure-ad.md)。

## <a name="export-your-current-subscription-assignments"></a>导出当前订阅分配
要将分配的订阅从一个协议迁移到另一个协议，第一步是将当前订阅分配导出为 CSV 文件。 在 Visual Studio 订阅管理门户中，你可以导出订阅者列表和有关分配的详细信息。 

此信息包括： 
- 订阅服务器名称。
- 电子邮件地址。 
- 通知电子邮件地址。 
- 订阅级别。
- 分配日期。
- 到期日期。
- 引用字段。
- 是否启用下载。
- 国家或地区。 
- 语言：
- 订阅状态。
- 订阅 GUID。

该列表导出为 CSV 文件，你可以在 Microsoft Excel 中轻松打开，以便准备将其上传到新协议。

要导出分配的订阅：
1. 登录到[管理门户](https://manage.visualstudio.com)。
2. 选择“导出”选项卡。
3. CSV 文件将下载到计算机。 文件名将反映当前协议的名称和类型，以及文件的创建日期。  

   > [!div class="mx-imgBorder"]
   > ![导出订阅者](_img/exporting-subscriptions/exporting-subscriptions.png "屏幕截图：显示用于下载已分配订阅列表的“导出”按钮。")

## <a name="prepare-your-subscription-list-for-upload-to-the-new-agreement"></a>准备订阅列表以上传到新协议
执行以下步骤打开导出的订阅列表，然后将相关的数据移动到模板以上传到新协议：
1. 找到并打开导出订阅列表时创建的文件。 你应会看到以下列名及其关联数据：
   - **订阅者名**
   - **电子邮件**
   - **通知电子邮件地址**
   - AAD 组 
   - **订阅级别**
   - 已分配
   - 已激活 
   - 到期日期 (UTC)
   - **引用**
   - **下载**
   - **国家/地区**
   - **语言**
   - 订阅状态
   - **订阅 GUID**
   - 使用状态
 
   用于将订阅上传到新协议的文件并不需要导出的 CSV 文件中的所有字段。 在上一列表中以粗体显示的字段将显示在用于上传列表的模板中。 

2. 下载用于上传订阅的 Excel 模板。  
   1. 登录到[管理门户](https://manage.visualstudio.com)。
   1. 在“管理订阅者”选项卡上，从下拉列表中选择新协议：
      > [!div class="mx-imgBorder"]
      > ![选择协议](_img/migrate-subscriptions/choose-agreement.png "屏幕截图：显示用于选择新协议的下拉列表。")
   1. 依次选择“添加”、“批量添加”。 
   1. “上传多个订阅者”对话框便会出现。  
   1. 在“步骤 2”下，选择“下载”链接以下载模板。 
      > [!div class="mx-imgBorder"]
      > ![下载批量添加模板](_img/migrate-subscriptions/download-template.png "屏幕截图：显示“下载”按钮。")
   
      该模板将显示在“下载”文件夹中。  
   1. 打开模板。

3. 打开已导出订阅者及空白的批量添加模板。 从导出的列表手动复制订阅数据，并将其粘贴到模板中。 

    请注意，导出的订阅者列表中列的顺序与模板中的顺序不同。 列名也略有不同。 下表显示了这两个电子表格的通用字段名：

   | 导出列表                | 批量添加模板  |
   |----------------------------|--------------------|
   | 订阅者名            | 名称               |
   | 电子邮件                      | 登录电子邮件      |
   | 通知电子邮件地址 | 通知电子邮件 |
   | 订阅级别         | 订阅级别 |
   | 参考                  | 参考          |
   | 下载                  | 下载          |
   | 国家/地区                    | Country            |
   | 语言                   | 语言           |
   | 订阅 GUID          | 订阅 GUID  |

   > [!TIP]
   > 如果有许多订阅者，你可能会发现在复制和粘贴数据时使用键盘快捷方式会很有帮助。 要选择列（如订阅者名）中的所有条目，请选择列的第一个条目（而不是列标题），选择并按住 Ctrl+Shift，然后选择向下箭头键。 这将选择该列的所有数据。  

4. 当所有数据都移动到批量添加模板时，请保存模板并将其关闭。 此列表是要上传到新协议的订阅列表。

## <a name="upload-your-subscription-list-to-the-new-agreement"></a>将订阅列表上传到新协议
1.  在[管理门户](https://manage.visualstudio.com)中，如果“上传多个订阅者”对话框仍处于打开状态，请选择“浏览”按钮。  转到保存订阅列表的位置并选中，然后选择“打开”。 （如果对话框未打开，请依次选择“添加”、“批量添加”。） 
    > [!div class="mx-imgBorder"]
    > ![浏览模板](_img/migrate-subscriptions/browse-template.png "屏幕截图：显示“上传多个订阅者”对话框中的“浏览”按钮。")
1. 订阅列表的名称现在将出现在“上传多个订阅者”对话框中。 选择“确定”，以上传文件。 
 
   在管理门户中，你可能会短暂地看到一条状态消息，指出系统正在上传文件。 上传完成后，你会看到消息“订阅者已成功更新”。
将订阅者从旧协议迁移到新协议已完成。  
> [!NOTE]
> 将订阅者添加到新协议后，你应将这些订阅者从旧协议中删除。 删除订阅者会阻止他们收到有关旧订阅的通知。

## <a name="resources"></a>资源
- 有关管理 Visual Studio 订阅的帮助，请参阅 [Visual Studio 订阅支持](https://aka.ms/vsadminhelp)。

## <a name="see-also"></a>另请参阅
- [Visual Studio 文档](/visualstudio/)
- [Azure DevOps 文档](/azure/devops/)
- [Azure 文档](/azure/)
- [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤
- [使用 Azure Active Directory 组分配更多订阅](assign-azure-ad.md)
- [编辑现有订阅](edit-license.md)
