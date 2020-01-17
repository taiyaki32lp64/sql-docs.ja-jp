---
title: SQL Server のレプリケーション | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], about
- replication [SQL Server]
ms.assetid: 3a5f4592-3c61-4b4d-9ceb-39716aeeba41
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 427367994418ea7e82288541c89b47cc8bb7ea75
ms.sourcegitcommit: d1bc0dd1ac626ee7034a36b81554258994d72c15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2019
ms.locfileid: "70958351"
---
# <a name="sql-server-replication"></a>SQL Server のレプリケーション
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  レプリケーションとは、あるデータベースから別のデータベースにデータやデータベース オブジェクトをコピーおよび配布し、それらのデータベースを同期させて一貫性を保つための一連のテクノロジです。 レプリケーションを使用すると、ローカル エリア ネットワーク、ワイド エリア ネットワーク、ダイヤルアップ接続、ワイヤレス接続、インターネットなどを経由して、別の場所や、リモート ユーザーまたはモバイル ユーザーにデータを配布することができます。  
  
 トランザクション レプリケーションは、高いスループットが必要とされるサーバー間のシナリオで使用されるのが一般的です。たとえば、スケーラビリティと可用性の向上、データ ウェアハウジングとレポート、複数サイトからのデータの統合、異種データの統合、バッチ処理のオフロードなどのシナリオで使用されます。 マージ レプリケーションは、データの競合の可能性があるモバイル アプリケーションや分散サーバー アプリケーションを主な対象としています。 モバイル ユーザーとのデータ交換、店舗販売時点管理 (POS) アプリケーション、複数サイトからのデータの統合などのシナリオが一般的です。 スナップショット レプリケーションは、トランザクション レプリケーションとマージ レプリケーションに初期データセットを提供するために使用されます。データの完全な更新が必要な場合にも使用できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、この 3 種類のレプリケーションにより、企業全体のデータの同期のための強力かつ柔軟なシステムが提供されます。 SQLCE 3.5 および SQLCE 4.0 に対するレプリケーションは [!INCLUDE[win8srv](../../includes/win8srv-md.md)] と [!INCLUDE[win8](../../includes/win8-md.md)]の両方でサポートされます。  


## <a name="whats-new"></a>新機能 
- SQL Server 2017 では、SQL Server のレプリケーションに重要な新機能は加えられていません。 
- SQL Server 2016 では、SQL Server のレプリケーションに重要な新機能は加えられていません。 

下位互換性の情報については、「[レプリケーションの旧バージョンとの互換性](replication-backward-compatibility.md)」を参照してください。 


 ## <a name="replication-security"></a>レプリケーションのセキュリティ
  
-   [レプリケーションのセキュリティ設定の表示および変更](security/view-and-modify-replication-security-settings.md)  
-   [パブリケーション アクセス リストのログインの管理](security/manage-logins-in-the-publication-access-list.md)  
  
## <a name="publishing-and-distribution"></a>パブリッシングおよびディストリビューション  
  
-   [パブリッシングおよびディストリビューションの構成](configure-publishing-and-distribution.md)   
-   [パブリケーション プロパティの表示および変更](publish/view-and-modify-publication-properties.md)   
-   [パブリッシングおよびディストリビューションの無効化](disable-publishing-and-distribution.md)  
  
## <a name="publications-and-articles"></a>パブリケーションおよびアーティクル 
  
-   [パブリケーションの作成](publish/create-a-publication.md)    
-   [アーティクルの定義](publish/define-an-article.md)   
-   [パブリケーション プロパティの表示および変更](publish/view-and-modify-publication-properties.md)   
-   [アーティクルのプロパティの表示と変更](publish/view-and-modify-article-properties.md)    
-   [パブリケーションの削除](publish/delete-a-publication.md)   
-   [アーティクルの削除](publish/delete-an-article.md)    
-   [Oracle データベースからのパブリケーションの作成](publish/create-a-publication-from-an-oracle-database.md)   
-   [サブスクリプションの有効期限の設定](publish/set-the-expiration-period-for-subscriptions.md)  
-   [スキーマ オプションの指定](publish/specify-schema-options.md)  
-   [スキーマ変更のレプリケート](publish/replicate-schema-changes.md)    
-   [ID 列の管理](publish/manage-identity-columns.md)   
-   [マージ パブリケーションの互換性レベルの設定](publish/set-the-compatibility-level-for-merge-publications.md)  
  
### <a name="snapshot-options"></a>スナップショット オプション  
  
-   [スナップショットのプロパティの構成](publish/configure-snapshot-properties-replication-transact-sql-programming.md)    
-   [FTP でのスナップショットの配信](publish/deliver-a-snapshot-through-ftp.md) 
  
### <a name="filter-data"></a>データのフィルター選択  
  
