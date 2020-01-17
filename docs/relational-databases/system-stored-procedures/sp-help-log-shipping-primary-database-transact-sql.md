---
title: sp_help_log_shipping_primary_database (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_primary_database_TSQL
- sp_help_log_shipping_primary_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_primary_database
ms.assetid: e711b01c-ef29-4eb6-a016-0e647e337818
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9559a882da12c3e2a7a48a0aaa656a554633aa6f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937913"
---
# <a name="sphelplogshippingprimarydatabase-transact-sql"></a>sp_help_log_shipping_primary_database (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  プライマリ データベースの設定を取得します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_log_shipping_primary_database  
[ @database = ] 'database' OR  
[ @primary_id = ] 'primary_id'  
```  
  
## <a name="arguments"></a>引数  
`[ @database = ] 'database'` ログ配布プライマリ データベースの名前です。 *データベース*は**sysname**、既定値はありません、NULL にすることはできません。  
  
`[ @primary_id = ] 'primary_id'` ログ配布構成におけるプライマリ データベースの ID。 *primary_id*は**uniqueidentifier** NULL にすることはできません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|説明|  
|-----------------|-----------------|  
|**primary_id**|ログ配布構成におけるプライマリ データベースの ID。|  
|**primary_database**|ログ配布構成におけるプライマリ データベースの名前。|  
|**backup_directory**|プライマリ サーバーからのトランザクション ログ バックアップ ファイルの保存先ディレクトリ。|  
|**backup_share**|ネットワークまたはバックアップ ディレクトリへの UNC パス。|  
|**backup_retention_period**|バックアップ ディレクトリでログ バックアップ ファイルが保持される時間 (分単位)。この時間を過ぎるとファイルは削除されます。|  
|**backup_compression**|ログ配布構成を使用するかどうかを示す[バックアップの圧縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)します。<br /><br /> **0** = 無効になっています。 ログ バックアップは圧縮されません。<br /><br /> **1** = 有効にします。 常にログ バックアップを圧縮します。<br /><br /> **2** = の設定を使用して、 [backup compression default サーバー構成オプションの構成を表示または](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)します。 これは既定値です。<br /><br /> バックアップの圧縮がでのみサポートされている[!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)](またはそれ以降のバージョン)。 その他のエディションでは、値は常に 2 です。|  
|**backup_job_id**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プライマリ サーバー上のバックアップ ジョブに関連付けられているエージェント ジョブの ID。|  
|**monitor_server**|インスタンスの名前、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ログ配布構成で監視サーバーとして使用されています。|  
|**monitor_server_security_mode**|監視サーバーへの接続に使用されるセキュリティ モード。<br /><br /> 1 = [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証。<br /><br /> 0 =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。|  
|**backup_threshold**|分単位の許容経過時間を通知する前にバックアップ操作の数が生成されます。|  
|**threshold_alert**|バックアップのしきい値を超えたときに発生する警告。|  
|**threshold_alert_enabled**|バックアップのしきい値のアラートが有効になっているかどうかを決定します。<br /><br /> **1** = 有効にします。<br /><br /> **0** = 無効になっています。|  
|**last_backup_file**|最新のトランザクション ログ バックアップの絶対パス。|  
|**last_backup_date**|最後のログ バックアップ操作の日時。|  
|**last_backup_date_utc**|最後のトランザクションの日付と時刻は、世界協定時刻で表される、プライマリ データベースでバックアップ操作にログインします。|  
|**history_retention_period**|指定したプライマリ データベースでログ配布履歴レコードが保持される時間 (分単位)。この時間を過ぎるとレコードは削除されます。|  
  
## <a name="remarks"></a>コメント  
 **sp_help_log_shipping_primary_database**から実行する必要があります、**マスター**プライマリ サーバー上のデータベース。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールは、この手順を実行できます。  
  
## <a name="examples"></a>使用例  
 この例を使用して**sp_help_log_shipping_primary_database**データベースのプライマリ データベースの設定を取得する[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]します。  
  
```  
EXEC master.dbo.sp_help_log_shipping_primary_database @database=N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
