---
title: インメモリ OLTP に対してサポートされていない SQL Server の機能 | Microsoft Docs
ms.custom: ''
ms.date: 05/29/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c39f03a7-e223-4fd7-bd30-142e28f51654
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 720b10e5f4cd7c7ba5676f9dddc2f64e632d64cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912131"
---
# <a name="unsupported-sql-server-features-for-in-memory-oltp"></a>インメモリ OLTP に対してサポートされていない SQL Server の機能
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能で、メモリ最適化オブジェクトと共に使用できないものについて説明します。  
  
## <a name="includessnoversionincludesssnoversion-mdmd-features-not-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インメモリ OLTP に対してサポートされない機能  

次に示す [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能は、(メモリ最適化データ ファイル グループを含む) メモリ最適化オブジェクトを持つデータベースでサポートされません。  

  
|サポートされない機能|機能の説明|  
|-------------------------|-------------------------|  
|メモリ最適化テーブルに対するデータ圧縮。|データ圧縮機能を使用することにより、データベース内のデータを圧縮したり、データベースのサイズを小さくすることができます。 詳細については、「 [Data Compression](../../relational-databases/data-compression/data-compression.md)」を参照してください。|  
|メモリ最適化テーブルと HASH インデックスのパーティション分割、および非クラスター化インデックス。|パーティション テーブルとパーティション インデックスのデータは、データベース内の複数のファイル グループに分散できるように、複数の単位に分割されます。 詳細については、「 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)」を参照してください。|  
| レプリケーション | サブスクライバー上でのメモリ最適化されたテーブルに対するトランザクション レプリケーションを除き、他のレプリケーション構成は、メモリ最適化されたテーブルを参照するテーブルまたはビューと互換性がありません。<br /><br />メモリ最適化ファイル グループがある場合、sync_mode='database snapshot' を使用したレプリケーションはサポートされません。<br /><br />詳細については、「[メモリ最適化テーブル サブスクライバーへのレプリケーション](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)」を参照してください。|
|ミラーリング|データベース ミラーリングは、MEMORY_OPTIMIZED_DATA ファイル グループのデータベースではサポートされていません。 ミラーリングの詳細については、「[データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)」を参照してください。|  
|ログの再構築|ログの再構築は、MEMORY_OPTIMIZED_DATA ファイル グループのデータベースでは、アタッチと ALTER DATABASE のいずれによるものでもサポートされていません。|  
|Linked Server|メモリ最適化テーブルと同じクエリまたはトランザクションで、リンク サーバーにアクセスすることはできません。 詳しくは、「 [リンク サーバー &#40;データベース エンジン&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)」を参照してください。|  
|一括ログ記録|データベースの復旧モデルにかかわらず、持続性のあるメモリ最適化テーブル上のすべての操作は、常に完全にログに記録されます。|  
|最小ログ記録|最小ログ記録は、メモリ最適化テーブルではサポートされていません。 最小ログ記録の詳細については、「[トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)」および「[一括インポートで最小ログ記録を行うための前提条件](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)」を参照してください。|  
|変更の追跡|変更の追跡は、インメモリ OLTP オブジェクトを含むデータベースで有効にすることができません。 |
| DDL トリガー | インメモリ OLTP テーブルまたはネイティブ コンパイル モジュールでは、データベースレベルとサーバーレベルの DDL トリガーはどちらもサポートされません。 |  
| 変更データ キャプチャ (CDC) | メモリ最適化テーブルが含まれるデータベースで CDC を有効にする、SQL Server 2017 CU15 以上のサポート。 これはデータベースとデータベース内のオンディスク テーブルにのみ該当します。 以前のバージョンの SQL Server では、CDC の内部で DROP TABLE に対して DDL トリガーが使用されているため、メモリ最適化テーブルが含まれるデータベースでは CDC を使用できません。 |  
| ファイバー モード | ファイバー モードは、メモリ最適化テーブルではサポートされていません。<br /><br />ファイバー モードがアクティブな場合は、メモリ最適化ファイル グループが含まれたデータベースを作成することも、既存データベースへのメモリ最適化ファイル グループの追加を行うこともできません。<br /><br />メモリ最適化ファイル グループが含まれたデータベースを使用している場合に、ファイバー モードを有効にすることはできます。 ただし、ファイバー モードを有効にするには、サーバーを再起動する必要があります。 このような場合、メモリ最適化ファイル グループを含むデータベースは回復できません。 メモリ最適化ファイル グループを含むデータベースのファイバー モードでの使用が無効になっていることを示すエラー メッセージが表示されます。<br /><br />ファイバー モードがアクティブであれば、メモリ最適化ファイル グループが含まれたデータベースのアタッチおよび復元は失敗します。 また、データベースが SUSPECT としてマークされます。<br /><br />詳細については、「 [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)」を参照してください。 |  
|Service Broker の制限事項|ネイティブ コンパイル ストアド プロシージャからキューにアクセスできません。<br /><br /> メモリ最適化テーブルにアクセスするトランザクションでリモート データベースのキューにアクセスできません。|  
|サブスクライバーでのレプリケーション|サブスクライバー上でのメモリ最適化テーブルに対するトランザクション レプリケーションはサポートされていますが、いくつかの制限があります。 詳細については、「 [メモリ最適化テーブル サブスクライバーへのレプリケーション](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)」を参照してください。|  


#### <a name="cross-database-queries-and-transcations"></a>データベースにまたがるクエリとトランザクション

一部の例外を除き、複数データベースにまたがるトランザクションはサポートされません。 次の表では、サポートされるケースと、対応する制限について説明します (「 [複数データベースにまたがるクエリ](../../relational-databases/in-memory-oltp/cross-database-queries.md)」も参照してください。)  


|データベース|Allowed|[説明]|  
|---------------|-------------|-----------------|  
| ユーザー データベース、**model**、および **msdb**。 | いいえ | ほとんどの場合、複数のデータベースにまたがるクエリおよびトランザクションは*サポートされません*。<br /><br />クエリがメモリ最適化テーブルまたはネイティブにコンパイルされたストアド プロシージャを使用している場合、そのクエリは他のデータベースにアクセスできません。 この制限は、クエリだけでなくトランザクションにも適用されます。<br /><br />例外は、システム データベースである **tempdb** と **master** です。 ここで、**master** データベースは読み取り専用アクセスで利用できます。 |
| **Resource** データベース、**tempdb** | はい | インメモリ OLTP オブジェクトを扱うトランザクションでは、**Resource** および **tempdb** システム データベースを追加の制限なく使用できます。


## <a name="scenarios-not-supported"></a>サポートされていないシナリオ  
  
- CLR ストアド プロシージャ内からのコンテキスト接続を使用したメモリ最適化テーブルへのアクセス。  
  
- メモリ最適化テーブルにアクセスするクエリでのキーセットと動的カーソル。 これらのカーソルは静的および読み取り専用に降格されます。  
  
- **MERGE INTO** _target_ の使用は、*target* がメモリ最適化テーブルである場合にはサポートされません。
    - **MERGE USING** _source_ は、メモリ最適化テーブルでサポートされます。  
  
- ROWVERSION (TIMESTAMP) データ型はサポートされていません。 詳細については、「[FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)」を参照してください。
  
- 自動終了は、MEMORY_OPTIMIZED_DATA ファイル グループのあるデータベースではサポートされていません。  
  
- データベース スナップショットは、MEMORY_OPTIMIZED_DATA ファイル グループのあるデータベースではサポートされていません。  
  
- インメモリ OLTP オブジェクトの CREATE/ALTER/DROP などのトランザクション DDL は、ユーザー トランザクション内ではサポートされていません。  
  
- イベント通知。  
  
- ポリシー ベースの管理 (PBM)。
    - PBM の "回避" モードと "ログのみ" モードはサポートされません。 サーバーにこのようなポリシーが存在すると、インメモリ OLTP の DDL が正常に実行されないことがあります。 "要求時" モードと "スケジュールで実行" モードはサポートされます。  

- データベースの包含 ([包含データベース](../../relational-databases/databases/contained-databases.md)) は、インメモリ OLTP ではサポートされていません。
    - Contained database authentication がサポートされます。 ただし、すべてのインメモリ OLTP オブジェクトは、動的管理ビュー (DMV) **dm_db_uncontained_entities** で "breaking containment" とマークされています。

  
## <a name="see-also"></a>参照  

- [SQL Server によるインメモリ OLTP のサポート](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)
