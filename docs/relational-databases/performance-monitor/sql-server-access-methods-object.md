---
title: SQL Server の Access Methods オブジェクト | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Access Methods object
- SQLServer:Access Methods
ms.assetid: 27558585-e780-48bb-a042-30d664662ebc
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: ab394b7eed0a284b8ed74e5333b01f27283469ca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987363"
---
# <a name="sql-server-access-methods-object"></a>SQL Server の Access Methods オブジェクト
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **Access Methods** オブジェクトには、データベース内の論理データへのアクセス方法を監視するためのカウンターがあります。 ディスク上のデータベース ページへの物理アクセスは、 **Buffer Manager** カウンターを使用して監視します。 データベースに格納されているデータへのアクセス方法を監視すれば、インデックスの追加や変更、パーティションの追加や移動、ファイルまたはファイル グループの追加、インデックスのデフラグ、クエリの書き直しなど、どのような措置によってクエリ パフォーマンスが向上するかを判断する際に役立ちます。 **Access Methods** カウンターを使用して、データベース内のデータ、インデックス、および空き領域サイズを監視し、各サーバー インスタンスのデータ量と断片化状況を確認することもできます。 インデックスが過度に断片化されると、パフォーマンスの低下につながります。  
  
 データ量、断片化、および使用状況の詳細な情報を得るには、次の動的管理ビューを使用します。  
  
-   [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)  
  
-   [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)  
  
 ファイル、タスク、およびセッション レベルでの **tempdb** の使用領域については、次の動的管理ビューを使用します。  
  
