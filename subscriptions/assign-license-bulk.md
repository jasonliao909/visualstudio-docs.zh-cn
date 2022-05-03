---
title: 将 Visual Studio 订阅分配给多个用户 | Microsoft Docs
author: evanwindom
ms.author: amast
manager: shve
ms.date: 04/26/2022
ms.topic: conceptual
description: 了解管理员如何一次分配多个订阅。
ms.openlocfilehash: 043fbf021f5ba4dc4a81b44abdc7d834f3a28f4f
ms.sourcegitcommit: 9e9f4cf4b34735fffa376b203ccaa74cb705ffe2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "144334292"
---
# <a name="assign-subscriptions-to-multiple-users"></a>将订阅分配给多个用户
你可以在订阅管理门户中一次添加一个多个用户，也可以采用大用户组形式添加。  要添加各个用户，请参阅[添加单个用户](assign-license.md)。

若要添加大量用户组，可以使用批量添加功能，或者组织使用的是Microsoft Azure Active Directory (Azure AD) **且组织具有受信任的协议**，则可以使用Azure AD组。 本文将介绍这两种方法的具体过程。  观看此视频或继续阅读，了解有关批量添加功能的详细信息。 

<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4vxNq]

## <a name="use-bulk-add-to-assign-subscriptions"></a>使用批量添加功能分配订阅
1. 登录 Visual Studio 订阅管理门户，网址： <https://manage.visualstudio.com> 。

1. 若要一次添加多个订阅者，请导航到“管理订阅者”选项卡。选择“添加”选项卡，然后选择下拉列表中的“批量添加”。  

1. 批量添加功能会使用 Microsoft Excel 模板上传订阅者信息。 在“上传多个订阅者”对话框中，选择“下载”下载模板。
   > [!div class="mx-imgBorder"]
   > ![下载 Excel 模板以上传多个订阅者](media/download-template-upload-subscribers.png "下载空白 Excel 模板，开始批量分配过程。")
   >
   > [!NOTE]
   > 请务必下载本模板的最新版本。 如果使用旧版本，批量上传可能会失败。

1. 在 Excel 电子表格的字段中，填写想要为其分配订阅的个人的信息。 （“引用”是可选字段。）完成后将文件保存在本地。

    > [!NOTE]
    > 管理员可以使用模板中的一个字段启用或禁用订阅者下载软件的功能。  如果禁用下载，则还会禁用他们对产品密钥的访问权限。

   为顺利地完成上传，请查看以下最佳做法：

    + 确保所有表单域均不含逗号。
    + 删除窗体字段中值前后的空格。
    + 请确保用户名不包含两部分名字或姓氏之间的额外空格。 例如，如果某个人具有两部分名字（如“Maggie May”），则应将其键入为“MaggieMay”，因为系统不会剪裁额外的空间。
    + 确保填写所有必填字段。 
    + 检查“错误消息”列。  如果列出了任何错误，请先修复这些错误，然后再尝试上传文件。 

1. 返回到 Visual Studio 订阅管理门户。 在“上传多个订阅者”对话框中，选择“浏览” 。
   > [!div class="mx-imgBorder"]
   > ![浏览到之前保存的模板以上传多个订阅者](media/bulk-add-browse-saved-template.png "你可以浏览到文件位置，或将其拖放到此对话框中。")

1. 导航到之前保存的 Excel 文件，然后选择“确定”。
   > [!div class="mx-imgBorder"]
   > ![上传 Excel 模板以上传多个订阅者](media/bulk-upload-subscribers.png "此处将显示包含你的数据的模板。选择“确定”开始上传。")

    将显示上传进度对话框。

    如果模板包含错误，上传将失败。  将显示错误，以便更正模板并再次尝试批量上传。
   > [!div class="mx-imgBorder"]
   > ![如果上传多个订阅者失败，将显示错误消息](_img/assign-license-bulk/bulk-add-upload-failure.png "如果上传的文件包含错误，则将显示此消息。解决错误，然后再次执行批量添加过程。")

   如果遇到故障，请执行以下步骤：
   1. 打开你创建的 Excel 文件、更正问题，然后保存文件。
   0. 返回到管理门户并关闭错误消息。
   0. 选择“添加”。
   0. 选择“批量添加”。
   0. 由于你已保存 Excel 文件，因此无需下载模板。  选择“浏览”，找到刚才保存的文件，然后选择“打开” 。
   0. 选择“确定” 。


    上传成功后，系统会显示订阅者列表和一条确认消息。
   > [!div class="mx-imgBorder"]
   > ![如果上传多个订阅者成功，将显示确认消息](_img/assign-license-bulk/bulk-add-upload-success.png "上传成功完成后，你将收到一条确认消息。")

## <a name="use-azure-active-directory-groups-to-assign-subscriptions"></a>使用 Azure Active Directory 组分配订阅 
使用此功能可以轻松地控制订阅分配。 在订阅管理门户中添加Azure Active Directory安全组，以确保为组中的每个人都分配订阅。 成员离开组织并从Azure Active Directory中删除时，会自动删除对订阅的访问权限。 


