---
title: 可用性グループの監視とトラブルシューティングのガイド
description: Always On 可用性グループのいくつかの一般的な問題の監視とトラブルシューティング作業を開始するために役立つコンテンツのインデックス。
ms.custom: seo-lt-2019
ms.date: 05/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 8d6d9954-ff6b-4e58-882e-eff0174f0d07
author: rothja
ms.author: jroth
ms.openlocfilehash: fa4b3ae0ef918b0d7706a7f4e47eceb50d380c0b
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822048"
---
# <a name="monitor-and-troubleshoot-availability-groups"></a>可用性グループの監視とトラブルシューティング
 このガイドは、Always On 可用性グループの監視と可用性グループのいくつかの一般的な問題のトラブルシューティング作業を開始するために役立ちます。 オリジナルのコンテンツに加えて、他の場所で公開されている役に立つ情報のランディング ページを提供します。 このガイドでは、可用性グループの大きな領域で発生する可能性があるすべての問題を完全に説明することはできませんが、根本原因の分析と問題の解決に関して正しい方向を示すことができます。 
 
 可用性グループは、統合テクノロジーであるため、発生する多くの問題は、データベース システムの他の問題の兆候である可能性があります。 いくつかの問題は、中断された可用性データベースなど、可用性グループ内の設定が原因です。 その他の問題には、SQL Server の設定、データベース ファイルの配置、可用性に関連しない体系的なパフォーマンスの問題など、SQL Server の他の側面に関する問題が含まれます。 他の問題は、ネットワーク I/O、TCP/IP、Active Directory、Windows Server フェールオーバー クラスタリング (WSFC) の問題など、SQL Server の外部にも存在する可能性があります。 多くの場合、可用性グループ、レプリカ、またはデータベースで発生する問題の根本原因を特定するには、複数のテクノロジーをトラブルシューティングする必要があります。  
  
  
##  <a name="BKMK_SCENARIOS"></a> トラブルシューティングのシナリオ  
 次の表には、可用性グループの一般的なトラブルシューティング シナリオへのリンクが含まれています。 これらは、構成、クライアント接続、フェールオーバー、パフォーマンスなどのシナリオの種類によって分類されています。  
  