-   [sys.dm_db_file_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
-   [sys.dm_db_task_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)  
  
-   [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
  
 次の表では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **Access Methods** カウンターについて説明します。  
  
|SQL Server の Access Methods カウンター|[説明]|  
|----------------------------------------|-----------------|  
|**AU cleanup batches/sec**|遅延および削除済みアロケーション ユニットをクリーンアップするバックグラウンド タスクによって正常に完了した 1 秒あたりのバッチの数。|  
|**AU cleanups/sec**|遅延および削除済みアロケーション ユニットをクリーンアップするバックグラウンド タスクによって正常に削除された 1 秒あたりのアロケーション ユニットの数。 各アロケーション ユニットの削除には複数のバッチが必要です。|  
|**By-reference Lob Create Count**|参照渡しで渡されたラージ オブジェクト (LOB) 値の数。 参照渡し LOB は、値で渡すコストを省くために特定の一括操作で使用されます。|  
|**By-reference Lob Use Count**|使用された参照渡し LOB 値の数。 参照渡し LOB は、値で渡すコストを省くために特定の一括操作で使用されます。|  
|**Count Lob Readahead**|先行読み取りが行われた LOB ページの数。|  
|**Count Pull In Row**|行外から行内に移動した列値の数。|  
|**Count Push Off Row**|行内から行外に移動した列値の数。|  
|**Deferred Dropped Aus**|遅延および削除済みアロケーション ユニットをクリーンアップするバックグラウンド タスクによって削除されるのを待っているアロケーション ユニットの数。|  
|**Deferred Dropped rowsets**|遅延および削除済み行セットをクリーンアップするバックグラウンド タスクによって削除されるのを待っている、オンライン インデックス作成操作の中止の結果として作成された行セットの数。|  
|**Dropped rowset cleanups/sec**|遅延および削除済み行セットをクリーンアップするバックグラウンド タスクによって正常に削除された、オンライン インデックス作成操作の中止の結果として作成された 1 秒あたりの行セットの数。|  
|**Dropped rowsets skipped/sec**|遅延および削除済み行セットをクリーンアップするバックグラウンド タスクによってスキップされた、オンライン インデックス作成操作の中止の結果として作成された 1 秒あたりの行セットの数。|  
|**Extent Deallocations/sec**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のこのインスタンスのすべてのデータベースで、1 秒あたりに割り当て解除されたエクステントの数。|  
|**Extents Allocated/sec**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のこのインスタンスのすべてのデータベースで、1 秒あたりに割り当てられたエクステントの数。|  
|**Failed AU cleanup batches/sec**|遅延および削除済みアロケーション ユニットをクリーンアップするバックグラウンド タスクで失敗し、再試行が必要な 1 秒あたりのバッチの数。 失敗の原因としては、メモリやディスク領域の不足、ハードウェア障害などがあります。|  
|**Failed leaf page cookie**|リーフ ページで変更が行われたため、インデックス検索時にリーフ ページクッキーを使用できなかった回数。 クッキーはインデックス検索を高速化するために使用されます。|  
|**Failed tree page cookie**|ツリー ページの親ページで変更が行われたため、インデックス検索時にツリー ページ クッキーを使用できなかった回数。 クッキーはインデックス検索を高速化するために使用されます。|  
|**Forwarded Records/sec**|転送されたレコード ポインターによって 1 秒あたりにフェッチされたレコードの数。|  
|**FreeSpace Page Fetches/sec**|空き領域スキャンによってフェッチされた 1 秒あたりのページ数。 このスキャンでは、レコード フラグメントの挿入要求または変更要求を達成するために、アロケーション ユニットに既に割り当てられているページ内の空き領域が検索されます。|  
|**FreeSpace Scans/sec**|レコード フラグメントの挿入または変更を目的として、アロケーション ユニットに既に割り当てられているページ内の空き領域を検索するために開始された 1 秒あたりのスキャンの数。 1 回のスキャンで複数のページが検索される場合があります。|  
|**Full Scans/sec**|1 秒あたりの制限されていないフル スキャンの数。 ベース テーブル スキャンまたはフル インデックス スキャンのどちらかです。|  
|**Index Searches/sec**|1 秒あたりのインデックス検索の数。 範囲スキャンの開始、範囲スキャンの再位置決め、スキャン ポイントの再検証、1 つのインデックス レコードのフェッチ、新しい行の挿入場所を探すためのインデックスの検索に使用されます。|  
|**InSysXact waits/sec**|InSysXact ビットが設定されているためにリーダーがページを待機する必要がある回数。|  
|**LobHandle Create Count**|作成された一時 LOB の数。|  
|**LobHandle Destroy Count**|破棄された一時 LOB の数。|  
|**LobSS Provider Create Count**|作成された LOB ストレージ サービス プロバイダー (LobSSP) の数。 LobSSP ごとに 1 つの作業テーブルが作成されます。|  
|**LobSS Provider Destroy Count**|破棄された LobSSP の数。|  
|**LobSS Provider Truncation Count**|切り捨てられた LobSSP の数。|  
|**Mixed page allocations/sec**|混合エクステントから 1 秒あたりに割り当てられたページ数。 IAM ページと、アロケーション ユニットに割り当てられた最初の 8 ページの保存に使用できます。|  
|**Page compression attempts/sec**|ページ レベルの圧縮に対して評価されたページの数。 サイズを大幅に節約できるため、圧縮されなかったページも含まれます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス内のすべてのオブジェクトを含みます。 特定のオブジェクトの詳細については、「 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)のこのインスタンスのすべてのデータベースで、1 秒あたりに割り当て解除されたエクステントの数。|  
|**Page Deallocations/sec**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のこのインスタンスのすべてのデータベースで、1 秒あたりに割り当て解除されたページの数。 混合エクステントと単一エクステントからのページが含まれます。|  
|**Page Splits/sec**|インデックス ページがオーバーフローしたために生じた 1 秒あたりのページ分割の数。|  
|**Pages Allocated/sec**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のこのインスタンスのすべてのデータベースで、1 秒あたりに割り当てられたページの数。 混合エクステントと単一エクステントの両方からのページ アロケーションが含まれます。|  
|**Pages compressed/sec**|ページの圧縮を使用して圧縮されるデータ ページの数。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス内のすべてのオブジェクトを含みます。 特定のオブジェクトの詳細については、「 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)のこのインスタンスのすべてのデータベースで、1 秒あたりに割り当て解除されたエクステントの数。|  
|**Probe Scans/sec**|インデックスまたはベース テーブル内の 1 つの限定された行を直接検索するときに使用される 1 秒あたりのプローブ スキャンの数。|  
|**Range Scans/sec**|1 秒あたりにインデックスでスキャン範囲が限定されたスキャンの数。|  
|**Scan Point Revalidations/sec**|スキャン ポイントがスキャンを続行するために再検証された 1 秒あたりの回数。|  
|**Skipped Ghosted Records/sec**|スキャン中にスキップされた 1 秒あたりの非実体レコードの数。|  
|**Table Lock Escalations/sec**|テーブルでロックが TABLE 粒度または HoBT 粒度にエスカレートされた回数。|  
|**Used leaf page cookie**|リーフ ページで変更が行われなかったため、インデックス検索時にリーフ ページ クッキーが正常に使用された回数。 クッキーはインデックス検索を高速化するために使用されます。|  
|**Used tree page cookie**|ツリー ページの親ページで変更が行われなかったため、インデックス検索時にツリー ページ クッキーが正常に使用された回数。 クッキーはインデックス検索を高速化するために使用されます。|  
|**Workfiles Created/sec**|1 秒あたりに作成された作業ファイルの数。 たとえば、作業ファイルを使用して、ハッシュ結合やハッシュ集計の一時結果を保存できます。|  
|**Worktables Created/sec**|1 秒あたりに作成された作業テーブルの数。 たとえば、作業テーブルを使用して、クエリ スプール、LOB 変数、XML 変数、およびカーソルの一時的な結果を保存できます。|  
|**Worktables From Cache Base**|内部使用のみです。|  
|**Worktables From Cache Ratio**|作成された作業テーブルのうち、作業テーブルの最初の 2 ページが割り当てられなかったが、作業テーブル キャッシュから直ちに使用できるようになった作業テーブルの割合。 作業テーブルを削除した場合、2 つのページが割り当てられたままになり、作業テーブル キャッシュに返されます。 これによりパフォーマンスが向上します。|  
  
## <a name="see-also"></a>参照  
 [リソースの利用状況の監視 &#40;システム モニター&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
