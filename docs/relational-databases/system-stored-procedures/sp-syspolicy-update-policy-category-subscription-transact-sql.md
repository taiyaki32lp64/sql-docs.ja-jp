---
title: sp_syspolicy_update_policy_category_subscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_update_policy_category_subscription_TSQL
- sp_syspolicy_update_policy_category_subscription
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_update_policy_category_subscription
ms.assetid: d0769566-8f5c-4c8a-84d3-ee17ea6e0cb4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f3833d16d0cf4e791064dc369d460fe9cf5cc3e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035365"
---
# <a name="spsyspolicyupdatepolicycategorysubscription-transact-sql"></a>sp_syspolicy_update_policy_category_subscription (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定したデータベースのポリシー カテゴリ サブスクリプションを更新します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syspolicy_update_policy_category_subscription [ @policy_category_subscription_id = ] policy_category_subscription_id  
    [ , [ @target_type = ] 'target_type' ]  
    [ , [ @target_object = ] 'target_object' ]  
    , [ @policy_category = ] 'policy_category'  
```  
  
## <a name="arguments"></a>引数  
`[ @policy_category_subscription_id = ] policy_category_subscription_id` 更新するポリシー カテゴリのサブスクリプションの識別子です。 *policy_category_subscription_id*は**int**、必要があります。  
  
`[ @target_type = ] 'target_type'` カテゴリのサブスクリプションのターゲット型です。 *target_type*は**sysname**、既定値は NULL です。  
  
 指定した場合*target_type*、'DATABASE' に値を設定する必要があります。  
  
`[ @target_object = ] 'target_object'` ポリシー カテゴリにサブスクライブするデータベースの名前です。 *target_object*は**sysname**、既定値は NULL です。  
  
`[ @policy_category = ] 'policy_category'` データベースでサブスクライブするポリシー カテゴリの名前です。 *policy_category*は**sysname**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 run sp_syspolicy_update_policy_category_subscription は msdb システム データベースのコンテキストで実行する必要があります。  
  
 値を取得する*policy_category_subscription_id*および*policy_category*、次のクエリを使用することができます。  
  
```  
SELECT a.policy_category_subscription_id, a.target_type, a.target_object  
    , b.name AS policy_category  
FROM msdb.dbo.syspolicy_policy_category_subscriptions AS a  
INNER JOIN msdb.dbo.syspolicy_policy_categories AS b  
ON a.policy_category_id = b.policy_category_id;  
```  
  
## <a name="permissions"></a>アクセス許可  
 PolicyAdministratorRole 固定データベース ロールのメンバーシップが必要です。  
  
> [!IMPORTANT]  
>  資格情報が昇格される可能性:PolicyAdministratorRole ロールのユーザーがサーバー トリガーを作成しのインスタンスの運用に影響する可能性のあるポリシーの実行をスケジュール設定、[!INCLUDE[ssDE](../../includes/ssde-md.md)]します。 たとえば、PolicyAdministratorRole ロールに割り当てられているユーザーは、ほとんどのオブジェクトが[!INCLUDE[ssDE](../../includes/ssde-md.md)]で作成されないようにすることができるポリシーを作成できます。 構成の制御について信頼できるユーザーにのみこの昇格される可能性の資格情報、ため PolicyAdministratorRole ロールを付与する必要があります、[!INCLUDE[ssDE](../../includes/ssde-md.md)]します。  
  
## <a name="examples"></a>使用例  
 次の例では、AdventureWorks2012 データベースが 'Finance' ポリシー カテゴリをサブスクライブするように既存のポリシー カテゴリのサブスクリプションを更新します。  
  
```  
EXEC msdb.dbo.sp_syspolicy_update_policy_category_subscription @policy_category_subscription_id = 1  
, @target_object = 'AdventureWorks2012'  
, @policy_category = 'Finance';  
  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [ポリシー ベースの管理ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_add_policy_category_subscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-subscription-transact-sql.md)   
 [sp_syspolicy_delete_policy_category_subscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-delete-policy-category-subscription-transact-sql.md)  
  
  
