---
title: PolyBase の監視とトラブルシューティング | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
f1_keywords:
- PolyBase, monitoring
- PolyBase, performance monitoring
helpviewer_keywords:
- PolyBase, troubleshooting
ms.assetid: f119e819-c3ae-4e0b-a955-3948388a9cfe
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 520637f8bcbe8ae1fcd4fee0ebf3fa33fe3b3650
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710490"
---
# <a name="monitor-and-troubleshoot-polybase"></a>PolyBase の監視とトラブルシューティング

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

PolyBase のトラブルシューティングを行うには、このトピックに記載されている手法を使用してください。

## <a name="catalog-views"></a>カタログ ビュー

PolyBase の操作を管理するには、次に示すカタログ ビューを使用します。

|||  
|-|-|  
|表示|[説明]|  
|[sys.external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)|外部テーブルを識別します。|  
|[sys.external_data_sources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)|外部のデータ ソースを識別します。|  
|[sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)|外部のファイル形式を識別します。|  

## <a name="dynamic-management-views"></a>動的管理ビュー  

|||  
|-|-|  
|[sys.dm_exec_compute_node_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)|[sys.dm_exec_compute_node_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md)|  
|[sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|[sys.dm_exec_distributed_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)|  
|[sys.dm_exec_distributed_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-requests-transact-sql.md)|[sys.dm_exec_distributed_sql_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-sql-requests-transact-sql.md)|  
|[sys.dm_exec_dms_services &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-services-transact-sql.md)|[sys.dm_exec_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|[sys.dm_exec_external_operations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-operations-transact-sql.md)|[sys.dm_exec_external_work &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-work-transact-sql.md)|  

PolyBase のクエリは、sys.dm_exec_distributed_request_steps 内で一連のステップに分割されます。 次の表は、ステップ名と関連 DMV のマッピングになっています。

|PolyBase のステップ|関連する DMV|  
|-|-|
|HadoopJobOperation | sys.dm_exec_external_operations|
|RandomIdOperation | sys.dm_exec_distributed_request_steps|
|HadoopRoundRobinOperation | sys.dm_exec_dms_workers|
|StreamingReturnOperation | sys.dm_exec_dms_workers|
|OnOperation | sys.dm_exec_distributed_sql_requests |

## <a name="to-monitor-polybase-queries-using-dmvs"></a>DMV を使用し PolyBase のクエリを監視するには

PolyBase のクエリを監視およびトラブルシューティングするには、次の DMV を使用します。

1. **実行時間が最長のクエリを検索する**  

   実行時間が最長のクエリの実行 ID を記録します。

   ```sql
    -- Find the longest running query  
   SELECT execution_id, st.text, dr.total_elapsed_time  
   FROM sys.dm_exec_distributed_requests  dr  
         cross apply sys.dm_exec_sql_text(sql_handle) st  
   ORDER BY total_elapsed_time DESC;  
   ```

1. **分散クエリの実行時間が最長の手順を検索する**  

   前の手順で記録した実行 ID を使用します。 実行時間が最長の手順の手順インデックスを記録します。

   実行時間が最長の手順の location_type を確認します。  

   - Head または Compute: SQL の操作を意味します。 手順 3a に進みます。

      - DMS: PolyBase データ移動サービスの操作を意味します。 手順 3b に進みます。

      ```sql  
      -- Find the longest running step of the distributed query plan  
      SELECT execution_id, step_index, operation_type, distribution_type,   
      location_type, status, total_elapsed_time, command   
      FROM sys.dm_exec_distributed_request_steps   
      WHERE execution_id = 'QID4547'   
      ORDER BY total_elapsed_time DESC;  
      ```  

1. **実行時間が最長の手順の実行の進行状況を検索する**  

   1. **SQL の手順の実行の進行状況を検索します**  

      前の手順で記録した実行 ID と手順のインデックスを使用します。 前の手順で記録した実行 ID と手順のインデックスを使用します。

      ```sql  
      -- Find the execution progress of SQL step    
      SELECT execution_id, step_index, distribution_id, status,   
      total_elapsed_time, row_count, command   
      FROM sys.dm_exec_distributed_sql_requests   
      WHERE execution_id = 'QID4547' and step_index = 1;  
      ```  

   1. **DMS の手順の実行の進行状況を検索します**

      前の手順で記録した実行 ID と手順のインデックスを使用します。

      ```sql  
      -- Find the execution progress of DMS step    
      SELECT execution_id, step_index, dms_step_index, status,   
      type, bytes_processed, total_elapsed_time  
      FROM sys.dm_exec_dms_workers   
      WHERE execution_id = 'QID4547'   
      ORDER BY total_elapsed_time DESC;
      ```  

1. **外部の DMS 操作の情報を検索する**  

   前の手順で記録した実行 ID と手順のインデックスを使用します。

   ```sql  
   SELECT execution_id, step_index, dms_step_index, compute_node_id,   
   type, input_name, length, total_elapsed_time, status   
   FROM sys.dm_exec_external_work   
   WHERE execution_id = 'QID4547' and step_index = 7   
   ORDER BY total_elapsed_time DESC;  
   ```  

## <a name="to-view-the--polybase-query-plan-to-be-changed"></a>PolyBase クエリ プランを参照するには (変更予定) 

1. SSMS で、 **[実際の実行プランを含める]** (Ctrl + M) を有効にし、クエリを実行します。

2. **[実行プラン]** タブをクリックします。

   ![PolyBase クエリ プラン](../../relational-databases/polybase/media/polybase-query-plan.png "PolyBase クエリ プラン")  

3. **[Remote Query 操作]** を右クリックし、 **[プロパティ]** を選択します。

4. Remote Query の値をコピーし、テキスト エディターに貼り付け、XML リモート クエリ プランを表示します。 例を次に示します。

   ```xml  

   <dsql_query number_nodes="1" number_distributions="8" number_distributions_per_node="8">  
      <sql>ExecuteMemo explain query</sql>  
      <dsql_operations total_cost="0" total_number_operations="6">  
        <dsql_operation operation_type="RND_ID">  
          <identifier>TEMP_ID_74</identifier>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_74] ([SensorKey] INT NOT NULL, [CustomerKey] INT NOT NULL, [GeographyKey] INT, [Speed] FLOAT(53) NOT NULL, [YearMeasured] INT NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">EXEC [tempdb].[sys].[sp_addextendedproperty] @name=N'IS_EXTERNAL_STREAMING_TABLE', @value=N'true', @level0type=N'SCHEMA', @level0name=N'dbo', @level1type=N'TABLE', @level1name=N'TEMP_ID_74'</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">UPDATE STATISTICS [tempdb].[dbo].[TEMP_ID_74] WITH ROWCOUNT = 2401, PAGECOUNT = 7</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="MULTI">  
          <dsql_operation operation_type="STREAMING_RETURN">  
            <operation_cost cost="1" accumulative_cost="1" average_rowsize="24" output_rows="5762.1" />  
            <location distribution="AllDistributions" />  
            <select>SELECT [T1_1].[SensorKey] AS [SensorKey],  
             [T1_1].[CustomerKey] AS [CustomerKey],  
             [T1_1].[GeographyKey] AS [GeographyKey],  
             [T1_1].[Speed] AS [Speed],  
             [T1_1].[YearMeasured] AS [YearMeasured]  
      FROM   (SELECT [T2_1].[SensorKey] AS [SensorKey],  
                     [T2_1].[CustomerKey] AS [CustomerKey],  
                     [T2_1].[GeographyKey] AS [GeographyKey],  
                     [T2_1].[Speed] AS [Speed],  
                     [T2_1].[YearMeasured] AS [YearMeasured]  
              FROM   [tempdb].[dbo].[TEMP_ID_74] AS T2_1  
              WHERE  ([T2_1].[Speed] > CAST (6.50000000000000000E+001 AS FLOAT))) AS T1_1</select>  
          </dsql_operation>  
          <dsql_operation operation_type="ExternalRoundRobinMove">  
            <operation_cost cost="16.594848" accumulative_cost="17.594848" average_rowsize="24" output_rows="19207" />  
            <external_uri>hdfs://10.193.26.177:8020/Demo/car_sensordata.tbl/</external_uri>  
            <destination_table>[TEMP_ID_74]</destination_table>  
          </dsql_operation>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_74]</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
      </dsql_operations>  
   </dsql_query>  
   ```  

## <a name="to-monitor-nodes-in-a-polybase-group"></a>PolyBase グループ内のノードを監視するには  

PolyBase スケール アウト グループの一部として一連のコンピューターを構成すると、マシンの状態を監視できます。 スケール アウト グループの作成の詳細については、「 [PolyBase スケールアウト グループ](../../relational-databases/polybase/polybase-scale-out-groups.md)」を参照してください。

1. グループのヘッド ノードの SQL Server に接続します。

2. DMV [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md) を実行し、PolyBase グループのすべてのノードを表示します。

3. DMV [sys.dm_exec_compute_node_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md) を実行し、PolyBase グループのすべてのノードの状態を表示します。

## <a name="hadoop-name-node-high-availability"></a>Hadoop 名前ノードの高可用性

PolyBase は現在、Zookeeper や Knox などの Name Node HA サービスとやり取りしません。 ただし、この機能を提供するための実績のある回避策を使用できます。

回避策:DNS 名を使用して、アクティブな Name Node への接続を再ルーティングします。 これを行うためには、外部データ ソースが DNS 名を使用して Name Node と通信していることを確認する必要があります。 Name Node のフェールオーバーが発生したときには、外部データ ソースの定義で使用される DNS 名に関連付けられている IP アドレスを変更する必要があります。 これには、すべての新しい接続を適切な Name Node に再ルーティングします。 フェールオーバーが発生したときに、既存の接続は失敗します。 このプロセスを自動化するために、"ハートビート" が、アクティブな Name Node の ping を実行できます。 ハートビートが失敗する場合、フェールオーバーが発生し、セカンダリ IP アドレスに自動的に切り替えると想定できます。

## <a name="error-messages-and-possible-solutions"></a>エラー メッセージと考えられる解決策

外部テーブルのエラーのトラブルシューティングについては、Murshed Zaman のブログ [https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/](https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/ "PolyBase のセットアップ エラーと考えられる解決策") を参照してください。

## <a name="see-also"></a>参照

[PolyBase Kerberos の接続性のトラブルシューティング](polybase-troubleshoot-connectivity.md)
