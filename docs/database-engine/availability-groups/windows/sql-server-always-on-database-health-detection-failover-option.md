---
title: データベース レベルの正常性検出
description: SQL Server の Always On 可用性グループで使用できるデータベース レベルの正常性検出機能について説明します。
ms.custom: seo-lt-2019
ms.date: 01/19/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- AlwaysOn
- DB_FAILOVER
- Always On
- High Availability
- SQL Server
ms.assetid: d74afd28-25c3-48a1-bc3f-e353bee615c2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6fa77fa3ac4733d9672b5bc72523d72abe640fc8
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75251262"
---
# <a name="availability-group-database-level-health-detection-failover-option"></a>可用性グループのデータベース レベルの正常性検出フェールオーバー オプション
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
SQL Server 2016 以降、Always On 可用性グループを構成するときに、データベース レベルの正常性検出 (DB_FAILOVER) オプションを使用できます。 何らかの問題が発生し、データベースがオンライン状態でなくなると、このデータベース レベルの正常性検出によって検知され、可用性グループの自動フェールオーバーがトリガーされます。

可用性グループのデータベース レベルの正常性検出は、可用性グループ全体に対して有効になるため、データベース レベルの正常性検出では可用性グループ内のすべてのデータベースが監視されます。 可用性グループ内の特定のデータベースを選択して有効にすることはできません。

## <a name="benefits-of-database-level-health-detection-option"></a>データベース レベルの正常性検出オプションの利点
---
可用性グループのデータベース レベルの正常性検出オプションは、データベースの高可用性を保証するオプションとして広く推奨されます。 すべての可用性グループに対して、このオプションを有効にすることを検討してください。 アプリケーションでいくつかのデータベースについて高い可用性が必要な場合は、そのデータベースを 1 つの可用性グループにまとめて、データベースの正常性オプションを有効にします。

たとえば、データベース レベルの正常性検出オプションが有効になっている場合、SQL Server が、いずれかのデータベースのトランザクション ログ ファイルに書き込むことができないと、データベースは障害状態に変わり、可用性グループはすぐにフェールオーバーします。データベースが再度オンラインになった時点で、アプリケーションは再接続し、最小限の中断で動作し続けることができます。

### <a name="enabling-database-level-health-detection"></a>データベース レベルの正常性検出の有効化

データベースの正常性オプションは一般的に推奨されるオプションですが、以前のバージョンにおける既定の設定との下位互換性を維持するために、**既定でオフ**になっています。

データベース レベルの正常性検出の設定を有効にする方法はいくつかあります。

1. SQL Server Management Studio で、SQL Server データベース エンジンに接続します。 オブジェクト エクスプ ローラー ウィンドウを使用して、AlwaysOn 高可用性ノードを右クリックし、**新しい可用性グループ ウィザード**を実行します。 [名前の指定] ページで **[データベース レベルの正常性検出]** チェック ボックスをオンします。 続けて、ウィザードの残りのページに情報を入力します。

   ![AlwaysOn/データベース正常性のチェック ボックスをオンにする](../../../database-engine/availability-groups/windows/media/always-on-enable-database-health-checkbox.png)

2. SQL Server Management Studio で既存の可用性グループの**プロパティ**を表示します。 SQL Server に接続します。 オブジェクト エクスプローラー ウィンドウを使用して、AlwaysOn 高可用性ノードを展開します。 可用性グループを展開します。 可用性グループを右クリックし、[プロパティ] を選択します。 **[データベース レベルの正常性検出]** オプションをオンにして、[OK] をクリックするか、[スクリプト] をクリックして変更します。

   ![AlwaysOn/AG プロパティ/データベース レベルの正常性検出](../../../database-engine/availability-groups/windows/media/always-on-ag-properties-database-level-health-detection.png)


3. **CREATE AVAILABILITY GROUP** の Transact-SQL 構文。 DB_FAILOVER パラメーターには、ON または OFF を指定できます。

   ```sql
   CREATE AVAILABILITY GROUP [Contoso-ag]
   WITH (DB_FAILOVER=ON)
   FOR DATABASE [AutoHa-Sample]
   REPLICA ON
       N'SQLSERVER-0' WITH (ENDPOINT_URL = N'TCP://SQLSERVER-0.DOMAIN.COM:5022',
         FAILOVER_MODE = AUTOMATIC, AVAILABILITY_MODE = SYNCHRONOUS_COMMIT),
       N'SQLSERVER-1' WITH (ENDPOINT_URL = N'TCP://SQLSERVER-1.DOMAIN.COM:5022',
        FAILOVER_MODE = AUTOMATIC, AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
    ```

4. **ALTER AVAILABILITY GROUP** の Transact-SQL 構文。 DB_FAILOVER パラメーターには、ON または OFF を指定できます。

   ```sql
   ALTER AVAILABILITY GROUP [Contoso-ag] SET (DB_FAILOVER = ON);

   ALTER AVAILABILITY GROUP [Contoso-ag] SET (DB_FAILOVER = OFF);
   ```

