---
title: ログ配布の監視 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], status
- history tables [SQL Server]
- historical information [SQL Server], log shipping
- log shipping [SQL Server], monitoring
- alerts [SQL Server], log shipping
- status information [SQL Server], log shipping
- monitoring log shipping [SQL Server]
ms.assetid: acf3cd99-55f7-4287-8414-0892f830f423
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 33bb8320abf11400e5224af747d71bcb49fc2d16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030711"
---
# <a name="monitor-log-shipping-transact-sql"></a>ログ配布の監視 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ログ配布を構成すると、すべてのログ配布サーバーの状態に関する情報を監視できます。 ログ配布操作の履歴と状態は、ログ配布ジョブにより、常にローカルに保存されます。 バックアップ操作の履歴と状態はプライマリ サーバーに格納され、コピー操作と復元操作の履歴と状態はセカンダリ サーバーに格納されます。 リモートの監視サーバーを実装している場合、この情報はリモートの監視サーバーにも格納されます。  
  
 ログ配布操作がスケジュールどおりに実行されなかった場合に警告を発生させることができます。 エラーは、バックアップ操作と復元操作の状態を監視する警告ジョブによって発生します。 これらのエラーの発生をオペレーターに通知する警告を定義できます。 監視サーバーを構成している場合、警告ジョブは、ログ配布構成に関するすべての操作に対してエラーを発生させる監視サーバーで実行されます。 監視サーバーが指定されていない場合、警告ジョブは、バックアップ操作を監視しているプライマリ サーバー インスタンスで実行されます。 監視サーバーが指定されていない場合、警告ジョブは、ローカルのコピー操作と復元操作を監視している各セカンダリ サーバー インスタンスでも実行されます。  
  
> [!IMPORTANT]  
>  ログ配布構成を監視するには、ログ配布を有効にするときに監視サーバーを追加する必要があります。 監視サーバーを後で追加する場合は、ログ配布構成を削除して、代わりに監視サーバーを含む新しい構成を用意します。 詳細については、「 [ログ配布の構成 &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)で導入されました。 監視サーバーは、一度構成すると、最初にログ配布を削除しない限り変更できません。  
  
## <a name="history-tables-containing-monitoring-information"></a>監視情報を含む履歴テーブル  
 監視の履歴テーブルには、監視サーバーに格納されているメタデータが含まれています。 また、指定されているプライマリ サーバーやセカンダリ サーバーに固有の情報のコピーもローカルに格納されています。  
  
 これらのテーブルでクエリを実行して、ログ配布セッションの状態を監視できます。 たとえば、ログ配布の状態を参照するには、バックアップ ジョブ、コピー ジョブ、および復元ジョブの状態と履歴を確認します。 以下の監視テーブルをクエリすることにより、特定のログ配布の履歴とエラーの詳細を参照できます。  
  
|テーブル|[説明]|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](../../relational-databases/system-tables/log-shipping-monitor-alert-transact-sql.md)|警告ジョブ ID を格納します。|  
|[log_shipping_monitor_error_detail](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)|ログ配布ジョブのエラーの詳細を格納します。 このテーブルをクエリして、あるエージェント セッションのエラーを参照することができます。 必要に応じて、エラーが記録された日付と時刻でエラーを並べ替えることができます。 各エラーは一連の例外として記録されるので、1 つのエージェント セッションで複数のエラー (シーケンス) が記録されることがあります。|  
|[log_shipping_monitor_history_detail](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)|ログ配布エージェントの履歴の詳細情報を格納します。 このテーブルをクエリして、エージェント セッションの履歴の詳細情報を参照することができます。|  
|[log_shipping_monitor_primary](../../relational-databases/system-tables/log-shipping-monitor-primary-transact-sql.md)|ログ配布構成ごとに、前回のバックアップ ファイルおよび監視に役立つ最後に復元したファイルに関する情報を含む、プライマリ データの管理レコードを格納します。|  
|[log_shipping_monitor_secondary](../../relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql.md)|前回のバックアップ ファイルおよび監視に役立つ最後に復元したファイルに関する情報を含む、セカンダリ データの管理レコードを格納します。|  
  
## <a name="stored-procedures-for-monitoring-log-shipping"></a>ログ配布を監視するためのストアド プロシージャ  
 監視情報と履歴情報は、 **msdb**のテーブルに格納されます。このテーブルには、ログ配布ストアド プロシージャを使用してアクセスできます。 次の表に示すサーバーで、これらのストアド プロシージャを実行します。  
  
|ストアド プロシージャ|[説明]|プロシージャを実行するサーバー|  
|----------------------|-----------------|---------------------------|  
|[sp_help_log_shipping_monitor_primary](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql.md)|**log_shipping_monitor_primary** テーブルから、指定したプライマリ データベースの監視レコードを返します。|監視サーバーまたはプライマリ サーバー|  
|[sp_help_log_shipping_monitor_secondary](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql.md)|**log_shipping_monitor_secondary** テーブルから、指定したセカンダリ データベースの監視レコードを返します。|監視サーバーまたはセカンダリ サーバー|  
|[sp_help_log_shipping_alert_job](../../relational-databases/system-stored-procedures/sp-help-log-shipping-alert-job-transact-sql.md)|警告ジョブのジョブ ID を返します。|監視サーバー (監視サーバーが定義されていない場合はプライマリ サーバーまたはセカンダリ サーバー)|  
|[sp_help_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)|プライマリ データベースの設定を取得し、 **log_shipping_primary_databases** テーブルと **log_shipping_monitor_primary** テーブルの値を表示します。|プライマリ サーバー|  
|[sp_help_log_shipping_primary_secondary](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-secondary-transact-sql.md)|プライマリ データベースのセカンダリ データベース名を取得します。|プライマリ サーバー|  
|[sp_help_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)|**log_shipping_secondary**、 **log_shipping_secondary_databases** 、および **log_shipping_monitor_secondary** の各テーブルからセカンダリ データベースの設定を取得します。|セカンダリ サーバー|  
|[sp_help_log_shipping_secondary_primary &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-primary-transact-sql.md)|セカンダリ サーバーにある指定されたプライマリ データベースの設定を取得します。|セカンダリ サーバー|  
  
## <a name="see-also"></a>参照  
 [ログ配布レポートの表示 &#40;SQL Server Management Studio&#41;](../../database-engine/log-shipping/view-the-log-shipping-report-sql-server-management-studio.md)   
 [ログ配布のストアド プロシージャとテーブル](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  
