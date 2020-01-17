---
title: dm_operation_status (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 06/05/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dm_operation_status_TSQL
- dm_operation_status
- sys.dm_operation_status
- sys.dm_operation_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_operation_status dynamic management view
- sys.dm_operation_status dynamic management view
ms.assetid: cc847784-7f61-4c69-8b78-5f971bb24d61
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: c49e4e01dd8ddaf0667546a8cc221a7918f42c81
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2019
ms.locfileid: "70911203"
---
# <a name="sysdm_operation_status-azure-sql-database"></a>sys.dm_operation_status (Azure SQL データベース)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] サーバーのデータベースに対して実行される操作に関する情報を返します。  
  
|列名|[データ型]|[説明]|  
|-----------------|---------------|-----------------|  
|session_activity_id|**uniqueidentifier**|操作の ID。 NULL 以外です。|  
|resource_type|**int**|操作が実行される対象のリソースの種類を示します。 NULL 以外です。 現在のリリースでは、このビューが追跡するのは [!INCLUDE[ssSDS](../../includes/sssds-md.md)] に対して実行される操作のみであり、これに対応する整数値は 0 です。|  
|resource_type_desc|**nvarchar(2048)**|操作が実行される対象のリソースの種類の説明。 現在のリリースでは、このビューが追跡するのは [!INCLUDE[ssSDS](../../includes/sssds-md.md)] に対して実行される操作のみです。|  
|major_resource_id|**sql_variant**|操作が実行される対象の [!INCLUDE[ssSDS](../../includes/sssds-md.md)] の名前。 Not Null。|  
|minor_resource_id|**sql_variant**|内部使用のみです。 NULL 以外です。|  
|operation|**nvarchar(60)**|[!INCLUDE[ssSDS](../../includes/sssds-md.md)] に対して実行される操作。たとえば、CREATE や ALTER などです。|  
|state|**tinyint**|操作の状態。<br /><br /> 0 = 保留<br />1 = 実行中<br />2 = 完了<br />3 = 失敗<br />4 = 取り消し|  
|state_desc|**nvarchar(120)**|PENDING = 操作はリソースまたはクォータが利用可能になるのを待機しています。<br /><br /> IN_PROGRESS = 操作は開始され、実行中です。<br /><br /> COMPLETED = 操作が正常に完了しました。<br /><br /> FAILED = 操作が失敗しました。 詳細については、 **error_desc**列を参照してください。<br /><br /> CANCELLED = ユーザーの要求によって操作が停止しました。|  
|percent_complete|**int**|操作が完了した割合 (%)。 値が連続しておらず、有効な値が以下に一覧表示されます。 Not NULL。<br/><br/>0 = 操作は開始されていません<br/>50 = 操作が進行中です<br/>100 = 操作の完了|  
|error_code|**int**|失敗した操作中に発生したエラーを示すコード。 値が 0 の場合は、操作が正常に完了したことを示します。|  
|error_desc|**nvarchar(2048)**|失敗した操作中に発生したエラーの説明。|  
|error_severity|**int**|失敗した操作中に発生したエラーの重大度レベル。 エラーの重大度の詳細については、「[データベースエンジンエラーの重大度](https://go.microsoft.com/fwlink/?LinkId=251052)」を参照してください。|  
|error_state|**int**|将来使用するために予約されています。 将来の互換性は保証されません。|  
|start_time|**datetime**|操作が開始した時点のタイムスタンプ。|  
|last_modify_time|**datetime**|実行時間の長い操作のレコードが最後に変更された時点のタイムスタンプ。 操作が正常に完了した場合、このフィールドには操作が完了した時点のタイムスタンプが表示されます。|  
  
## <a name="permissions"></a>アクセス許可  
 このビューは、サーバーレベルプリンシパルログインの**master**データベースでのみ使用できます。  
  
## <a name="remarks"></a>Remarks  
 このビューを使用するには、 **master**データベースに接続している必要があります。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーの**master**データベースの `sys.dm_operation_status` ビューを使用して、[!INCLUDE[ssSDS](../../includes/sssds-md.md)]で実行される次の操作の状態を追跡します。  
  
-   データベースの作成  
  
-   データベースをコピーします。 データベースのコピーによって、ソース サーバーおよび対象サーバーの両方にあるこのビューに、レコードが作成されます。  
  
-   データベースの変更  
  
-   サービス層のパフォーマンス レベルの変更  
  
-   データベースのサービス層を変更します (Basic から Standard への変更など)。  
  
-   地理的レプリケーション リレーションシップの設定  
  
-   地理的レプリケーション リレーションシップの終了  
  
-   ダイアログ ボックスの  
  
-   データベースの削除  
  
## <a name="example"></a>例  
 データベース ' mydb ' に関連付けられている最新の geo レプリケーション操作を表示します。  
  
```  
SELECT * FROM sys.dm_operation_status   
   WHERE major_resource_id = 'myddb'   
   ORDER BY start_time DESC;  
```  
  
## <a name="see-also"></a>参照  
 [Geo レプリケーションの動的管理ビューおよび関数&#40;Azure SQL Database&#41; ](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)   
 [dm_geo_replication_link_status &#40;Azure SQL Database&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [geo_replication_links &#40;Azure SQL Database&#41; ](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)  
  
  
