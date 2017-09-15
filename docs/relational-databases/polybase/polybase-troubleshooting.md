---
title: "PolyBase のトラブルシューティング | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- PolyBase, monitoring
- PolyBase, performance monitoring
helpviewer_keywords:
- PolyBase, troubleshooting
ms.assetid: f119e819-c3ae-4e0b-a955-3948388a9cfe
caps.latest.revision: 22
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: fa59193fcedb1d5437d8df14035fadca2b3a28f1
ms.openlocfilehash: e65ea926f3a2d2fb3c30c511a1fbba6150de7b42
ms.contentlocale: ja-jp
ms.lasthandoff: 07/31/2017

---
# <a name="polybase-troubleshooting"></a>PolyBase のトラブルシューティング
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  PolyBase のトラブルシューティングを行うには、このトピックに記載されている手法を使用してください。  
  
## <a name="catalog-views"></a>カタログ ビュー  
 PolyBase の操作を管理するには、次に示すカタログ ビューを使用します。  
  
|||  
|-|-|  
|表示|説明|  
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
  
1.  **実行時間が最長のクエリを検索する**  
  
     実行時間が最長のクエリの実行 ID を記録します。  
  
    ```tsql  
     -- Find the longest running query  
    SELECT execution_id, st.text, dr.total_elapsed_time  
    FROM sys.dm_exec_distributed_requests  dr  
         cross apply sys.dm_exec_sql_text(sql_handle) st  
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
2.  **分散クエリの実行時間が最長の手順を検索する**  
  
     前の手順で記録した実行 ID を使用します。 実行時間が最長の手順の手順インデックスを記録します。  
  
     実行時間が最長の手順の location_type を確認します。  
  
    -   Head または Compute: SQL の操作を意味します。 手順 3a に進みます。  
  
    -   DMS: PolyBase データ移動サービスの操作を意味します。 手順 3b に進みます。  
  
    ```tsql  
    -- Find the longest running step of the distributed query plan  
    SELECT execution_id, step_index, operation_type, distribution_type,   
    location_type, status, total_elapsed_time, command   
    FROM sys.dm_exec_distributed_request_steps   
    WHERE execution_id = 'QID4547'   
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
3.  **実行時間が最長の手順の実行の進行状況を検索する**  
  
    1.  **SQL の手順の実行の進行状況を検索します**  
  
         前の手順で記録した実行 ID と手順のインデックスを使用します。 前の手順で記録した実行 ID と手順のインデックスを使用します。  
  
        ```tsql  
        -- Find the execution progress of SQL step    
        SELECT execution_id, step_index, distribution_id, status,   
        total_elapsed_time, row_count, command   
        FROM sys.dm_exec_distributed_sql_requests   
        WHERE execution_id = 'QID4547' and step_index = 1;  
  
        ```  
  
    2.  **DMS の手順の実行の進行状況を検索します**  
  
         前の手順で記録した実行 ID と手順のインデックスを使用します。  
  
        ```tsql  
        -- Find the execution progress of DMS step    
        SELECT execution_id, step_index, dms_step_index, status,   
        type, bytes_processed, total_elapsed_time  
        FROM sys.dm_exec_dms_workers   
        WHERE execution_id = 'QID4547'   
        ORDER BY total_elapsed_time DESC;  
  
        ```  
  
4.  **外部の DMS 操作の情報を検索する**  
  
     前の手順で記録した実行 ID と手順のインデックスを使用します。  
  
    ```tsql  
    SELECT execution_id, step_index, dms_step_index, compute_node_id,   
    type, input_name, length, total_elapsed_time, status   
    FROM sys.dm_exec_external_work   
    WHERE execution_id = 'QID4547' and step_index = 7   
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
## <a name="to-view-the--polybase-query-plan"></a>PolyBase クエリ プランを参照するには  
  
1.  SSMS で、[ **実際の実行プランを含める** ] \(Ctrl + M) を有効にし、クエリを実行します。  
  
2.  [ **実行プラン** ] タブをクリックします。  
  
     ![PolyBase クエリ プラン](../../relational-databases/polybase/media/polybase-query-plan.png "PolyBase クエリ プラン")  
  
3.  [ **Remote Query 操作** ] を右クリックし、[ **プロパティ**] を選択します。  
  
4.  Remote Query の値をコピーし、テキスト エディターに貼り付け、XML リモート クエリ プランを表示します。  例を次に示します。  
  
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
  
1.  グループのヘッド ノードの SQL Server に接続します。  
  
2.  DMV [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md) を実行し、PolyBase グループのすべてのノードを表示します。  
  
3.  DMV [sys.dm_exec_compute_node_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md) を実行し、PolyBase グループのすべてのノードの状態を表示します。  
  
 ## <a name="known-limitations"></a>既知の制限事項
 
 PolyBase には次の制限事項があります。 
 - 可変長列の全長を含め、最大行サイズは 1 MB 以下にする必要があります。 
 - PolyBase では、Hive 0.12 以降のデータ型 (つまり、Char(), VarChar()) はサポートされません。   
 - SQL Server または Azure SQL データ ウェアハウスから ORC ファイル形式にデータをエクスポートするとき、java のメモリ不足エラーに起因し、テキストでいっぱいの列はわずか 50 列に制限されることがあります。 この問題を回避するには、列の一部だけをエクスポートします。
- [SQL Server 2016 のフェールオーバー クラスターにノードを追加すると、PolyBase の機能をインストールできません](https://support.microsoft.com/en-us/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster)
  
## <a name="error-messages-and-possible-solutions"></a>エラー メッセージと考えられる解決策

外部テーブルのエラーのトラブルシューティングについては、Murshed Zaman のブログ [https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/](https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/ "PolyBase setup errors and possible solutions")を参照してください。

## <a name="see-also"></a>参照
[PolyBase Kerberos の接続性のトラブルシューティング](polybase-troubleshoot-connectivity.md)
