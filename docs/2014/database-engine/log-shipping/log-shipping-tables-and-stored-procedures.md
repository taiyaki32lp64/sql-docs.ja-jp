---
title: ログ配布テーブルとストアド プロシージャ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- secondary servers [SQL Server]
- monitor servers [SQL Server]
- log shipping [SQL Server], system tables
- log shipping [SQL Server], stored procedures
- primary servers [SQL Server]
ms.assetid: 03420810-4c38-4c0c-adf0-913eb044c50a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d88e0826617b63638c720f176da84a85d68a7e18
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774501"
---
# <a name="log-shipping-tables-and-stored-procedures"></a>Log Shipping Tables and Stored Procedures
  このトピックでは、ログ配布構成に関連付けられているすべてのテーブルおよびストアド プロシージャについて説明します。 すべてのログ配布テーブルは、各サーバーの **msdb** に保存されます。 次の表は、ログ配布構成にあるどのサーバーで、どのテーブルおよびストアド プロシージャが使用されるかを示しています。  
  
## <a name="primary-server-tables"></a>プライマリ サーバーのテーブル  
  
|テーブル|説明|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](/sql/relational-databases/system-tables/log-shipping-monitor-alert-transact-sql)|警告ジョブ ID を格納します。 リモート監視サーバーが構成されていない場合のみ、このテーブルがプライマリ サーバーで使用されます。|  
|[log_shipping_monitor_error_detail](/sql/relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql)|このプライマリ サーバーに関連付けられているログ配布ジョブのエラー詳細を格納します。|  
|[log_shipping_monitor_history_detail](/sql/relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql)|このプライマリ サーバーに関連付けられているログ配布ジョブの履歴詳細を格納します。|  
|[log_shipping_monitor_primary](/sql/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql)|このプライマリ データベースの 1 つの監視レコードを格納します。|  
|[log_shipping_primary_databases](/sql/relational-databases/system-tables/log-shipping-primary-databases-transact-sql)|特定のサーバー上にあるプライマリ データベースの構成情報を格納します。 プライマリ データベースごとに 1 行ずつ格納します。|  
|[log_shipping_primary_secondaries](/sql/relational-databases/system-tables/log-shipping-primary-secondaries-transact-sql)|プライマリ データベースをセカンダリ データベースにマッピングします。|  
  
## <a name="primary-server-stored-procedures"></a>プライマリ サーバーのストアド プロシージャ  
  
|ストアド プロシージャ|説明|  
|----------------------|-----------------|  
|[sp_add_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql)|バックアップ ジョブ、ローカル監視レコード、リモート監視レコードを含め、ログ配布構成のプライマリ データベースを設定します。|  
|[sp_add_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-secondary-transact-sql)|既存のプライマリ データベースにセカンダリ データベース名を追加します。|  
|[sp_change_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql)|ローカル監視レコードやリモート監視レコードなど、プライマリ データベースの設定を変更します。|  
|[sp_cleanup_log_shipping_history](/sql/relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql)|保持期間に基づいて、ローカルおよびモニター上の履歴をクリーンアップします。|  
|[sp_delete_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql)|バックアップ ジョブ、ローカル履歴、リモート履歴など、プライマリ データベースのログ配布を削除します。|  
|[sp_delete_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql)|プライマリ データベースからセカンダリ データベース名を削除します。|  
|[sp_help_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql)|プライマリ データベースの設定を取得し、 **log_shipping_primary_databases** テーブルと **log_shipping_monitor_primary** テーブルの値を表示します。|  
|[sp_help_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-secondary-transact-sql)|プライマリ データベースのセカンダリ データベース名を取得します。|  
|[sp_refresh_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql)|指定したログ配布エージェントの最新情報でモニターを更新します。|  
  
## <a name="secondary-server-tables"></a>セカンダリ サーバーのテーブル  
  
