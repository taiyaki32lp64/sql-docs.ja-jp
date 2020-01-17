---
title: syspolicy_policy_categories (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_categories
- syspolicy_policy_categories_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_groups view
ms.assetid: 65f080c7-771f-4cf6-a7a0-88882c637f8d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: af9086ba9de7d9c61bcedecd4331e7e0e77d6489
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121123"
---
# <a name="syspolicypolicycategories-transact-sql"></a>syspolicy_policy_categories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  インスタンスでポリシー ベースの管理のポリシー カテゴリごとに 1 行を表示します。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 ポリシー カテゴリを使用して、多数のポリシーがある場合は、ポリシーを整理できます。 次の表では、syspolicy_policy_groups ビュー内の列について説明します。  
 
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|policy_category_id|**int**|ポリシー カテゴリの識別子です。|  
|NAME|**sysname**|ポリシー カテゴリの名前。|  
|mandate_database_subscriptions|**bit**|ポリシー カテゴリ (1) 明示的なサブスクリプションがなくても、インスタンスのすべてのデータベースに適用されますか、ポリシー カテゴリは、明示的なサブスクリプション (0) を使用して、データベースに適用する必要があるかどうかを示します。|  
  
## <a name="remarks"></a>コメント  
 ポリシー ベースの管理ポリシーのグループの一覧が表示されます。  
  
## <a name="permissions"></a>アクセス許可  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>関連項目  
 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [ポリシーベースの管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
