---
title: 負荷の監視
description: Analytics Platform System (APS) 管理コンソールまたは並列データウェアハウス (PDW) システムビューを使用して、アクティブおよび最近の負荷を監視します。 "
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b284fdcef506924c26e452196db6e9518faa1351
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400962"
---
# <a name="monitor-loads-into-parallel-data-warehouse"></a>並列データウェアハウスへの負荷を監視する
Analytics Platform System (APS) 管理コンソールまたは並列データウェアハウス (PDW)[システムビュー](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-reference-tsql-system-views/)を使用して、アクティブおよび最近の[dwloader](dwloader.md)の読み込みを監視します。 
  
> [!TIP]  
> 読み込みを実行するために SQL ステートメントを使用する INSERT ステートメントまたはビジネスインテリジェンスツールを使用することによって、一部の読み込みが開始されます。 

<!-- MISSING LINKS
To monitor this type of load, see [Monitoring Active Queries](monitor-active-queries.md).  
-->
  
## <a name="prerequisites"></a>前提条件  
読み込みの監視に使用される方法に関係なく、ログインには基になるデータソースにアクセスする権限が必要です。 

<!-- MISSING LINKS
For the permissions to grant, see "Use All of the Admin Console" in [Grant Permissions to Use the Admin Console](grant-permissions-admin-console.md). 

--> 
  
## <a name="monitoring-loads"></a>負荷の監視  
以下のセクションでは、負荷を監視する方法について説明します。  
  
### <a name="to-monitor-loads-by-using-the-admin-console"></a>管理コンソールを使用して負荷を監視するには  
  
1.  管理コンソールにログオンします。 <!-- MISSING LINKS See [Monitor the Appliance by Using the Admin Console;](monitor-admin-console.md) for instructions. --> 
  
2.  上部のメニューで、[**読み込み**] をクリックします。 最近とアクティブなすべての読み込みを含む並べ替え可能なテーブルが表示され、読み込みが完了しているか、まだアクティブになっているかなどの追加情報が表示されます。 列ヘッダーをクリックすると、行が並べ替えられます。  
  
3.  特定の負荷に関するその他の詳細を表示するには、左側の列の [読み込み**ID** ] をクリックします。 詳細ビューでは、負荷の各ステップの進行状況を確認できます。  
  
管理コンソールに表示される負荷に関するメタデータの詳細については、次のシステムビューを参照してください。  
  
-   [dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages](https://msdn.microsoft.com/library/mt203879.aspx)  
  
-   [pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
### <a name="to-monitor-loads-by-using-system-views"></a>システムビューを使用して負荷を監視するには  
SQL Server PDW ビューを使用してアクティブおよび最近の読み込みを監視するには、次の手順に従います。 使用されるシステムビューごとに、ビューによって返される列と可能性のある値の詳細については、そのビューのドキュメントを参照してください。  
  
1.  このビュー `request_id`の`command`列でローダーコマンドラインを見つけることにより、 [dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)ビューでの読み込みのを検索します。  
  
    たとえば、次のコマンドは、コマンドテキストと現在の状態、およびを`request_id`返します。  
  
    ```sql  
    SELECT request_id, status, command FROM sys.dm_pdw_exec_requests;  
    ```  
  
2.  `request_id`を使用して、 [pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md) 、および[sys. pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)ビューを使用して、読み込みに関する追加情報を取得します。 たとえば、次のクエリでは、 `run_id`負荷の開始時刻、終了時刻、および実行時間に関する情報と、処理された行数に関する情報が返されます。  
  
    ```sql  
    SELECT lbr.run_id,   
    er.submit_time, er.end_time, er.total_elapsed_time, er.error_id, lbr.rows_processed, lbr.rows_rejected, lbr.rows_inserted   
    FROM sys.dm_pdw_exec_requests er   
    LEFT OUTER JOIN   
    sys.pdw_loader_backup_runs lbr   
    ON (er.request_id=lbr.requst_id)   
    WHERE er.request_id='12738';  
    ```  
  
<!-- MISSING LINKS

## See Also  
[Common metadata query examples](metadata-query-examples.md)
-->  
  