|テーブル|説明|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](/sql/relational-databases/system-tables/log-shipping-monitor-alert-transact-sql)|警告ジョブ ID を格納します。 リモート監視サーバーが構成されていない場合のみ、このテーブルがセカンダリ サーバーで使用されます。|  
|[log_shipping_monitor_error_detail](/sql/relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql)|このセカンダリ サーバーに関連付けられているログ配布ジョブのエラー詳細を格納します。|  
|[log_shipping_monitor_history_detail](/sql/relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql)|このセカンダリ サーバーに関連付けられているログ配布ジョブの履歴詳細を格納します。|  
|[log_shipping_monitor_secondary](/sql/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql)|このセカンダリ サーバーに関連付けられているセカンダリ データベースごとに 1 つの監視レコードを格納します。|  
|[log_shipping_secondary](/sql/relational-databases/system-tables/log-shipping-secondary-transact-sql)|特定のサーバー上にあるセカンダリ データベースの構成情報を格納します。 セカンダリ ID ごとに 1 行ずつ格納します。|  
|[log_shipping_secondary_databases](/sql/relational-databases/system-tables/log-shipping-secondary-databases-transact-sql)|特定のセカンダリ データベースの構成情報を格納します。 セカンダリ データベースごとに 1 行ずつ格納します。|  
  
> [!NOTE]  
>  特定のプライマリ データベースと同じセカンダリ サーバー上にあるセカンダリ データベースでは、 **log_shipping_secondary** テーブルの設定が共有されます。 1 つのセカンダリ データベースで共有設定が変更されると、すべてのセカンダリ データベースで設定が変更されます。  
  
## <a name="secondary-server-stored-procedures"></a>セカンダリ サーバーのストアド プロシージャ  
  
|ストアド プロシージャ|説明|  
|----------------------|-----------------|  
|[sp_add_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql)|ログ配布についてセカンダリ データベースを設定します。|  
|[sp_add_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-primary-transact-sql)|指定したプライマリ データベースのセカンダリ サーバーに対して、プライマリ情報の設定、ローカルおよびリモート監視リンクの追加、コピー ジョブと復元ジョブの作成を行います。|  
|[sp_change_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql)|ローカル監視レコードやリモート監視レコードなど、セカンダリ データベースの設定を変更します。|  
|[sp_change_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-primary-transact-sql)|配布元ディレクトリ、配布先ディレクトリ、ファイル保持期間など、セカンダリ データベースの設定を変更します。|  
|[sp_cleanup_log_shipping_history](/sql/relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql)|保持期間に基づいて、ローカルおよびモニター上の履歴をクリーンアップします。|  
|[sp_delete_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql)|セカンダリ データベース、ローカル履歴、およびリモート履歴を削除します。|  
|[sp_delete_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-primary-transact-sql)|指定したプライマリ サーバーについての情報をセカンダリ サーバーから削除します。|  
|[sp_help_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql)|**log_shipping_secondary**、 **log_shipping_secondary_databases**、および **log_shipping_monitor_secondary** の各テーブルからセカンダリ データベースの設定を取得します。|  
|[sp_help_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-primary-transact-sql)|セカンダリ サーバーにある指定されたプライマリ データベースの設定を取得します。|  
|[sp_refresh_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql)|指定したログ配布エージェントの最新情報でモニターを更新します。|  
  
## <a name="monitor-server-tables"></a>監視サーバーのテーブル  
  
|テーブル|説明|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](/sql/relational-databases/system-tables/log-shipping-monitor-alert-transact-sql)|警告ジョブ ID を格納します。|  
|[log_shipping_monitor_error_detail](/sql/relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql)|ログ配布ジョブのエラーの詳細を格納します。|  
|[log_shipping_monitor_history_detail](/sql/relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql)|ログ配布ジョブの履歴詳細を格納します。|  
|[log_shipping_monitor_primary](/sql/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql)|この監視サーバーに関連付けられているプライマリ データベースごとに 1 つの監視レコードを格納します。|  
|[log_shipping_monitor_secondary](/sql/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql)|この監視サーバーに関連付けられているセカンダリ データベースごとに 1 つの監視レコードを格納します。|  
  
## <a name="monitor-server-stored-procedures"></a>監視サーバーのストアド プロシージャ  
  
|ストアド プロシージャ|説明|  
|----------------------|-----------------|  
|[sp_add_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-alert-job-transact-sql)|ログ配布警告ジョブがまだ作成されていない場合は、作成します。|  
|[sp_delete_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-alert-job-transact-sql)|プライマリ データベースが関連付けられていない場合は、ログ配布警告ジョブを削除します。|  
|[sp_help_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-alert-job-transact-sql)|警告ジョブのジョブ ID を返します。|  
|[sp_help_log_shipping_monitor_primary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql)|**log_shipping_monitor_primary** テーブルから、指定したプライマリ データベースの監視レコードを返します。|  
|[sp_help_log_shipping_monitor_secondary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql)|**log_shipping_monitor_secondary** テーブルから、指定したセカンダリ データベースの監視レコードを返します。|  
  
  
