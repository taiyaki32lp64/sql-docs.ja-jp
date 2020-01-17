---
title: sp_add_maintenance_plan_job (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_maintenance_plan_job_TSQL
- sp_add_maintenance_plan_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_maintenance_plan_job
ms.assetid: 7205855c-964f-4f55-bf75-39a55f6fe7bd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ba27f90c8d2fc4c7e174333080815d56f90e48c5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091918"
---
# <a name="spaddmaintenanceplanjob-transact-sql"></a>sp_add_maintenance_plan_job (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  メンテナンス プランを既存のジョブに関連付けます。  
  
> [!NOTE]  
>  このストアド プロシージャは、データベース メンテナンス プランで使用されます。 この機能は、このストアド プロシージャを使用しないメンテナンス プランに置き換わりました。 このプロシージャは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からアップグレードしたプログラムでデータベース メンテナンス プランを管理する場合に使用します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_add_maintenance_plan_job [ @plan_id = ] 'plan_id' , [ @job_id = ] 'job_id'  
```  
  
## <a name="arguments"></a>引数  
`[ @plan_id = ] 'plan_id'` メンテナンス プランの ID を指定します。 *plan_id*は**uniqueidentifier**、有効な ID を指定する必要があります  
  
`[ @job_id = ] 'job_id'` メンテナンス プランに関連付けられるジョブの ID を指定します。 *job_id*は**uniqueidentifier**、有効な ID を指定する必要があります ジョブまたはジョブを作成するには、実行**sp_add_job**、または SQL Server Management Studio を使用します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_add_maintenance_plan_job**から実行する必要があります、 **msdb**データベース。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールが実行できる**sp_add_maintenance_plan_job**します。  
  
## <a name="examples"></a>使用例  
 この例は、ジョブ"B8FCECB1-E22C-11D2-AA64-00C04F688EAE"を使用して作成したメンテナンス プランに追加します。 **sp_add_maintenance_plan_job**します。  
  
```  
EXECUTE   sp_add_maintenance_plan_job N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC', N'B8FCECB1-E22C-11D2-AA64-00C04F688EAE';  
```  
  
## <a name="see-also"></a>関連項目  
 [メンテナンス プラン](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [データベース メンテナンス プラン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
