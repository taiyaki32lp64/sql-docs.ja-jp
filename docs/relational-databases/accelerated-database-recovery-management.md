---
title: 高速データベース復旧 | Microsoft Docs
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- accelerated database recovery [SQL Server], recovery-only
- database recovery [SQL Server]
author: mashamsft
ms.author: mathoma
ms.reviewer: kfarlee
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8fea43ea41bc3e65fa0a6b36c7557322431e95fd
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245260"
---
# <a name="manage-accelerated-database-recovery"></a>高速データベース復旧を管理する

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

## <a name="enabling-and-controlling-adr"></a>ADR の有効化と制御

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] では ADR は既定でオフになっており、DDL 構文を使用して制御できます。
```sql
ALTER DATABASE [DB] SET ACCELERATED_DATABASE_RECOVERY = {ON | OFF}
[(PERSISTENT_VERSION_STORE_FILEGROUP = { filegroup name }) ];

```

この構文を使用してこの機能のオン/オフを制御し、*永続的なバージョン ストア* (PVS) データに特定のファイルグループを指定します。 ファイル グループが指定されていない場合、PVS はプライマリ ファイル グループに格納されます。

## <a name="managing-the-persistent-version-store-filegroup"></a>永続的なバージョン ストア ファイルグループの管理
ADR 機能は変更をバージョン管理することを基盤としており、さまざまなバージョンのデータ要素が PVS に保管されます。
PVS の場所の見つけ方と PVS に含まれるデータ サイズの管理方法には注意点があります。

### <a name="to-enable-adr-without-specifying-a-filegroup"></a>ファイルグループを指定せずに ADR を有効にするには

```sql
ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = ON;
GO
```

この場合、PVS ファイルグループが指定されていないとき、`PRIMARY` ファイルグループで PVS データが保持されます。

### <a name="to-enable-adr-and-specify-that-the-pvs-should-be-stored-in-the-versionstorefg-filegroup"></a>ADR を有効にし、PVS を [VersionStoreFG] ファイルグループに格納するように指定するには

このスクリプトを実行する前に、ファイルグループを作成します。

```sql
ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = ON
(PERSISTENT_VERSION_STORE_FILEGROUP = [VersionStoreFG])
```

### <a name="to-disable-the-adr-feature"></a>ADR 機能を無効にするには

```sql
ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = OFF;
GO
```

ADR 機能が無効になった後でも、論理的に元に戻すときに必要となる永続的なバージョン ストアにバージョンが格納されます。

### <a name="change-the-location-of-the-pvs-to-a-different-filegroup"></a>PVS の場所を別のファイルグループに変更する

さまざまな理由から、PVS の場所を別のファイルグループに移さなければならないことがあります。 たとえば、PVS でもっとたくさんの領域が必要になったり、高速のストレージが必要になったりすることがあります。

PVS の場所の変更は、3 つの手順からなるプロセスです。

1. ADR 機能をオフにします。

   ```sql
   ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = OFF;
   GO
   ```

2. PVS に格納されているすべてのバージョンを解放できるようになるまで待ちます。

   ADR をオンにし、永続的なバージョン ストアに新しい場所を指定するには、まず、PVS の前の場所からバージョン情報がすべて削除されていることを確認する必要があります。 その消去を強制するには、次のコマンドを実行します。

   ```sql
   EXEC sys.sp_persistent_version_cleanup [database name]
   ```

   `sys.sp_persistent_version_cleanup` ストアド プロシージャは同期型です。つまり、現行の PVS からすべてのバージョン情報が消去されるまで完了となりません。  完了したら、DMV `sys.dm_persistent_version_store_stats` を問い合わせ、`persistent_version_store_size_kb` の値を調べることでバージョン情報が確かに削除されていることを確認できます。

   ```sql
   SELECT DB_Name(database_id), persistent_version_store_size_kb 
   FROM sys.dm_tran_persistent_version_store_stats where database_id = [MyDatabaseID]
   ```

   persistent_version_store_size_kb の値が 0 のとき、ADR 機能を再度有効にし、PVS を新しいファイルグループに置くように構成できます。

1. PVS の新しい場所を指定して ADR をオンにする

   ```sql
   ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = ON
   (PERSISTENT_VERSION_STORE_FILEGROUP = [VersionStoreFG])
   ```

## <a name="troubleshooting"></a>トラブルシューティング

`sys.dm_tran_persistent_version_store_stats` を問い合わせ、PVS のサイズを確認します。

`% of DB` のサイズを確認します。 また、一般的なサイズとの違いにもご注意ください。

PVS は、ベースラインより大幅に大きいか、データベース サイズの 50% に近くなっている場合に大きいと見なされます。 

1. `oldest_active_transaction_id` を取得し、トランザクション ID に基づいて `sys.dm_tran_database_transactions` を問い合わせることでこのトランザクションが本当に長時間アクティブになっているのかを確認します。

   アクティブなトランザクションがあると、PVS を消去できません。

1. データベースが可用性グループに含まれる場合、`secondary_low_water_mark` を確認してください。 これは `sys.dm_hadr_database_replica_states` によって報告される `low_water_mark_for_ghosts` と同じです。 `sys.dm_hadr_database_replica_states` を問い合わせ、いずれかのレプリカでこの値が隠されていないか確認します。これも PVS の消去を妨げるためです。
1. `min_transaction_timestamp` (あるいは、オンライン PVS の消去が妨げられている場合は `online_index_min_transaction_timestamp`) を確認し、それに基づいて列 `transaction_sequence_num` の `sys.dm_tran_active_snapshot_database_transactions` を確認し、古いスナップショット トランザクションが PVS の消去を妨げているセッションを見つけます。
1. 上記のいずれも該当しない場合、中止となったトランザクションによって消去が妨げられていることになります。 `aborted_version_cleaner_last_start_time` と `aborted_version_cleaner_last_end_time` を確認し、中止となったトランザクションの消去が完了しているかを確認します。 中止となったトランザクションの消去が完了した後は、`oldest_aborted_transaction_id` の値が上位に移動するはずです。
1. 中止となったトランザクションが最近、正常に完了しなかった場合、エラー ログを確認し、`VersionCleaner` の問題を報告しているメッセージがないか確認します。