### <a name="caveats"></a>注意事項

現時点では、データベース レベルの正常性検出オプションを使用しても、SQL Server ではディスクの稼働時間が監視されない点に注意してください。SQL Server では、データベース ファイルの可用性は直接監視されません。 ディスク ドライブで障害が発生したり、利用できなくなったりしても、それだけで可用性グループが自動的にフェールオーバーされるとは限りません。

たとえば、アクティブなトランザクションがなく、物理書き込みも発生していないデータベースがアイドル状態のとき、そのデータベース ファイルのいくつかにアクセスできなくなると、SQL Server によるそのファイルの IO 読み取りまたは書き込みは行われず、データベースの状態もすぐには変更されない可能性があるため、フェールオーバーはトリガーされません。 後で、データベース チェックポイントが発生したとき、またはクエリ実行のために物理読み取りまたは書き込みが発生すると、SQL Server はファイルで問題が発生していることを検知し、データベースの状態を変更します。その後、データベースの正常性が変更されたため、データベース レベルの正常性検出が設定されている可用性グループがフェールオーバーします。

また、SQL Server データベース エンジンがクエリ実行のためにデータ ページを読み取る必要があるとき、そのデータ ページがバッファー プール メモリにキャッシュされていると、物理アクセスを伴うディスクの読み取りを行わなくても、そのクエリ要求に対処できます。 したがって、データ ファイルが存在しない、または利用できない場合、データベース正常性オプションが有効になっていても、データベースの状態はすぐには変更されないため、自動フェールオーバーがすぐにトリガーされることはありません。


## <a name="database-failover-is-separate-from-flexible-failover-policy"></a>データベースのフェールオーバーと柔軟なフェールオーバー ポリシーの分離
データベース レベルの正常性検出では、フェールオーバー ポリシーに対して SQL Server プロセスの正常性のしきい値が構成された、柔軟なフェールオーバー ポリシーが実装されています。 データベース レベルの正常性検出は DB_FAILOVER パラメーターを使用して構成されますが、可用性グループ オプション FAILURE_CONDITION_LEVEL はそれとは別のもので、SQL Server プロセスの正常性検出を構成します。 この 2 つのオプションは互いに独立しています。

## <a name="managing-and-monitoring-database-level-health-detection"></a>データベース レベルの正常性検出の管理と監視

### <a name="dynamic-management-views"></a>動的管理ビュー

システム DMV sys.availability_groups には、データベース レベルの正常性検出オプションがオフ (0) かオン (1) かを示す db_failover 列があります。

```sql
select name, db_failover from sys.availability_groups
```


dmv 出力の例:

|name  |  db_failover|
|---------|---------|
| Contoso-ag | 1  |

### <a name="errorlog"></a>ErrorLog
データベース レベルの正常性検出チェックが原因で、可用性グループがフェールオーバーした場合、SQL Server エラー ログ (または sp_readerrorlog のテキスト) にはエラー メッセージ 41653 が表示されます。

たとえば、次のエラー ログの抜粋は、ディスクで問題が発生したためにトランザクション ログの書き込みが失敗し、その後、AutoHa-Sample という名前のデータベースがシャットダウンして、データベース レベルの正常性検出がトリガーされ、可用性グループをフェールオーバーしたことを示しています。

>2016-04-25 12:20:21.08 spid1s      エラー:17053、重大度:16、状態: 1.
>
>2016-04-25 12:20:21.08 spid1s      SQLServerLogMgr::LogWriter:オペレーティング システム エラー 21 (デバイスの準備ができていません) が発生しました。
>2016-04-25 12:20:21.08 spid1s      ログ フラッシュ中の書き込みエラー。
>
>2016-04-25 12:20:21.08 spid79      エラー:9001、重大度:21、状態:4.
>
>2016-04-25 12:20:21.08 spid79      データベース 'AutoHa-Sample' のログは使用できません。 イベント ログで、関連するエラー メッセージを確認してください。 エラーがある場合は解決し、データベースを再起動してください。
>
>**2016-04-25 12:20:21.15 spid79      エラー:41653、重大度:21、状態:1。**
>
>**2016-04-25 12:20:21.15 spid79      データベース 'AutoHa-Sample' でエラー (エラーの種類:2 'DB_SHUTDOWN') が発生し、可用性グループ 'Contoso-ag' が失敗しました。発生したエラーの詳細については、SQL Server エラー ログを参照してください。この問題が解決しない場合は、システム管理者に問い合わせてください。**
>
>2016-04-25 12:20:21.17 spid79      データベース 'AutoHa-Sample' の状態情報 - 書き込まれた Lsn: '(34:664:1)'    コミット LSN: '(34:656:1)'    コミット時間:'Apr 25 2016 12:19PM'
>
>2016-04-25 12:20:21.19 spid15s     可用性レプリカ 'SQLServer-0' (レプリカ ID: {c4ad5ea4-8a99-41fa-893e-189154c24b49}) で、プライマリ データベース 'AutoHa-Sample' の、セカンダリ データベースとの Always On 可用性グループ接続が終了しました。 このメッセージは情報提供だけを目的としています。 ユーザーによる操作は不要です。
>
>2016-04-25 12:20:21.21 spid75      Always On:可用性グループ 'Contoso-ag' のローカル レプリカは、Windows Server フェールオーバー クラスタリング (WSFC) クラスターからの要求により、解決中のロールに遷移する準備をしています。 このメッセージは情報提供だけを目的としています。 ユーザーによる操作は不要です。
>
>2016-04-25 12:20:21.21 spid75      可用性グループ 'ag' のローカル可用性レプリカの状態が 'PRIMARY_NORMAL' から 'RESOLVING_NORMAL' に変わりました。  可用性グループがオフラインに移行しているため、状態が変わりました。  関連付けられている可用性グループが削除されたか、関連付けられている可用性グループをユーザーが Windows Server フェールオーバー クラスタ リング (WSFC) 管理コンソールでオフラインにしたか、可用性グループが別の SQL Server インスタンスにフェールオーバーしているため、レプリカがオフラインに移行しています。  詳細については、SQL Server エラー ログ、Windows Server フェールオーバー クラスタリング (WSFC) 管理コンソール、または WSFC ログをご覧ください。