> [!IMPORTANT]
>
> 以下限制适用于使用 Azure AD 组添加订阅者的情况：
> + 在最初将组添加到管理门户时，管理员必须是 Azure AD 租户的成员。  添加组后，对组成员身份进行更改不需要管理员参与。 
> + 组必须至少包含一个成员。  不支持空组。
> + 所有用户都必须处于组的顶层。  不支持嵌套组。
> + 仅支持受信任协议。 （只有能够“过度分配”订阅的协议才是受信任的。）
> + 组的所有成员都必须具有与其 Azure AD 帐户关联的电子邮件地址。
> + 对于使用 Azure AD 组添加的订阅，不支持对通知使用不同的电子邮件地址。  

观看此视频或继续阅读，了解有关使用 Azure Active Directory 组功能添加订阅者的详细信息。 
<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4rvvW]

1. 登录 Visual Studio 订阅管理门户，网址：[https://manage.visualstudio.com](https://manage.visualstudio.com)。

2. 若要一次添加多个订阅者，请导航到“管理订阅者”选项卡。

3. 选择“添加”选项卡，然后选择下拉列表中的“Azure Active Directory 组”。  

   > [!div class="mx-imgBorder"]
   > ![使用 Azure AD 选择批量添加](_img/assign-license-bulk/bulk-add-aad.png "选择“使用 Azure AD 功能批量添加”以从 Azure Active Directory 组拉取订阅者。")

4. 右侧将显示一个浮出控件窗口。  开始输入要添加到表单域的 Azure AD 组的名称。 系统将搜索组织中可用的Azure AD组进行匹配。 

5. 选择组后，该字段将自动填充组名。 在添加用户之前，可以选择查看该组中的用户。 接下来，可以选择组的订阅级别、下载权限和通信首选项。 可以根据需要在引用字段中添加详细信息。 

   > [!div class="mx-imgBorder"]
   > ![选择 Azure AD 组](_img/assign-license-bulk/bulk-add-aad-details.png "选择 Azure AD 组的名称以添加该组中的订阅者。")

6. 选择“添加”，然后选择“确认” 。 

7. 若要查看添加的组，请滚动到用户列表的底部。  

8. 选择“查看订阅者”以显示组的成员。 可以查看组中订阅者的详细信息。  但是，无法对订阅者或分配给订阅者的订阅进行任何编辑。    

> [!NOTE]
> 如果已单独为用户（这些用户随后将作为 Azure AD 组的一部分进行添加）分配了订阅，则这些用户将添加到组中，并且不再单独列出。 但是，如果单个订阅对应于不同的订阅级别，则他们将拥有两个订阅。  示例：如果用户有一个单独的 Visual Studio Professional 订阅，并且他们是组的成员，该组已分配有 Visual Studio Enterprise 订阅，则他们将同时拥有这两个订阅。  
>
> 如果从已分配有订阅的 Azure Active Directory 组中删除订阅者，则最长可能需要 24 小时才能在管理门户中反映更新。 


## <a name="frequently-asked-questions"></a>常见问题

### <a name="q-why-cant-i-see-the-option-to-use-azure-active-directory-groups-to-add-subscribers"></a>问：为何看不到使用 Azure Active Directory 组来添加订阅者的选项？
答：此功能目前仅适用于具有受信任的协议的组织。  选择“详细信息”按钮以显示你的协议信息。

   > [!div class="mx-imgBorder"]
   > ![单击“详细信息”按钮](_img/assign-license-bulk/bulk-add-agreement.png "单击“详细信息”按钮以查看你拥有的协议类型")

### <a name="q-i-added-users-to-my-azure-active-directory-group-but-they-dont-have-subscriptions-yet-why"></a>问：我向我的 Azure Active Directory 组添加了用户，但这些用户还没有订阅。 为什么？ 
答：如果更改直接在Azure Active Directory中进行了更改，则应非常快速地分配订阅。  如果在本地 Active Directory 中进行了更改，则首先需要同步到Azure Active Directory。 根据本地 Active Directory 的配置方式，更改最多可能需要 24 小时才能反映。 如果时间超过 24 小时，我们的 [支持团队可以帮助排查任何问题](https://aka.ms/vsadminhelp)。 

### <a name="q-can-i-choose-multiple-subscription-levels-to-be-assigned-within-an-azure-active-directory-group"></a>问：能否选择多个要在 Azure Active Directory 组内分配的订阅级别？
答：否 - 组中的每个人都会收到相同的订阅级别。

### <a name="q-can-i-edit-subscriber-details-of-individuals-added-in-an-azure-active-directory-group"></a>问：能否编辑在 Azure Active Directory 组中添加的成员的订阅者详细信息？
答：否 - 若要修改单个订阅者的信息，请将其从Azure Active Directory安全组中删除，并单独为其分配订阅。

### <a name="q-can-i-add-separate-notification-email-addresses-for-members-of-an-azure-active-directory-group"></a>问：能否为 Azure Active Directory 组的成员添加单独的通知电子邮件地址？
答：否 - 对于使用Azure Active Directory组添加的订阅，当前不支持通知的单独电子邮件地址。 所有电子邮件都将发送到主电子邮件 (用户主体名称) 。

## <a name="resources"></a>资源
[Visual Studio 管理和订阅支持](https://aka.ms/vsadminhelp)

## <a name="see-also"></a>请参阅
+ [Visual Studio 文档](/visualstudio/)
+ [Azure DevOps 文档](/azure/devops/)
+ [Azure 文档](/azure/)
+ [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤
只有一两个订阅者要添加？ 请查阅[添加单个用户](assign-license.md)
