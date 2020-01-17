---
title: sys.server_resource_stats (Azure SQL データベース) |Microsoft Docs
ms.custom: ''
ms.date: 06/28/2018
ms.service: sql-database
ms.reviewer: carlrab, edmaca
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: 72e363b05e8f14dda535abd70e4218c949c42c91
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133072"
---
# <a name="sysserver_resource_stats-azure-sql-database"></a>sys.server_resource_stats (Azure SQL データベース)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Azure SQL マネージ インスタンスの CPU 使用量、IO、およびストレージのデータを返します。 データは、5 分間隔で収集と集計が実行されます。 レポートは 15 秒ごとに 1 つの行があります。 返されるデータには、CPU 使用率、ストレージ サイズ、I/O 使用率、およびマネージ インスタンス SKU が含まれています。 履歴データは約 14 日間保持されます。

**Sys.server_resource_stats**ビューでは、データベースが関連付けられている Azure SQL マネージ インスタンスのバージョンによって異なる定義します。 新しいサーバー バージョンにアップグレードする際は、それら定義の違いとアプリケーションに必要な変更を考慮してください。
 
  
 次の表は、v12 サーバーで使用できる列について説明しています。  
  
|[列]|データ型|説明|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime2**|15 秒のレポート期間の開始を示す UTC 時刻|  
|end_time|**datetime**|15 秒のレポート期間の終了を示す UTC 時刻|
|resource_type|nvarchar (128)|メトリックが提供されているリソースの種類|
|resource_name|nvarchar(128)|リソースの名前。|
|sku|nvarchar(128)|インスタンスのインスタンスのサービス階層を管理します。 使用できる値を次に示します。 <br><ul><li>General Purpose</li></ul><ul><li>Business Critical</li></ul>|
|hardware_generation|nvarchar(128)|ハードウェアの世代の識別子 Gen 4 など Gen 5。|
|virtual_core_count|int|(8、16 または 24 がパブリック プレビュー) のインスタンスあたりの仮想コアの数を表します|
|avg_cpu_percent|decimal(5,2)|インスタンスで使用されるマネージ インスタンスのサービス層の制限の割合で表した平均コンピューティング使用率。 すべてのデータベース インスタンスですべてのリソース プールの CPU 時間の合計として計算は、指定した間隔でその層の使用可能な CPU 時間で割った値します。|
|reserved_storage_mb|BIGINT|インスタンスあたりのストレージに予約されています (ストレージの量は、その顧客のマネージ インスタンスの購入を領域)|
|storage_space_used_mb|decimal(18,2)|(ユーザーとシステムの両方のデータベースを含む) のすべてのマネージ インスタンス データベースのファイルによって使用されるストレージ|
|io_request|BIGINT|間隔内で物理 i/o の合計数|
|io_bytes_read|BIGINT|間隔内で読み取られた物理バイト数|
|io_bytes_written|BIGINT|間隔内に記述された物理バイト数|

 
> [!TIP]  
>  これらの制限とサービス レベルに関する詳細なコンテキスト、トピックを参照してください。[マネージ インスタンスのサービス レベル](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tiers)します。  
    
## <a name="permissions"></a>アクセス許可  
 このビューに接続するアクセス許可を持つすべてのユーザー ロールが使用できる、**マスター**データベース。  
  
## <a name="remarks"></a>コメント  
 によって返されるデータ**sys.server_resource_stats**は、サービスの制限が許容される最大の割合として表現された avg_cpu 以外 (バイト) またはメガバイト数 (列名に記載されている) のいずれかで使用される合計として表されます実行している階層/パフォーマンス レベル。  
 
## <a name="examples"></a>使用例  
 次の例では、過去 1 週間で平均してコンピューティング使用率が 80% 以上になっているすべてのデータベースが返されます。  
  
```sql  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT resource_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.server_resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY resource_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
    
## <a name="see-also"></a>関連項目  
 [インスタンスのサービス レベルの管理](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tiers)
