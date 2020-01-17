---
title: sp_syspolicy_configure (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_configure
- sp_syspolicy_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_configure
ms.assetid: 70c10922-9345-4190-ba69-808a43f760da
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5aa9801d312e5f862cb6274659496aff10c774ad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68010499"
---
# <a name="spsyspolicyconfigure-transact-sql"></a>sp_syspolicy_configure (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ポリシー ベースの管理を有効にするかどうかなど、ポリシー ベースの管理の設定を構成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syspolicy_configure [ @name = ] 'name'  
    , [ @value = ] value  
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'name'` 構成する設定の名前です。 *名前*は**sysname**が必要であり、NULL または空の文字列にすることはできません。  
  
 *名前*値は次のいずれかを指定できます。  
  
-   'Enabled' : ポリシー ベースの管理を有効にするかどうかを指定します。  
  
-   'HistoryRetentionInDays' : ポリシー評価履歴を保持する日数を指定します。 0 に設定した場合、履歴は自動的には削除されません。  
  
-   'LogOnSuccess' では、ポリシー ベースの管理が成功したポリシー評価を記録するかどうかを指定します。  
  
`[ @value = ] value` 指定された値に関連付けられている値は、*名前*します。 *値*は**sql_variant**、必要があります。  
  
-   'Enabled' を指定する場合*名前*値は次のいずれかを使用することができます。  
  
    -   0 = ポリシー ベースの管理を無効にします。  
  
    -   1 = ポリシー ベースの管理を有効にします。  
  
-   'HistoryRententionInDays' を指定する場合*名前*整数値としての日数を指定します。  
  
-   'LogOnSuccess' を指定した場合*名前*値は次のいずれかを使用することができます。  
  
    -   0 = では、ポリシーの評価に失敗しましただけをログします。  
  
    -   1 = 成功および失敗したポリシー評価評価の両方を記録します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 msdb システム データベースのコンテキストで sp_syspolicy_configure を実行する必要があります。  
  
 これらの設定の現在の値を表示するには、msdb.dbo.syspolicy_configuration システム ビューをクエリします。  
  
## <a name="permissions"></a>アクセス許可  
 PolicyAdministratorRole 固定データベース ロールのメンバーシップが必要です。  
  
> [!IMPORTANT]  
>  資格情報が昇格される可能性:PolicyAdministratorRole ロールのユーザーがサーバー トリガーを作成しのインスタンスの運用に影響する可能性のあるポリシーの実行をスケジュール設定、[!INCLUDE[ssDE](../../includes/ssde-md.md)]します。 たとえば、PolicyAdministratorRole ロールに割り当てられているユーザーは、ほとんどのオブジェクトが[!INCLUDE[ssDE](../../includes/ssde-md.md)]で作成されないようにすることができるポリシーを作成できます。 構成の制御について信頼できるユーザーにのみこの昇格される可能性の資格情報、ため PolicyAdministratorRole ロールを付与する必要があります、[!INCLUDE[ssDE](../../includes/ssde-md.md)]します。  
  
## <a name="examples"></a>使用例  
 次の例には、ポリシー ベースの管理ができるようにします。  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'Enabled'  
, @value = 1;  
  
GO  
```  
  
 次の例では、ポリシーの履歴の保有期間を 14 日間に設定します。  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'HistoryRetentionInDays'  
, @value = 14;  
  
GO  
```  
  
 次の例では、成功したポリシー評価と失敗したポリシー評価の両方をログに記録するようにポリシー ベースの管理を構成します。  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'LogOnSuccess'  
, @value = 1;  
  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [ポリシー ベースの管理ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_set_config_enabled &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-enabled-transact-sql.md)   
 [sp_syspolicy_set_config_history_retention &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-history-retention-transact-sql.md)   
 [sp_syspolicy_set_log_on_success &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-log-on-success-transact-sql.md)  
  
  
