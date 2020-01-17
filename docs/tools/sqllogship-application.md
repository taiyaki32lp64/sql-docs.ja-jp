---
title: sqllogship アプリケーション |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- sqllogship
ms.assetid: 8ae70041-f3d9-46e4-8fa8-31088572a9f8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0e59ba2473ce58caebcb76521dcc191479abdb92
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2019
ms.locfileid: "68065450"
---
# <a name="sqllogship-application"></a>sqllogship アプリケーション
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **sqllogship** アプリケーションは、ログ配布構成のバックアップ、コピー、復元操作、および関連するクリーンアップ作業を行います。 操作は、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の特定のインスタンスで特定のデータベースに対して行われます。  
  
 構文規則の詳細については、「![コマンド プロンプト ユーティリティ リファレンス &#40;データベース エンジン&#41;](../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン")」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqllogship -server instance_name { -backup primary_id | -copy secondary_id | -restore secondary_id } [ -verboselevel level ] [ -logintimeout timeout_value ] [ -querytimeout timeout_value ]  
```  
  
## <a name="arguments"></a>引数  
 **-server** _instance_name_  
 操作を実行する [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスを指定します。 指定するサーバー インスタンスは、指定するログ配布操作によって異なります。 **-backup**を指定する場合、 *instance_name* は、ログ配布構成のプライマリ サーバーの名前にする必要があります。 **-copy** または **-restore**を指定する場合、 *instance_name* は、ログ配布構成のセカンダリ サーバーの名前にする必要があります。  
  
 **-backup** _primary_id_  
 *primary_id*でプライマリ ID を指定したプライマリ データベースのバックアップ操作を行います。 この ID を取得するには、 [log_shipping_primary_databases](../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md) システム テーブルから選択するか、 [sp_help_log_shipping_primary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md) ストアド プロシージャを使用します。  
  
 バックアップ操作を行うと、バックアップ ディレクトリにログ バックアップが作成されます。 その後、ファイル保有期間に基づき、 **sqllogship** アプリケーションによって古いバックアップ ファイルが削除されます。 次に、プライマリ サーバーと監視サーバーにバックアップ操作の履歴ログが記録されます。 最後に、保有期間に基づき古い履歴情報を削除するため、 [sp_cleanup_log_shipping_history](../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)が実行されます。  
  
 **-copy** _secondary_id_  
 *secondary_id*でセカンダリ ID を指定したセカンダリ データベースのバックアップを、指定したセカンダリ サーバーからコピーするコピー操作を行います。 この ID を取得するには、 [log_shipping_secondary](../relational-databases/system-tables/log-shipping-secondary-transact-sql.md) システム テーブルから選択するか、 [sp_help_log_shipping_secondary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md) ストアド プロシージャを使用します。  
  
 この操作を行うと、バックアップ ディレクトリからコピー先ディレクトリにバックアップ ファイルがコピーされます。 その後、 **sqllogship** アプリケーションによって、セカンダリ サーバーと監視サーバーにコピー操作の履歴ログが記録されます。  
  
 **-restore** _secondary_id_  
 *secondary_id*でセカンダリ ID を指定したセカンダリ データベースを取得するため、指定したセカンダリ サーバーで復元操作を行います。 この ID を取得するには、 **sp_help_log_shipping_secondary_database** ストアド プロシージャを使用します。  
  
 復元先ディレクトリにある、最新の復元ポイント以降に作成されたバックアップ ファイルは、セカンダリ データベースに復元されます。 その後、ファイル保有期間に基づき、 **sqllogship** アプリケーションによって古いバックアップ ファイルが削除されます。 次に、セカンダリ サーバーと監視サーバーに復元操作の履歴ログが記録されます。 最後に、保有期間に基づき古い履歴情報を削除するため、 **sp_cleanup_log_shipping_history**が実行されます。  
  
 **-verboselevel** _level_  
 ログ配布の履歴に追加するメッセージのレベルを指定します。 *level* は、次のいずれかの整数です。  
  
|level|[説明]|  
|-----------|-----------------|  
|0|トレースおよびデバッグのメッセージを出力しません。|  
|1|エラー処理メッセージを出力します。|  
|2|警告およびエラー処理メッセージを出力します。|  
|**3**|情報メッセージ、警告、およびエラー処理メッセージを出力します。 これが既定値です。|  
|4|すべてのデバッグおよびトレースのメッセージを出力します。|  
  
 **-logintimeout** _timeout_value_  
 サーバー インスタンスへのログインを試みてからタイムアウトするまでの時間を指定します。既定値は 15 秒です。 *timeout_value* のデータ型は **int**_です。_  
  
 **-querytimeout** _timeout_value_  
 指定した操作を開始してからタイムアウトするまでの時間を指定します。既定では、タイムアウトはありません。 *timeout_value* のデータ型は **int**_です。_  
  
## <a name="remarks"></a>Remarks  
 可能な限り、バックアップ、コピー、および復元ジョブでバックアップ、コピー、および復元を行うことをお勧めします。 バッチ操作や他のアプリケーションからこれらのジョブを開始するには、 [sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md) ストアド プロシージャを呼び出します。  
  
 **sqllogship** で作成されるログ配布の履歴には、ログ配布のバックアップ、コピー、および復元ジョブで作成される履歴も含まれます。 **sqllogship** を繰り返し使用してログ配布構成のバックアップ、コピー、および復元操作を行う場合、対応するログ配布ジョブを無効にすることを検討してください。 詳細については、「 [Disable or Enable a Job](../ssms/agent/disable-or-enable-a-job.md)」をご覧ください。  
  
 **sqllogship** アプリケーション  (SqlLogShip.exe) は、x:\Program Files\Microsoft SQL Server\130\Tools\Binn ディレクトリにインストールされます。  
  
## <a name="permissions"></a>アクセス許可  
 **sqllogship** では Windows 認証を使用します。 コマンドを実行する Windows 認証アカウントには、Windows のディレクトリ アクセスおよび [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の権限が必要です。 要件は、 **sqllogship** コマンドで **-backup**、 **-copy**、 **-restore** のいずれのオプションを指定するかで変わります。  
  
|オプション|ディレクトリ アクセス|アクセス許可|  
|------------|----------------------|-----------------|  
|**-backup**|バックアップ ディレクトリの読み取り/書き込みアクセス許可が必要です。|BACKUP ステートメントと同一の権限が必要です。 詳細については、「 [BACKUP &#40;Transact-SQL&#41;](../t-sql/statements/backup-transact-sql.md)」を参照してください。|  
|**-copy**|バックアップ ディレクトリの読み取りアクセス許可と、コピー ディレクトリの書き込みアクセス許可が必要です。|[sp_help_log_shipping_secondary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md) ストアド プロシージャと同一の権限が必要です。|  
|**-restore**|コピー ディレクトリの読み取り/書き込みアクセス許可が必要です。|RESTORE ステートメントと同一の権限が必要です。 詳細については、「[RESTORE &#40;Transact-SQL&#41;](../t-sql/statements/restore-statements-transact-sql.md)」を参照してください。|  
  
> [!NOTE]  
>  バックアップ ディレクトリおよびコピー ディレクトリのパスを検索するには、**sp_help_log_shipping_secondary_database** ストアド プロシージャを実行するか、**msdb** の **log_shipping_secondary** テーブルを参照します。 バックアップ ディレクトリおよびコピー先ディレクトリのパスはそれぞれ、 **backup_source_directory** 列および **backup_destination_directory** 列にあります。  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [log_shipping_primary_databases &#40;Transact-SQL&#41;](../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)   
 [log_shipping_secondary &#40;Transact-SQL&#41;](../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_help_log_shipping_primary_database &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [sp_start_job &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)  
  
  
