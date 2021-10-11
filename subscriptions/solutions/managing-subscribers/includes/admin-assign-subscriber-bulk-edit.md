---
title: 如何批量分配订阅者？
description: 超级管理员或管理员希望详细了解如何使用批量功能。
ms.topic: include
ms.assetid: 3b450a79-47d2-4434-899d-bea29a0271e1
author: CaityBuschlen
ms.author: cabuschl
ms.date: 06/01/2021
user.type: admin
tags: bulk
subscription.type: vl, cloud, retail, partner
sap.id: b84fffb5-3363-eb7d-224e-1c63faf4067b
ms.openlocfilehash: d837b52d57a212f7519adfbc027eadbcf5f45dab
ms.sourcegitcommit: 364e106fcbf4fb6af534e81d8b700901f79f4ec8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2021
ms.locfileid: "129013210"
---
## <a name="how-do-i-assign-subscribers-in-bulk"></a>如何批量分配订阅者？

有两个选项可以批量分配订阅者。
- 你可以使用 [Excel 模板批量上传](https://docs.microsoft.com/visualstudio/subscriptions/assign-license-bulk#use-bulk-add-to-assign-subscriptions)。
- 如果组织具有可超额分配订阅的协议类型，你可以使用 [Azure Active Directory (Azure AD) 组分配](https://docs.microsoft.com/visualstudio/subscriptions/assign-license-bulk#use-azure-active-directory-groups-to-assign-subscriptions)。

## <a name="use-bulk-upload"></a>使用批量上传
1. 确保在协议下拉菜单中选中需要更新的协议。
2. 选择“添加”，然后在下拉菜单中选择“批量编辑”。  按照弹出窗口中的说明操作。
3. 导出 Excel 工作表后，你可以在文件中进行必要的编辑，然后保存并上传该文件。 编辑时，请注意 GUID 无法更改。
4. 选择“确定”开始批量编辑。

如果模板包含任何错误，上传将失败。 系统将显示错误，因此你可以更正模板，然后重试。

## <a name="use-azure-ad-groups"></a>使用 Azure AD 组
使用 Azure AD 批量上传目前仅适用于具有可以过度认领协议的组织。
1. 确保在协议下拉菜单中选中需要更新的协议。
2. 选择“添加”，然后从下拉菜单中选择“Azure Active Directory 组”。 
3. 开始输入要添加到表单域的 Azure AD 组名。 键入名称时，搜索会更新，以显示组织内可用的 Azure AD 组。
4. 选择组后，该字段将自动填充组名。 进行更改之前，你可以查看该组中的用户。
5. 依次选择“添加”、“确认”。 
6. 添加到 Azure AD 组的任何未来用户都会自动获得订阅。 对于从组中删除的任何用户，其订阅也会相应删除。