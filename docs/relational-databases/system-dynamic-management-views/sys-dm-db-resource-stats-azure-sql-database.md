---
title: dm_db_resource_stats (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 05/21/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1dd66834788896e6952a0352eb2a19fd1a828513
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245961"
---
# <a name="sysdm_db_resource_stats-azure-sql-database"></a>sys.dm_db_resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]データベースの CPU、i/o、およびメモリの消費量を返します。 データベースにアクティビティがない場合でも、15 秒ごとに 1 つの行が存在します。 履歴データは約1時間保持されます。  
  
|列|データ型|説明|  
|-------------|---------------|-----------------|  
|end_time|**/**|UTC 時刻は、現在のレポート間隔の終了を示します。|  
|avg_cpu_percent|**decimal (5, 2)**|サービス層の制限に対する割合での平均コンピューティング使用率。|  
|avg_data_io_percent|**decimal (5, 2)**|サービス層の上限に対する平均データ i/o 使用率 (%)。 Hyperscale データベースについては、「[リソース使用率の統計情報のデータ IO](https://docs.microsoft.com/azure/sql-database/sql-database-hyperscale-performance-diagnostics#data-io-in-resource-utilization-statistics)」を参照してください。|  
|avg_log_write_percent|**decimal (5, 2)**|サービス層の制限に対する割合としての、平均トランザクションログの書き込み (MBps)。|  
|avg_memory_usage_percent|**decimal (5, 2)**|サービス層の制限に対する平均メモリ使用率 (%)。<br /><br /> これには、バッファープールページに使用されるメモリと、インメモリ OLTP オブジェクトのストレージが含まれます。|  
|xtp_storage_percent|**decimal (5, 2)**|サービス層の制限 (レポート間隔の終了時) に対するインメモリ OLTP のストレージ使用率。 これには、メモリ最適化テーブル、インデックス、およびテーブル変数の、次のインメモリ OLTP オブジェクトのストレージに使用されるメモリが含まれます。 また、ALTER TABLE 操作の処理に使用されるメモリも含まれています。<br /><br /> インメモリ OLTP がデータベースで使用されていない場合は0を返します。|  
|max_worker_percent|**decimal (5, 2)**|データベースのサービス階層の上限に対する割合での最大同時実行ワーカー (要求)。|  
|max_session_percent|**decimal (5, 2)**|データベースのサービス層の上限に対する割合での最大同時セッション数。|  
|dtu_limit|**通り**|この期間中のこのデータベースの現在の最大データベース DTU 設定です。 仮想コアベースのモデルを使用しているデータベースの場合、この列は NULL になります。|
|cpu_limit|**decimal (5, 2)**|この期間中のこのデータベースの仮想コア数。 DTU ベースのモデルを使用しているデータベースの場合、この列は NULL になります。|
|avg_instance_cpu_percent|**decimal (5, 2)**|SQL DB プロセスに対する平均データベース CPU 使用率 (%)。|
|avg_instance_memory_percent|**decimal (5, 2)**|SQL DB プロセスに対する平均データベースメモリ使用率 (%)。|
|avg_login_rate_percent|**decimal (5, 2)**|単に情報を示すためだけに特定されます。 サポートされていません。 将来の互換性は保証されません。|
|replica_role|**通り**|現在のレプリカのロールのうち、0がプライマリ、1がセカンダリ、2がフォワーダー (geo セカンダリのプライマリ) であることを表します。 読み取り可能なすべてのセカンダリに ReadOnly インテントを使用して接続すると、"1" と表示されます。 ReadOnly インテントを指定せずに geo セカンダリに接続すると、"2" (フォワーダーに接続) が表示されます。|
|||
  
> [!TIP]  
>  これらの制限とサービスレベルの詳細については、[サービス階層](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)とサービス階層の[機能と制限](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)に関するトピックを参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 このビューには、VIEW DATABASE STATE 権限が必要です。  
  
## <a name="remarks"></a>コメント  
 **Dm_db_resource_stats**によって返されるデータは、実行しているサービス階層/パフォーマンスレベルに対して許容される最大制限の割合として表されます。
 
 過去60分以内にデータベースが別のサーバーにフェールオーバーされた場合、ビューはそのフェールオーバー以降にプライマリデータベースであった時間のデータのみを返します。  
  
 保有期間が長いこのデータの詳細なビューを表示するには、 **master**データベースの**resource_stats**カタログビューを使用します。 このビューは、5分ごとにデータをキャプチャし、履歴データを14日間保持します。  詳細については、「 [sys. resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)」を参照してください。  
  
 データベースがエラスティックプールのメンバーである場合、パーセント値として表示されるリソース統計は、エラスティックプール構成で設定されたデータベースの上限に対する比率として表されます。  
  
## <a name="example"></a>例  
  
次の例では、現在接続しているデータベースの最新の時間によって並べ替えられたリソース使用率データを返します。  
  
```  
SELECT * FROM sys.dm_db_resource_stats ORDER BY end_time DESC;  
  
```  
  
 次の例では、過去1時間のユーザーデータベースのパフォーマンスレベルで許容される最大 DTU 制限の割合という観点から、平均 DTU 消費量を示しています。 パフォーマンスレベルは、一定の割合で100% 近くの割合で増やすことを検討してください。  
  
```  
SELECT end_time,   
  (SELECT Max(v)    
   FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS    
   value(v)) AS [avg_DTU_percent]   
FROM sys.dm_db_resource_stats;  
  
```  
  
 次の例では、過去1時間の CPU 使用率、データとログ i/o、およびメモリ使用量の平均値と最大値を返します。  
  
```  
SELECT    
    AVG(avg_cpu_percent) AS 'Average CPU Utilization In Percent',   
    MAX(avg_cpu_percent) AS 'Maximum CPU Utilization In Percent',   
    AVG(avg_data_io_percent) AS 'Average Data IO In Percent',   
    MAX(avg_data_io_percent) AS 'Maximum Data IO In Percent',   
    AVG(avg_log_write_percent) AS 'Average Log Write I/O Throughput Utilization In Percent',   
    MAX(avg_log_write_percent) AS 'Maximum Log Write I/O Throughput Utilization In Percent',   
    AVG(avg_memory_usage_percent) AS 'Average Memory Usage In Percent',   
    MAX(avg_memory_usage_percent) AS 'Maximum Memory Usage In Percent'   
FROM sys.dm_db_resource_stats;  
  
```  
  
## <a name="see-also"></a>参照  
 [resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [サービスレベル](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [サービス層の機能と制限](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
