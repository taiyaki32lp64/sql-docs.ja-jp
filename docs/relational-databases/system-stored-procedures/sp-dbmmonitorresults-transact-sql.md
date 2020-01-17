---
title: sp_dbmmonitorresults (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorresults
- sp_dbmmonitorresults_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorresults
- database mirroring [SQL Server], monitoring
ms.assetid: d575e624-7d30-4eae-b94f-5a7b9fa5427e
author: stevestein
ms.author: sstein
ms.openlocfilehash: e46116111e9f1e85cdaad48e9742e62fba187e74
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899177"
---
# <a name="spdbmmonitorresults-transact-sql"></a>sp_dbmmonitorresults (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース ミラーリング監視履歴が格納されている状態テーブルから、監視対象データベースの状態行を返します。事前に、このプロシージャで最新の状態を取得するかどうかを選択できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dbmmonitorresults database_name   
   , rows_to_return  
    , update_status   
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 ミラーリングの状態を返すデータベースを指定します。  
  
 *rows_to_return*  
 返す行の量を指定します。  
  
 0 = 最後の行  
  
 1 = 過去 2 時間の行  
  
 2 行の最後の 4 時間を =  
  
 3 = 過去 8 時間の行  
  
 4 行の最後の日を =  
  
 5 = 過去 2 日間の行  
  
 6 最後の行を =  
  
 7 = 最後の 500 行  
  
 8 = 最後 1,000 行  
  
 9 = 最新 1,000,000 行  
  
 *update_status*  
 プロシージャの結果を返す前にことを指定します。  
  
 0 = は、データベースの状態を更新できません。 結果は最新 2 行のみから計算されます。行の古さは状態テーブルが更新された日時を基に判断されます。  
  
 1 = データベースの状態を呼び出して更新**sp_dbmmonitorupdate**結果を計算する前にします。 ただし、状態テーブルが直前の 15 秒、またはユーザー内で更新されている場合はのメンバー、 **sysadmin**固定サーバー ロール、 **sp_dbmmonitorresults**状態を更新することがなく実行されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
 指定されたデータベースの履歴の状態の要求された行数を返します。 各行には、次の情報が含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|ミラー化されたデータベースの名前です。|  
|**role**|**int**|現在のミラーリング サーバー インスタンスのロール:<br /><br /> 1 = プリンシパル<br /><br /> 2 = ミラー|  
|**mirroring_state**|**int**|データベースの状態。<br /><br /> 0 = 中断状態<br /><br /> 1 = 切断<br /><br /> 2 = 同期中<br /><br /> 3 = フェールオーバーを保留しています<br /><br /> 4 = 同期済み|  
|**witness_status**|**int**|データベース ミラーリング セッションのデータベースのミラーリング監視サーバーの接続の状態を指定できます。<br /><br /> 0 = 不明<br /><br /> 1 = 接続済み<br /><br /> 2 = 切断|  
|**log_generation_rate**|**int**|1 秒あたりのキロバイトの前にこのデータベースのミラーリングの状態の更新以降に生成されたログの量。|  
|**unsent_log**|**int**|送信キュー キロバイト単位でプリンシパルにある未送信ログのサイズ。|  
|**send_rate**|**int**|プリンシパルからキロバイト/秒でミラーへのログのレートを送信します。|  
|**unrestored_log**|**int**|キロバイト単位でミラー サーバーで再実行キューのサイズ。|  
|**recovery_rate**|**int**|ミラーの再実行率 (KB/秒単位)。|  
|**transaction_delay**|**int**|ミリ秒単位ですべてのトランザクションの遅延の合計。|  
|**transactions_per_sec**|**int**|サーバー インスタンスのプリンシパルで 1 秒あたり発生しているトランザクションの数。|  
|**average_delay**|**int**|データベース ミラーリングのためには、各トランザクションのプリンシパル サーバー インスタンスでの平均遅延です。 高パフォーマンス モードで (は、設定すると、SAFETY プロパティが OFF に)、通常この値は 0。|  
|**time_recorded**|**datetime**|データベース ミラーリング監視で行が記録された時間。 これは、プリンシパルのシステム クロックの時間です。|  
|**time_behind**|**datetime**|ミラー データベースが現在をキャッチするプリンシパルのシステム クロックのおおよその時間。 この値はプリンシパル サーバー インスタンスでのみ意味を持ちます。|  
|**local_time**|**datetime**|この行が更新されたときのローカル サーバー インスタンスのシステム クロック時間。|  
  
## <a name="remarks"></a>コメント  
 **sp_dbmmonitorresults**のコンテキストでのみ実行できる、 **msdb**データベース。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **sysadmin**固定サーバー ロールまたは、 **dbm_monitor**固定データベース ロール、 **msdb**データベース。 **Dbm_monitor**役割は、データベース ミラーリングの状態を表示がない更新しますが、ない表示または構成するデータベース ミラーリング イベントは、そのメンバーを使用できます。  
  
> [!NOTE]  
>  初めて**sp_dbmmonitorupdate**の実行が作成されます、 **dbm_monitor**固定データベース ロール、 **msdb**データベース。 メンバー、 **sysadmin**すべてのユーザーを追加できるは、固定サーバー ロール、 **dbm_monitor**固定データベース ロール。  
  
## <a name="examples"></a>使用例  
 次の例では、データベースの状態を更新することがなく、過去 2 時間に記録された行を返します。  
  
```  
USE msdb;  
EXEC sp_dbmmonitorresults AdventureWorks2012, 2, 0;  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース ミラーリングの監視 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangemonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitoraddmonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)   
 [sp_dbmmonitordropmonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorupdate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)  
  
  
