---
title: sp_help_log_shipping_secondary_database (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_secondary_database
- sp_help_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_secondary_database
ms.assetid: 11ce42ca-d3f1-44c8-9cac-214ca8896b9a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 65c4cd3f6ca07f2c3cb35dc7dcbaad373930ecc5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066809"
---
# <a name="sphelplogshippingsecondarydatabase-transact-sql"></a>sp_help_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  1 つ以上のセカンダリ データベースの設定を取得します。  
  

  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database' OR  
[ @secondary_id = ] 'secondary_id'  
```  
  
## <a name="arguments"></a>引数  
`[ @secondary_database = ] 'secondary_database'` セカンダリ データベースの名前です。 *secondary_database*は**sysname**、既定値はありません。  
  
`[ @secondary_id = ] 'secondary_id'` ログ配布構成におけるセカンダリ サーバーの ID。 *secondary_id*は**uniqueidentifier** NULL にすることはできません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|説明|  
|-----------------|-----------------|  
|**secondary_id**|ログ配布構成におけるセカンダリ サーバーの ID。|  
|**primary_server**|プライマリ インスタンスの名前、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ログ配布構成にします。|  
|**primary_database**|ログ配布構成におけるプライマリ データベースの名前。|  
|**backup_source_directory**|プライマリ サーバーからのトランザクション ログ バックアップ ファイルの保存先ディレクトリ。|  
|**backup_destination_directory**|バックアップ ファイルがコピー先のセカンダリ サーバー上のディレクトリ。|  
|**file_retention_period**|バックアップ ファイルが削除されるまで、セカンダリ サーバーで保持される分単位の時間の長さ。|  
|**copy_job_id**|セカンダリ サーバーでのコピー ジョブに関連付けられた ID。|  
|**restore_job_id**|セカンダリ サーバー上の復元ジョブに関連付けられている ID です。|  
|**monitor_server**|インスタンスの名前、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ログ配布構成で監視サーバーとして使用されています。|  
|**monitor_server_security_mode**|監視サーバーへの接続に使用されるセキュリティ モード。<br /><br /> 1 = [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証。<br /><br /> 0 =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。|  
|**secondary_database**|ログ配布構成におけるセカンダリ データベースの名前。|  
|**restore_delay**|セカンダリ サーバーが指定されたバックアップ ファイルを復元する前に待機する分単位の時間数。 既定値は、0 分です。|  
|**restore_all**|1 に設定すると、セカンダリ サーバーでは復元ジョブの実行時にすべてのトランザクション ログ バックアップが復元されます。 それ以外の場合、1 つのファイルを復元した後を停止します。|  
|**restore_mode**|セカンダリ データベースの復元モード。<br /><br /> 0 = NORECOVERY でログを復元します。<br /><br /> 1 = STANDBY でログを復元します。|  
|**disconnect_users**|かどうか 1 に設定、ユーザーが切断されているセカンダリ データベースから復元操作を実行します。 既定 = 0。|  
|**block_size**|サイズ (バイト単位) をバックアップ デバイスのブロック サイズとして使用されます。|  
|**buffer_count**|バックアップまたは復元操作で使用されるバッファーの合計数。|  
|**max_transfer_size**|サイズをバイト単位の最大入力または出力要求によって発行された[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]バックアップ デバイスにします。|  
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
|**last_restored_latency**|プライマリ ログ バックアップの作成時に、セカンダリで復元された場合との間経過した時間 (分) の量。<br /><br /> 初期値には NULL です。|  
  
## <a name="remarks"></a>コメント  
 含める場合は、 *secondary_database*パラメーター、結果セットが含まれますセカンダリ データベースに関する情報を含める場合、 *secondary_id*パラメーター、結果セットが含まれますそのセカンダリ ID に関連付けられているすべてのセカンダリ データベースに関する情報  
  
 **sp_help_log_shipping_secondary_database**から実行する必要があります、**マスター**セカンダリ サーバー上のデータベース。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールは、この手順を実行できます。  
  
## <a name="see-also"></a>関連項目  
 [sp_help_log_shipping_secondary_primary &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-primary-transact-sql.md)   
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
