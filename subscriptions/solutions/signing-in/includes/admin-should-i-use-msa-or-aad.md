---
title: 我应该使用 Microsoft 帐户还是 Azure Active Directory？
description: 管理员同时拥有 MSA 和 Azure AD 帐户，但不知道要使用哪个帐户
ms.topic: include
ms.assetid: 8cb1b018-b97a-42e9-a71e-68e60cb8cec1
author: evanwindom
ms.author: amast
ms.date: 06/02/2021
user.type: admin
tags: msa
subscription.type: vl, cloud, retail, partner
sap.id: 17a2bf94-0d03-2629-dfd8-e8935f9126ec
ms.openlocfilehash: f6e17f0ba340aa150b4277c36afcd4da18cb9e83
ms.sourcegitcommit: 28168514c0c9472e852de35cceb4f95837669da6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "133254505"
---
## <a name="should-i-use-microsoft-account-msa-or-azure-active-directory-azure-ad"></a>我应该使用 Microsoft 帐户 (MSA) 还是 Azure Active Directory (Azure AD)？

MSA 是你所拥有并维护的一个电子邮件帐户，可以用于访问 Microsoft 服务。 如果离开公司，你仍可以访问连接到该标识的服务。 在管理门户中手动删除访问权限之前，你可以继续使用分配的 Visual Studio 订阅，也可以管理协议。

Azure AD 是由贵组织管理的基于云租户。 你的 Azure AD 帐户可用于控制对 Microsoft 服务的访问。 当你离开公司且你的帐户遭停用时，无法再使用此电子邮件地址登录。

我们建议使用 Azure AD，因为管理门户可以自动管理未经授权的访问。 当你在 Azure AD 中停用用户帐户时，系统也会阻止其对订阅或管理门户的访问。 