|シナリオ|シナリオの種類|[説明]|  
|--------------|-------------------|-----------------|  
|[AlwaysOn 可用性グループの構成のトラブルシューティング &#40;SQL Server&#41;](troubleshoot-always-on-availability-groups-configuration-sql-server.md)|構成|可用性グループのサーバー インスタンスの構成に関する一般的な問題のトラブルシューティングに役立つ情報を提供します。 構成に関する一般的な問題には、可用性グループが無効になっている、アカウントが適切に構成されていない、データベース ミラーリング エンドポイントが存在しない、エンドポイントにアクセスできない (SQL Server エラー 1418)、ネットワーク アクセスが存在しない、データベース参加コマンドが失敗する (SQL Server エラー 35250) などがあります。|  
|[失敗したファイルの追加操作のトラブルシューティング &#40;AlwaysOn 可用性グループ&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)|構成|ファイルの追加操作によってセカンダリ データベースが中断され、NOT SYNCHRONIZING 状態になっています。|  
|[マルチ サブネット環境で可用性グループ リスナーに接続できない](https://support.microsoft.com/kb/2792139/en-us)|クライアント接続|可用性グループ リスナーを構成した後で、リスナーへの ping が失敗するか、アプリケーションから接続できません。|  
|[失敗した自動フェールオーバーのトラブルシューティング](https://support.microsoft.com/kb/2833707)|[フェールオーバー]|自動フェールオーバーが正常に完了しませんでした。|  
|[トラブルシューティング:可用性グループ接続の超過 RTO](troubleshoot-availability-group-exceeded-rto.md)|パフォーマンス|データ損失のない自動フェールオーバーまたは計画的な手動フェールオーバーの後で、フェールオーバー時間が RTO を超過します。 または、同期コミット セカンダリ レプリカのフェールオーバー時間を推定したとき (自動フェールオーバー パートナーなど)、RTO を超過していることが判明します。|  
|[トラブルシューティング:可用性グループ接続の超過 RPO](troubleshoot-availability-group-exceeded-rpo.md)|パフォーマンス|強制的な手動フェールオーバーを実行した後で、データ損失が RPO より大きくなります。 または、非同期コミット セカンダリ レプリカのデータ損失の可能性を計算したとき、計算結果が RPO を超過していることが判明します。|  
|[トラブルシューティング:プライマリ上の変更がセカンダリ レプリカに反映されない](troubleshoot-primary-changes-not-reflected-on-secondary.md)|パフォーマンス|クライアント アプリケーションは、プライマリ レプリカの更新を正常に完了しますが、セカンダリ レプリカのクエリを実行すると、変更が反映されていないことが示されます。|  
|[トラブルシューティング:Always On 可用性グループでの長い HADR_SYNC_COMMIT 待機の種類](https://blogs.msdn.microsoft.com/sql_server_team/troubleshooting-high-hadr_sync_commit-wait-type-with-always-on-availability-groups/)|パフォーマンス|HADR_SYNC_COMMIT が異常に長い場合は、データの移動フローまたはセカンダリ レプリカのログの書き込みにパフォーマンスの問題があります。|  

##  <a name="BKMK_TOOLS"></a> トラブルシューティングに役立つツール  
 可用性グループを構成または実行するときには、さまざまなツールでさまざまな種類の問題を診断できます。 次の表では、ツールに関する役立つ情報のリンクを提供します。  
  
|ツール|[説明]|  
|----------|-----------------|  
|[AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)|使いやすいインターフェイスで可用性グループの正常性の概要を報告します。|  
|[Always On ポリシー](always-on-policies.md)|AlwaysOn ダッシュボードの使用|  
|[SQL Server エラー ログ&#40;Always On 可用性グループ&#41;](sql-server-error-log-always-on-availability-groups.md)|可用性グループ、レプリカ、データベースのログ状態遷移イベント、他の Always On コンポーネントのステータス、Always On エラー|  
|[CLUSTER.LOG &#40;Always On 可用性グループ&#41;](cluster-log-always-on-availability-groups.md)|可用性グループ リソースの状態遷移を含むログ クラスター イベント、および SQL Server リソース DLL からのイベントとエラー。|  
|[Always On 正常性診断ログ](always-on-health-diagnostics-log.md)|[sp_server_diagnostics &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) によって WSFC クラスター (SQL Server リソース DLL) に報告された SQL Server の正常性診断をログに記録します。|  
|[動的管理ビューおよびシステム カタログ ビュー&#40;Always On 可用性グループ&#41;](dynamic-management-views-and-system-catalog-views-always-on-availability-groups.md)|構成、正常性状態、パフォーマンス メトリックなどの可用性グループに関する情報を報告します。|  
|[Always On 拡張イベント](always-on-extended-events.md)|可用性グループの詳細な診断をおよび役に立つ根本原因の分析を提供します。|  
|[Always On の待機の種類](always-on-wait-types.md)|可用性グループに固有の待機の統計情報および役に立つパフォーマンス調整を提供します。|  
|Always On パフォーマンス カウンター|可用性グループのアクティビティの監視は、システム モニターに反映され、パフォーマンス調整に役立ちます。 詳細については、「[SQL Server, availability replica](~/relational-databases/performance-monitor/sql-server-availability-replica.md)」(SQL Server、可用性レプリカ) および「[SQL Server, database replica](~/relational-databases/performance-monitor/sql-server-database-replica.md)」(SQL Server、データベース レプリカ) を参照してください。|  
|[Always On リング バッファー](always-on-ring-buffers.md)|内部診断用に SQL Server システム内のアラートを記録します。可用性グループに関連する問題のデバッグに使用できます。|  
  
##  <a name="BKMK_MONITOR"></a> 可用性グループの監視  
 可用性グループのトラブルシューティングに最適なタイミングは、自動または手動に関係なく、問題のためにフェールオーバーが必要になる前です。 これは、可用性グループのパフォーマンス メトリックを監視し、可用性レプリカが、サービス レベル アグリーメント (SLA) の境界の外部で実行されているときにアラートを送信することで実行できます。 たとえば、同期セカンダリ レプリカのパフォーマンスの問題のために推定フェールオーバー時間が増加する場合は、自動フェールオーバーが発生するまで待ちたくありません。さらにフェールオーバー時間が回復時刻の目標を超えていることを確認できます。  
  
 可用性グループは、高可用性およびディザスター リカバリー ソリューションなので、監視する最も重要なパフォーマンス メトリックは、回復時刻の目標 (RTO) に影響する推定フェールオーバー時間と、回復ポイントの目標 (RPO) に影響する災害時のデータ損失の可能性です。 SQL Server が公開するデータからこれらのメトリックをいつでも収集できるので、実際の障害イベントが発生する前に、システムの高可用性ディザスター リカバリー (HADR) 機能の問題のアラートを知ることができます。 したがって、可用性グループのデータの同期プロセスを詳しく理解し、それに応じてメトリックを収集することが重要です。  
  
 次の表には、可用性グループのソリューションの正常性を監視するのに役立つトピックへのリンクがあります。  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[Always On 可用性グループのパフォーマンスを監視する](monitor-performance-for-always-on-availability-groups.md)|可用性グループのデータ同期プロセス、フロー制御ゲート、可用性グループを監視するときに役立つメトリックについて説明し、RTO および RPO のメトリックを収集する方法についても説明します。|  
|[可用性グループの監視 &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)|可用性グループを監視するためのツールについて説明します。|  
|[Always On の正常性モデル: パート 1:正常性モデルのアーキテクチャ](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/09/overview-of-the-alwayson-manageability-health-model.aspx)|Always On 正常性モデルの概要を示します。|  
|[Always On の正常性モデル: パート 2:正常性モデルの拡張](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)|追加情報を表示するように Always On 正常性モデルと Always On ダッシュボードをカスタマイズする方法を示します。|  
|[PowerShell を使用した Always On 正常性状態の監視: パート 1:基本的なコマンドレットの概要](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-1.aspx)|可用性グループの正常性を監視するために使用できる PowerShell コマンドレットの基本的な概要を説明します。|  
|[PowerShell を使用した Always On 正常性状態の監視: パート 2:高度なコマンドレットの使用方法](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-2.aspx)|可用性グループの正常性を監視するための Always On PowerShell コマンドレットの高度な使用方法を説明します。|  
|[PowerShell を使用した Always On 正常性状態の監視: パート 3:シンプルな監視アプリケーション](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/monitoring-alwayson-health-with-powershell-part-3.aspx)|アプリケーションで可用性グループを自動的に監視する方法を示します。|  
|[PowerShell を使用した Always On 正常性状態の監視: パート 4:SQL Server エージェントとの統合](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/the-always-on-health-model-part-4.aspx)|SQL Server エージェントと可用性グループの監視を統合し、問題が発生したときの適切なユーザーへの通知を構成する方法について説明します。|  

## <a name="next-steps"></a>次のステップ  
 [SQL Server AlwaysOn チーム ブログ](https://blogs.msdn.com/b/sqlalwayson/)   
 [CSS SQL Server エンジニアのブログ](https://blogs.msdn.com/b/psssql/)  
  
  
