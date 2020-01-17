---
title: managed_backup.sp_get_backup_diagnostics (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_get_backup_diagnostics_TSQL
- sp_get_backup_diagnostics
- smart_admin.sp_get_backup_diagnostics_TSQL
- smart_admin.sp_get_backup_diagnostics
dev_langs:
- TSQL
helpviewer_keywords:
- sp_get_backup_diagnostics
- smart_admin.sp_get_backup_diagnostics
ms.assetid: 2266a233-6354-464b-91ec-824ca4eb9ceb
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5e967ae5b46ec703da4e8b1fff64f298fdf8a081
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942043"
---
# <a name="managedbackupspgetbackupdiagnostics-transact-sql"></a>managed_backup.sp_get_backup_diagnostics (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  スマート管理者によってログに記録、拡張イベントを返します  
  
 このストアド プロシージャを使用して、スマート管理者によってログに記録、拡張イベントを監視するには[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]イベントは、このシステムに記録されますと確認できるし、このストアド プロシージャを使用して監視します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
managed_backup.sp_get_backup_diagnostics [@xevent_channel = ] 'event type' [, [@begin_time = ] 'time1' ] [, [@end_time = ] 'time2'VARCHAR(255) = 'Xevent',@begin_time DATETIME = NULL,@end_time DATETIME = NULL  
```  
  
##  <a name="Arguments"></a> 引数  
 @xevent_channel  
 拡張イベントの種類。 既定値は、それまでの 30 分間にログに記録されたすべてのイベントを返すよう設定されています。 記録されたイベントは、有効になっている拡張イベントの種類によって異なります。 このパラメーターを使用すると、特定の種類のイベントのみが表示されるようにストアド プロシージャにフィルターを適用できます。 イベントの完全名を指定するかなどの部分文字列を指定できます。 **'Admin'** 、 **'Analytic'** 、 **'Operational'** 、および **'Debug'** します。 @event_channelは**VARCHAR (255)** します。  
  
 イベントの種類が現在有効になって使用の一覧を取得する、 **managed_backup.fn_get_current_xevent_settings**関数。  
  
 [@begin_time  
 イベントが表示対象となる期間の開始時刻。 @begin_timeパラメーターは DATETIME で、既定値は NULL です。 これが指定されていない場合は、過去 30 分からのイベントが表示されます。  
  
 @end_time  
 イベントが表示対象となる期間の終了時刻。 @end_timeパラメーターでは、DATATIME が既定値は NULL です。  これを指定しない場合は、現在までのイベントが表示されます。  
  
## <a name="table-returned"></a>返されるテーブル  
 このストアド プロシージャには、次の情報を含むテーブルが返されます。  
  
||||  
|-|-|-|  
|列名|データ型|説明|  
|event_type|NVARCHAR (512)|拡張イベントの種類。|  
|event|NVARCHAR (512)|イベント ログの概要|  
|Timestamp|timestamp|イベントの発生時刻を示す、イベントのタイムスタンプ|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 必要があります**EXECUTE**ストアド プロシージャに対する権限。 また必要もあります**VIEW SERVER STATE**が内部的に他のシステム オブジェクトを呼び出すためのアクセス許可がこのアクセス許可が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、過去 30 分間にログに記録されたすべてのイベントが返されます。  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics  
  
```  
  
 次の例では、特定の時間範囲に記録されたすべてのイベントを返します。  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics @xevent_channel = 'Admin',  
  @begin_time = '2013-06-01', @end_time = '2013-06-10'  
  
```  
  
 次の例では、過去 30 分間にログに記録されたすべての分析イベントが返されます。  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics @xevent_channel = 'Analytic'  
  
```  
  
  
