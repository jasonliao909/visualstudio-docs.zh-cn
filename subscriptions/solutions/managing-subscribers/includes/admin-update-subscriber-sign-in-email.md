---
title: 如何更新订阅者的登录电子邮件地址？
description: 超级管理员或管理员想要批量更新订阅者域。
ms.topic: include
ms.assetid: c1220a33-26b0-4bf9-be97-ab2b3055e351
author: CaityBuschlen
ms.author: cabuschl
ms.date: 06/01/2021
user.type: admin
tags: email
subscription.type: vl, cloud, retail, partner
sap.id: b84fffb5-3363-eb7d-224e-1c63faf4067b
ms.openlocfilehash: 56ba89a2546c384835addb05574c3280fed500e6
ms.sourcegitcommit: 485f0f6f578568ee31b2ac093e32a6d01dc9c1c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2021
ms.locfileid: "130019244"
---
## <a name="update-subscribers-sign-in-email-address"></a>更新订阅者登录电子邮件地址

你可以逐个更新订阅者登录电子邮件地址，也可使用批量编辑进行更新。 

##  <a name="bulk-edit"></a>批量编辑
1. 在“管理订阅者”页面，确保你正在浏览需要更新的协议。
2. 选择“批量编辑”，导出 Excel 文件，然后按照弹出窗口中的说明操作。
3. 在文件中进行必要的编辑，然后保存并上传该文件。 编辑时，请注意 GUID 无法更改。
4. 选择“确定”开始批量编辑。
5. 你的订阅者将收到一封电子邮件，告知他们有关更改。

## <a name="individual-edit"></a>逐个编辑 
1. 在“管理订阅者”页面，确保你正在浏览需要更新的协议。
2. 选择要更新的订阅者，然后选择订阅者名旁边的 (…) 省略号。
3. 选择“编辑”。
4. 在浮出空间面板中，进行必要的编辑，然后选择“保存”。
5. 你的订阅者将收到一封电子邮件，告知他们有关更改。

## <a name="azure-active-directory-azure-ad"></a>Azure Active Directory (Azure AD) 
如果你使用 Azure AD 组分配订阅，则任何电子邮件地址或名称更新都会自动反映在 [manage.visualstudio.com](https://manage.visualstudio.com) 中。 保存更改后，相应更新应会在 24 小时内显示在管理门户中。 
1. 登录到 [Azure 门户](https://portal.azure.com)。
2. 进行必要的更新。

## <a name="impact-of-sign-in-email-updates"></a>登录电子邮件更新的影响
更改登录电子邮件会对订阅者产生负面影响，包括：
- Visual Studio IDE 登录问题。
- Azure DevOps 登录问题。
- 每月 Azure 开发/测试个人额度问题。

[详阅更改登录电子邮件](https://docs.microsoft.com/visualstudio/subscriptions/subscription-level-changes)如何影响订阅者的相关权益。