### <a name="extended-event-sqlserveravailability_replica_database_fault_reporting"></a>拡張イベント sqlserver.availability_replica_database_fault_reporting

SQL Server 2016 以降、新しい拡張イベントが定義されました。このイベントは、データベース レベルの正常性検出によってトリガーされます。  イベントの名前は **sqlserver.availability_replica_database_fault_reporting** です。

この XEvent は、プライマリ レプリカでのみトリガーされます。 また、可用性グループでホストされているデータベースに対して、データベース レベルの正常性に関する問題が検出されたときにトリガーされます。

このイベントをキャプチャする XEvent セッションを作成する例を次に示します。 パスが指定されていないため、XEvent 出力ファイルは、SQL Server エラー ログの既定のパスに配置されます。 このスクリプトは、可用性グループのプライマリ レプリカで実行してください。

拡張イベント セッション スクリプトの例

```sql
CREATE EVENT SESSION [AlwaysOn_dbfault] ON SERVER
ADD EVENT sqlserver.availability_replica_database_fault_reporting
ADD TARGET package0.event_file(SET filename=N'dbfault.xel',max_file_size=(5),max_rollover_files=(4))
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,
    MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)
GO
ALTER EVENT SESSION AlwaysOn_dbfault ON SERVER STATE=START
GO
```

#### <a name="extended-event-output"></a>拡張イベントの出力
SQL Server Management Studio を使用して、プライマリ SQL Server に接続し、[管理] ノードを展開して、拡張イベントを展開します。 セッション (上記の例では AlwaysOn_dbfault という名前) を見つけてを展開し、出力ファイルを確認してください。 出力ファイルをクリックすると、新しいタブでイベント ファイルが開きます。

フィールドの説明:

|列のデータ | [説明]|
|---------|---------|
|availability_group_id |可用性グループの ID。|
|availability_group_name |可用性グループの名前です。|
|availability_replica_id |可用性レプリカの ID。|
|availability_replica_name |可用性レプリカの名前。|
|database_name |エラーをレポートしているデータベースの名前。|
|database_replica_id |可用性レプリカ データベースの ID。|
|failover_ready_replicas |同期されている自動フェールオーバー セカンダリ レプリカの数。|
|fault_type  | レポートされたエラー ID。 指定できる値  <br/> 0 - NONE <br/>1 - Unknown<br/>2 - Shutdown|
|is_critical | SQL Server 2016 の XEvent では、この値は常に true を返します。|


この出力例は、AutoHa-Sample2 という名前のデータベースで "fault_type 2 シャットダウン" が発生したため、SQLSERVER-1 という名前のレプリカの、可用性グループ Contoso-ag で、重大なイベントが発生したことを示しています。

|フィールド  | 値|
|---------|---------|
|availability_group_id | 24E6FE58-5EE8-4C4E-9746-491CFBB208C1|
|availability_group_name | Contoso-ag|
|availability_replica_id | 3EAE74D1-A22F-4D9F-8E9A-DEFF99B1F4D1|
|availability_replica_name | SQLSERVER-1|
|database_name | AutoHa-Sample2|
|database_replica_id | 39971379-8161-4607-82E7-098590E5AE00|
|failover_ready_replicas | 1|
|fault_type | 2|
|is_critical | True|


### <a name="related-references"></a>関連リファレンス

* [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)

* [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)

* [可用性グループの自動フェールオーバーのための柔軟なフェールオーバー ポリシー (SQL Server)](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md)

* [SQL Server データベースのデータとログ ドライブをテストするための AlwaysOn フェールオーバー ポリシーの強化](https://blogs.msdn.microsoft.com/alwaysonpro/2016/01/14/enhance-alwayson-failover-policy-to-test-sql-server-database-data-and-log-drives/)

* [拡張イベント](../../../relational-databases/extended-events/extended-events.md)



