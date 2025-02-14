---
title: 向订阅管理门户添加新的每月订阅 | Microsoft Docs
author: evanwindom
ms.author: amast
manager: shve
ms.assetid: 36f0d9f1-fe28-469f-a54c-dc46638270a8
ms.date: 05/18/2022
ms.topic: how-to
description: 了解如何向订阅管理门户添加新购买的每月 Visual Studio 订阅
ms.openlocfilehash: f4d2b8014828812febeb33d31da97b9b99048349
ms.sourcegitcommit: 2c4ca71e7711d9c4a468b1bcff026565c765952c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2022
ms.locfileid: "145172633"
---
# <a name="add-new-monthly-visual-studio-subscriptions-to-the-subscriptions-administration-portal"></a>向订阅管理门户添加新的每月 Visual Studio 订阅

使用 Azure 订阅购买新的每月 Visual Studio 订阅后，可能需要将它们添加到订阅管理门户，以便将它们分配给用户。  

## <a name="how-do-i-know-if-i-need-to-add-my-subscriptions"></a>如何判断我是否需要添加自己的订阅？

添加每月订阅的步骤取决于你的组织已有的订阅种类，以及你是否是新管理员。
+ 如果你是新管理员，我们会在你首次登录订阅管理门户时，检查是否有你拥有用户访问管理员权限的 Azure 订阅。  如果我们为你找到了每月订阅，就会自动添加它们。 
+ 如果以前已使用 Azure 订阅添加或管理每月购买的订阅，我们会在每次登录时检查新的每月订阅。 
+ 如果你已是批量许可订阅的管理员，但尚未添加或托管每月订阅，则需要使用以下步骤添加它们。

## <a name="how-to-add-monthly-subscriptions"></a>如何添加每月订阅

1. 登录订阅管理门户 (<https://manage.visualstudio.com>)
0. 在“管理订阅者”选项卡上，选择“添加协议”下拉列表 
0. 在下拉列表中，选择“新建每月订阅”
   > [!div class="mx-imgBorder"]
   > ![用于添加新的每月订阅的下拉列表](_img/add-monthly-subs/add-subs-drop-down.png "依次选择“添加协议”、“新建每月订阅”。")
0. 系统会搜索你拥有用户访问管理员权限的任何 Azure 订阅，并导入使用这些 Azure 订阅购买的所有 Visual Studio 订阅。
0. 如果没有任何 Azure 订阅的用户访问管理员权限，或者找不到任何Visual Studio订阅，将收到以下消息：
   > [!div class="mx-imgBorder"]
   > ![找不到一个或多个新的每月订阅](_img/add-monthly-subs/no-subs-found.png "指出没有 Azure 订阅或 Visual Studio 订阅可供你使用的错误消息。")
0. 如果找到新的每月订阅，将收到确认消息
   > [!div class="mx-imgBorder"]
   > ![关于已添加订阅的确认消息](_img/add-monthly-subs/subs-added-confirmation.png "确认消息将显示已添加的订阅。")

## <a name="things-to-keep-in-mind"></a>要点

+ 添加新的每月订阅的选项只在第一次购买订阅时可用。  添加每月订阅后，我们会在每次登录到门户时检查新订阅。 
+ 你可能会发现，找到的新订阅已分配给订阅者。  这是因为还有其他管理员可以访问 Azure 订阅，并且他们已向用户分配了新的 Visual Studio 订阅。  既然你已将它们添加到门户，所以也就可以管理这些订阅。 

## <a name="support-resources"></a>支持资源

如需有关管理 Visual Studio 订阅的帮助，请联系 [Visual studio 订阅支持](https://aka.ms/vsadminhelp)。

## <a name="next-steps"></a>后续步骤

至此，你已添加订阅，可以将它们分配给用户了。  可以通过多种方式来进行分配：
+ [单独分配订阅](assign-license.md)
+ [将订阅分配给多个用户](assign-license-bulk.md)
+ [将特定订阅分配给特定用户](assign-guid.md)

## <a name="see-also"></a>请参阅

+ [Visual Studio 文档](/visualstudio/)
+ [Azure DevOps 文档](/azure/devops/)
+ [Azure 文档](/azure/)
+ [Microsoft 365 文档](/microsoft-365/)