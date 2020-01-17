---
title: sp_help_maintenance_plan (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_maintenance_plan_TSQL
- sp_help_maintenance_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_maintenance_plan
ms.assetid: e972a510-960e-41d6-93c5-c71cd581a585
author: stevestein
ms.author: sstein
ms.openlocfilehash: 42a98fe7af16c4e8aab22d6ace02f359dfe02c54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096199"
---
# <a name="sphelpmaintenanceplan-transact-sql"></a>sp_help_maintenance_plan (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定したメンテナンス プランに関する情報を返します。 プランが指定されていない場合、このストアド プロシージャは、すべてのメンテナンス プランに関する情報を返します。  
  
> **注:** このストアド プロシージャは、データベース メンテナンス プランで使用されます。 この機能は、このストアド プロシージャを使用しないメンテナンス プランに置き換わりました。 このプロシージャは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からアップグレードしたプログラムでデータベース メンテナンス プランを管理する場合に使用します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_maintenance_plan [ [ @plan_id = ] 'plan_id' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @plan_id = ] 'plan\_id'` メンテナンス プランのプラン ID を指定します。 *plan_id*は**UNIQUEIDENTIFIER**します。 既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
 場合*plan_id*が指定されている**sp_help_maintenance_plan**は 3 つのテーブルを返します。プラン、データベース、およびジョブ。  
  
### <a name="plan-table"></a>Plan テーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|メンテナンス プランの ID|  
|**plan_name**|**sysname**|メンテナンス プランの名前。|  
|**date_created**|**datetime**|メンテナンス プランが作成された日付。|  
|**所有者**|**sysname**|メンテナンス プランの所有者です。|  
|**max_history_rows**|**int**|システム テーブルで、メンテナンス プランの履歴を記録するために割り当てられる行数の最大数。|  
|**remote_history_server**|**int**|履歴レポートが書き込まれる先のリモート サーバーの名前。|  
|**max_remote_history_rows**|**int**|履歴レポートが書き込まれる先のリモート サーバー上のシステム テーブルに割り当てられる行数の最大数。|  
|**user_defined_1**|**int**|既定値は NULL|  
|**user_defined_2**|**nvarchar(100)**|既定値は NULL|  
|**user_defined_3**|**datetime**|既定値は NULL|  
|**user_defined_4**|**uniqueidentifier**|既定値は NULL|  
  
### <a name="database-table"></a>データベース テーブル  
  
|列名|説明|  
|-----------------|-----------------|  
|**database_name**|メンテナンス プランに関連付けられているすべてのデータベースの名前です。 *database_name* は **sysname** です。|  
  
### <a name="job-table"></a>ジョブ テーブル  
  
|列名|説明|  
|-----------------|-----------------|  
|**job_id**|メンテナンス プランに関連付けられているすべてのジョブの ID。 *job_id*は**uniqueidentifier**します。|  
  
## <a name="remarks"></a>コメント  
 **sp_help_maintenance_plan**では、 **msdb**データベース。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールが実行できる**sp_help_maintenance_plan**します。  
  
## <a name="examples"></a>使用例  
 この例のわかりやすい情報、メンテナンスの詳細については、FAD6F2AB-3571-11 D 3 9D4A 00C04FB925FC を計画します。  
  
```  
EXECUTE   sp_help_maintenance_plan   
   N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC';  
```  
  
## <a name="see-also"></a>関連項目  
 [メンテナンス プラン](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [データベース メンテナンス プラン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
