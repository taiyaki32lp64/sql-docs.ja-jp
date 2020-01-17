---
title: sp_help_log_shipping_monitor_secondary (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_monitor_secondary
- sp_help_log_shipping_monitor_secondary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_monitor_secondary
ms.assetid: 3ac091ea-c9a8-4c05-a0b6-1ccf4e001339
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b1acf456bda88eeee0493d3f9d7ccc063a5bda50
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001012"
---
# <a name="sphelplogshippingmonitorsecondary-transact-sql"></a>sp_help_log_shipping_monitor_secondary (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  監視テーブルからセカンダリ データベースに関する情報を返します。  
  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_log_shipping_monitor_secondary  
[ @secondary_server = ] 'secondary_server',  
[ @secondary_database = ] 'secondary_database'  
```  
  
## <a name="arguments"></a>引数  
`[ @secondary_server = ] 'secondary_server'` セカンダリ サーバーの名前です。 *secondary_server*は**sysname**、既定値はありません。  
  
`[ @secondary_database = ] 'secondary_database'` セカンダリ データベースの名前です。 *secondary_database*は**sysname**、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|[列]|説明|  
|------------|-----------------|  
|**secondary_server**|セカンダリ インスタンスの名前、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ログ配布構成にします。|  
|**secondary_database**|ログ配布構成におけるセカンダリ データベースの名前。|  
|**secondary_id**|ログ配布構成におけるセカンダリ サーバーの ID。|  
|**primary_server**|ログ配布構成における [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のプライマリ インスタンスの名前。|  
|**primary_database**|ログ配布構成におけるプライマリ データベースの名前。|  
|**restore_threshold**|許容経過時間を分単位の数は、アラートを生成する前に、操作を復元します。|  
|**threshold_alert**|復元のしきい値を超えたときに発生する警告。|  
|**threshold_alert_enabled**|復元のしきい値の警告を有効にするかどうか。<br /><br /> 1 = 有効にします。<br /><br /> 0 = 無効になっています。|  
|**last_copied_file**|セカンダリ サーバーにコピーされた最後のバックアップ ファイルの名前。|  
|**last_copied_date**|セカンダリ サーバーに最後にコピー操作の日付と時刻。|  
|**last_copied_date_utc**|世界協定時刻で表される、セカンダリ サーバーに最後にコピー操作の日付と時刻。|  
|**last_restored_file**|セカンダリ データベースに復元される最後のバックアップ ファイルの名前。|  
|**last_restored_date**|最後の日付と時刻は、セカンダリ データベースに対する操作を復元します。|  
|**last_restored_date_utc**|最後の日付と時刻、世界協定時刻で表される、セカンダリ データベースに対する操作を復元します。|  
|**history_retention_period**|時間、分単位でログ配布履歴されるレコードは削除する前に特定のセカンダリ データベースに保持されます。|  
  
## <a name="remarks"></a>コメント  
 **sp_help_log_shipping_monitor_secondary**から実行する必要があります、**マスター**監視サーバー上のデータベース。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールは、この手順を実行できます。  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
