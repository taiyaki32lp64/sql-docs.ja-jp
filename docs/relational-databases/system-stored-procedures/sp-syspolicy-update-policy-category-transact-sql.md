---
title: sp_syspolicy_update_policy_category (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_update_policy_category_TSQL
- sp_syspolicy_update_policy_category
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_update_policy_category
ms.assetid: 6b6413c2-7a3b-4eff-91d9-5db2011869d6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1124dccf4053542cc7545da4ff8eb0928479c2ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096162"
---
# <a name="spsyspolicyupdatepolicycategory-transact-sql"></a>sp_syspolicy_update_policy_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ポリシー カテゴリをデータベースのサブスクリプションの要求に設定するかどうかを更新します。 サブスクリプションが必須で、ポリシー カテゴリはすべてのデータベースに適用されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syspolicy_update_policy_category { [ @name = ] 'name' | [ @policy_category_id = ] policy_category_id }  
    , [ @mandate_database_subscriptions = ] mandate_database_subscriptions ]  
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'name'` ポリシー カテゴリの名前です。 *名前*は**sysname**場合に、指定する必要があります*policy_category_id*は NULL です。  
  
`[ @policy_category_id = ] policy_category_id` ポリシー カテゴリの識別子です。 *policy_category_id*は**int**場合に、指定する必要があります*名前*は NULL です。  
  
`[ @mandate_database_subscriptions = ] mandate_database_subscriptions` データベース サブスクリプションがポリシー カテゴリに対して必須かどうかを判断します。 *mandate_database_subscriptions*は、**ビット**値、既定値は NULL です。 値は次のいずれかを使用できます。  
  
-   0 = 必須ではないです。  
  
-   1 = 必須  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 sp_syspolicy_update_policy_category は msdb システム データベースのコンテキストで実行する必要があります。  
  
 いずれかの値を指定する必要があります*名前*または*policy_category_id*します。 どちらも NULL にできません。 これらの値を取得するには、msdb.dbo.syspolicy_policy_categories システム ビューに対してクエリを実行します。  
  
## <a name="permissions"></a>アクセス許可  
 PolicyAdministratorRole 固定データベース ロールのメンバーシップが必要です。  
  
> [!IMPORTANT]  
>  資格情報が昇格される可能性:PolicyAdministratorRole ロールのユーザーがサーバー トリガーを作成しのインスタンスの運用に影響する可能性のあるポリシーの実行をスケジュール設定、[!INCLUDE[ssDE](../../includes/ssde-md.md)]します。 たとえば、PolicyAdministratorRole ロールに割り当てられているユーザーは、ほとんどのオブジェクトが[!INCLUDE[ssDE](../../includes/ssde-md.md)]で作成されないようにすることができるポリシーを作成できます。 構成の制御について信頼できるユーザーにのみこの昇格される可能性の資格情報、ため PolicyAdministratorRole ロールを付与する必要があります、[!INCLUDE[ssDE](../../includes/ssde-md.md)]します。  
  
## <a name="examples"></a>使用例  
 次の例では、データベースのサブスクリプションが要求されるように 'Finance' カテゴリを更新します。  
  
```  
EXEC msdb.dbo.sp_syspolicy_update_policy_category @name = N'Finance'  
, @mandate_database_subscriptions = 1;  
  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [ポリシー ベースの管理ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_add_policy_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-transact-sql.md)   
 [sp_syspolicy_delete_policy_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-delete-policy-category-transact-sql.md)   
 [sp_syspolicy_rename_policy_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-rename-policy-category-transact-sql.md)  
  
  
