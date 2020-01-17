---
title: sp_help_log_shipping_monitor_primary (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_monitor_primary
- sp_help_log_shipping_monitor_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_monitor_primary
ms.assetid: d9dfcb8f-1da6-49ca-a2c8-411574915434
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b3f579fb9a263b69755baaa1be84f6d51e9beac1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113843"
---
# <a name="sphelplogshippingmonitorprimary-transact-sql"></a>sp_help_log_shipping_monitor_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  監視テーブルからプライマリ データベースに関する情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_log_shipping_monitor_primary  
[ @primary_server = ] 'primary_server',   
[ @primary_database = ] 'primary_database'  
```  
  
## <a name="arguments"></a>引数  
`[ @primary_server = ] 'primary_server'` プライマリ インスタンスの名前、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ログ配布構成にします。 *primary_server*は**sysname** NULL にすることはできません。  
  
`[ @primary_database = ] 'primary_database'` プライマリ サーバー上のデータベースの名前です。 *primary_database*は**sysname**、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|説明|  
|-----------------|-----------------|  
|**primary_id**|ログ配布構成におけるプライマリ データベースの ID。|  
|**primary_server**|ログ配布構成における [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のプライマリ インスタンスの名前。|  
|**primary_database**|ログ配布構成におけるプライマリ データベースの名前。|  
|**backup_threshold**|分単位の許容経過時間を通知する前にバックアップ操作の数が生成されます。|  
|**threshold_alert**|バックアップのしきい値を超えたときに発生する警告。|  
|**threshold_alert_enabled**|バックアップのしきい値のアラートが有効になっているかどうかを決定します。 1 = 有効になっています。0 = 無効になっています。|  
|**last_backup_file**|最新のトランザクション ログ バックアップの絶対パス。|  
|**last_backup_date**|最後のトランザクションの日付と時刻は、プライマリ データベースでバックアップ操作にログインします。|  
|**last_backup_date_utc**|最後のトランザクションの日付と時刻は、世界協定時刻で表される、プライマリ データベースでバックアップ操作にログインします。|  
|**history_retention_period**|指定したプライマリ データベースでログ配布履歴レコードが保持される時間 (分単位)。この時間を過ぎるとレコードは削除されます。|  
  
## <a name="remarks"></a>コメント  
 **sp_help_log_shipping_monitor_primary**から実行する必要があります、**マスター**監視サーバー上のデータベース。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールは、この手順を実行できます。  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
