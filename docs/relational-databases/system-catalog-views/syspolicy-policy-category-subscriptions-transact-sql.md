---
title: syspolicy_policy_category_subscriptions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_category_subscriptions_TSQL
- syspolicy_policy_category_subscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_group_subscriptions view
ms.assetid: b3b3a7d7-0b78-46c0-9755-045f7a5692b9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 304e904ab95e4be58ba2a373bd6ed9c11131049f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094893"
---
# <a name="syspolicypolicycategorysubscriptions-transact-sql"></a>syspolicy_policy_category_subscriptions (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのポリシー ベースの管理サブスクリプションごとに 1 つの行を表示します。 各行には、対象とポリシー カテゴリのペアについて説明します。 次の表では、syspolicy_policy_group_subscriptions ビュー内の列について説明します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|policy_category_subscription_id|**int**|このレコードの識別子。|  
|target_type|**sysname**|このサブスクリプションの対象であるデータベース オブジェクトの種類。|  
|target_object|**sysname**|対象オブジェクトの名前。|  
|policy_category_id|**int**|ターゲットに適用されるポリシー カテゴリの ID。|  
  
## <a name="remarks"></a>コメント  
 ポリシー カテゴリをサブスクライブしているターゲットを表示します。  
  
## <a name="permissions"></a>アクセス許可  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>関連項目  
 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [ポリシーベースの管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
