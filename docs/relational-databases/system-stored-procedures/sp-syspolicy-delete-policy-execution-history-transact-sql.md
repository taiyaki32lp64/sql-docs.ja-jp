---
title: sp_syspolicy_delete_policy_execution_history (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_delete_policy_execution_history
- sp_syspolicy_delete_policy_execution_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_delete_policy_execution_history
ms.assetid: fe651af9-267e-45ec-b4e7-4b0698fb1be3
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f0cb7f631b75be4e8b2f4063b03aca1895ba6900
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997336"
---
# <a name="spsyspolicydeletepolicyexecutionhistory-transact-sql"></a>sp_syspolicy_delete_policy_execution_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ポリシー ベースの管理でポリシー実行履歴を削除します。 このストアド プロシージャを使用して、特定のポリシーまたはすべてのポリシーの実行履歴、および特定の日付までの実行履歴を削除できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syspolicy_delete_policy_execution_history [ @policy_id = ] policy_id ]  
    [ , [ @oldest_date = ] 'oldest_date' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @policy_id = ] policy_id` 実行履歴を削除するポリシーの識別子です。 *policy_id*は**int**、必要があります。 NULL にすることができます。  
  
`[ @oldest_date = ] 'oldest_date'` ポリシー実行履歴を保持する最も古い日付です。 実行履歴もこの日付より前は削除されます。 *oldest_date*は**datetime**、必要があります。 NULL にすることができます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 sp_syspolicy_delete_policy_execution_history は msdb システム データベースのコンテキストで実行する必要があります。  
  
 値を取得する*policy_id*、し、実行履歴の日付を表示するには、次のクエリを使用することができます。  
  
```  
SELECT a.name AS N'policy_name', b.policy_id, b.start_date, b.end_date  
FROM msdb.dbo.syspolicy_policies AS a   
INNER JOIN msdb.dbo.syspolicy_policy_execution_history AS b  
ON a.policy_id = b.policy_id  
```  
  
 1 つまたは両方の値に NULL を指定する場合、次の動作が適用されます。  
  
-   すべてのポリシー実行履歴を削除するには、両方の NULL を指定*policy_id*および*oldest_date*します。  
  
-   特定のポリシーのすべてのポリシー実行履歴を削除するには、ポリシーの識別子を指定*policy_id*、NULL を指定して*oldest_date*します。  
  
-   NULL を指定する、特定の日付の前に、すべてのポリシーのポリシー実行履歴を削除する*policy_id*、日付を指定して*oldest_date*します。  
  
 ポリシーの実行履歴をアーカイブするには、オブジェクト エクスプローラーでポリシー履歴ログを開いて、実行履歴をファイルにエクスポートします。 ポリシー履歴ログにアクセスするには、展開**管理**を右クリックして**ポリシーの管理**、 をクリックし、**履歴の表示**します。  
  
## <a name="permissions"></a>アクセス許可  
 PolicyAdministratorRole 固定データベース ロールのメンバーシップが必要です。  
  
> [!IMPORTANT]  
>  資格情報が昇格される可能性:PolicyAdministratorRole ロールのユーザーがサーバー トリガーを作成しのインスタンスの運用に影響する可能性のあるポリシーの実行をスケジュール設定、[!INCLUDE[ssDE](../../includes/ssde-md.md)]します。 たとえば、PolicyAdministratorRole ロールに割り当てられているユーザーは、ほとんどのオブジェクトが[!INCLUDE[ssDE](../../includes/ssde-md.md)]で作成されないようにすることができるポリシーを作成できます。 構成の制御について信頼できるユーザーにのみこの昇格される可能性の資格情報、ため PolicyAdministratorRole ロールを付与する必要があります、[!INCLUDE[ssDE](../../includes/ssde-md.md)]します。  
  
## <a name="examples"></a>使用例  
 次の例では、ID が 7 のポリシーについて特定の日付より前のポリシーの実行履歴を削除します。  
  
```  
EXEC msdb.dbo.sp_syspolicy_delete_policy_execution_history @policy_id = 7  
, @oldest_date = '2009-02-16 16:00:00.000';  
  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [ポリシー ベースの管理ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_set_config_history_retention &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-history-retention-transact-sql.md)   
 [sp_syspolicy_purge_history &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-purge-history-transact-sql.md)  
  
  