-   [列フィルターの定義および変更](publish/define-and-modify-a-column-filter.md)    
-   [静的行フィルターの定義および変更](publish/define-and-modify-a-static-row-filter.md)    
-   [マージ アーティクルのパラメーター化された行フィルターの定義および変更](publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)    
-   [パラメーター化された行フィルターの最適化](publish/optimize-parameterized-row-filters.md)    
-   [マージ アーティクル間の結合フィルターの定義および変更](publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
### <a name="transactional-replication-options"></a>トランザクション レプリケーション オプション  
  
-   [データの変更をトランザクション アーティクルに反映する方法の設定](publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)    
-   [トランザクション パブリケーションの更新可能なサブスクリプションの有効化](publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
### <a name="merge-replication-options"></a>マージ レプリケーション オプション  
  
-   [マージ テーブル アーティクル間に論理レコード リレーションシップを定義する](publish/define-a-logical-record-relationship-between-merge-table-articles.md)    
-   [マージ レプリケーションのプロパティの指定](merge/specify-merge-replication-properties.md)    
-   [マージ アーティクル競合回避モジュールの指定](publish/specify-a-merge-article-resolver.md)    

  
## <a name="manage-subscriptions"></a>サブスクリプションを管理する  
  
-   [Create a Pull Subscription](create-a-pull-subscription.md)    
-   [プル サブスクリプションのプロパティの表示または変更](view-and-modify-pull-subscription-properties.md)    
-   [プル サブスクリプションの削除](delete-a-pull-subscription.md)    
-   [プッシュ サブスクリプションの作成](create-a-push-subscription.md)   
-   [プッシュ サブスクリプションのプロパティの表示または変更](view-and-modify-push-subscription-properties.md)   
-   [プッシュ サブスクリプションの削除](delete-a-push-subscription.md)   
-   [同期スケジュールの指定](specify-synchronization-schedules.md)    
-   [トランザクション パブリケーションの更新可能なサブスクリプションの作成](publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
-   [SQL Server 以外のサブスクライバーのサブスクリプションの作成](create-a-subscription-for-a-non-sql-server-subscriber.md)  
  
## <a name="synchronize-subscriptions"></a>サブスクリプションの同期  
  
-   [初期スナップショットの作成および適用](create-and-apply-the-initial-snapshot.md)   
-   [パラメーター化されたフィルターを使用したパブリケーションのスナップショットの作成](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)    
-   [トランザクション サブスクリプションのバックアップからの初期化 (レプリケーション Transact-SQL プログラミング)](initialize-a-transactional-subscription-from-a-backup.md)    
-   [手動によるサブスクリプションの初期化](initialize-a-subscription-manually.md)    
-   [プル サブスクリプションの同期](synchronize-a-pull-subscription.md)    
-   [プッシュ サブスクリプションの同期](synchronize-a-push-subscription.md)   
-   [サブスクリプションの再初期化](reinitialize-a-subscription.md)    
-   [同期中のスクリプトの実行 (レプリケーション Transact-SQL プログラミング)](execute-scripts-during-synchronization-replication-transact-sql-programming.md)    
-   [マージ アーティクルのビジネス ロジック ハンドラーの実装](implement-a-business-logic-handler-for-a-merge-article.md)  
-   [ビジネス ロジック ハンドラーのデバッグ&#40;レプリケーション プログラミング&#41;](debug-a-business-logic-handler-replication-programming.md)    
-   [同期中にトリガーと制約の動作を制御する &#40;レプリケーション Transact-SQL プログラミング&#41;](control-behavior-of-triggers-and-constraints-in-synchronization.md)    
-   [マージ アーティクルのカスタム競合回避モジュールの実装](implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="administration"></a>管理 
  
-   [レプリケーション エージェント プロファイルの操作](agents/work-with-replication-agent-profiles.md)   
-   [サブスクライバーでのデータの検証](validate-data-at-the-subscriber.md)    
-   [パラメーター化されたフィルターによるマージ パブリケーションのパーティションの管理](publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)    
-   [マージ レプリケーション内のテーブルにデータを一括読み込みする (レプリケーション Transact-SQL プログラミング)](bulk-load-data-into-tables-in-a-merge-publication.md)    
-   [マージ メタデータのクリーンアップ (レプリケーション Transact-SQL プログラミング)](administration/clean-up-merge-metadata-replication-transact-sql-programming.md)    
-   [マージ アーティクルのダミー更新の実行 (レプリケーション Transact-SQL プログラミング)](administration/perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming.md)    
-   [レプリケートされたコマンドなどディストリビューション データベースに格納されている情報を表示する (レプリケーション Transact-SQL プログラミング)](monitor/view-replicated-commands-and-information-in-distribution-database.md)    
-   [トランザクション レプリケーションの連携バックアップの有効化 (レプリケーション Transact-SQL プログラミング)](administration/enable-coordinated-backups-for-transactional-replication.md)   
-   [ピア ツー ピア トポロジの管理 (レプリケーション Transact-SQL プログラミング)](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)    
-   [レプリケーション トポロジの停止 (レプリケーション Transact-SQL プログラミング)](administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)    
-   [Oracle パブリッシャー用のトランザクション セット ジョブの構成 (レプリケーション Transact-SQL プログラミング)](administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
-   [レプリケーション スクリプトのアップグレード (レプリケーション Transact-SQL プログラミング)](administration/upgrade-replication-scripts-replication-transact-sql-programming.md)  
  
## <a name="monitor"></a>モニター
  
-   [管理者以外のユーザーがレプリケーション モニターを使用できるようにする](monitor/allow-non-administrators-to-use-replication-monitor.md)    
-   [プログラムによるレプリケーションの監視](monitor/programmatically-monitor-replication.md)    
-   [レプリケートされたコマンドなどディストリビューション データベースに格納されている情報を表示する (レプリケーション Transact-SQL プログラミング)](monitor/view-replicated-commands-and-information-in-distribution-database.md)    
-   [マージ パブリケーションの競合情報の表示 (レプリケーション Transact-SQL プログラミング)](view-conflict-information-for-merge-publications.md) 
-   [トランザクション レプリケーションの待機時間の計測および接続の検証](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
