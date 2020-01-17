---
title: sys.dm_pdw_nodes_exec_query_plan (Transact-sql) |Microsoft Docs
description: プランハンドルで指定されたバッチのプラン表示を XML 形式で返す動的管理ビュー。 プランハンドルで指定されたプランは、キャッシュされるか、現在実行中であることができます。
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 96b499ea5bc38d2a4cf9c380116108009ea46086
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73145637"
---
# <a name="syspdw_nodes_dm_exec_query_plan-transact-sql"></a>システム pdw _nodes_dm_exec_query_plan (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

プラン ハンドルで指定されたバッチのプラン表示を XML 形式で返します。 プランハンドルで指定されたプランは、キャッシュされるか、現在実行中であることができます。  

## <a name="table-returned"></a>返されたテーブル  
  
|列名|データ型|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|ノードに関連付けられている一意の数値 ID。| 
|**dbid**|**smallint**|このプランに対応する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがコンパイルされたときに有効であったコンテキスト データベースの ID。 計画外および準備された SQL ステートメントの場合、ステートメントがコンパイルされたデータベースの ID。<br /><br /> 列は null 値を許容します。|  
|**objectid**|**int**|このクエリプランのオブジェクト (ストアドプロシージャやユーザー定義関数など) の ID。 アドホックバッチおよび準備されたバッチの場合、この列は**null**になります。<br /><br /> 列は null 値を許容します。|  
|**number**|**smallint**|番号付きストアドプロシージャの整数。 アドホックバッチおよび準備されたバッチの場合、この列は**null**になります。<br /><br /> 列は null 値を許容します。| 
|**encrypted**|**bit**|対応するストアドプロシージャが暗号化されているかどうかを示します。<br /><br /> 0 = 暗号化されていない<br /><br /> 1 = 暗号化<br /><br /> 列は null 値を許容しません。|  
|**query_plan**|**xml**|*Plan_handle*で指定されたクエリ実行プランのコンパイル時の Showplan 表現を格納します。 Showplan は XML 形式です。 アドホック [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、ストアドプロシージャ呼び出し、ユーザー定義関数呼び出しなどを含むバッチごとに1つのプランが生成されます。<br /><br /> 列は null 値を許容します。|  
  
## <a name="remarks"></a>備考  
[sys.dm_exec_query_plan](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql?view=sql-server-ver15)でも同じ解説が適用されます。  
  
## <a name="permissions"></a>Permissions  
 **Sysadmin**サーバーロールが必要です。または、サーバーに対する `VIEW SERVER STATE` 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [SQL Data Warehouse および並列データウェアハウスの動的管理&#40;ビュー transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

 ## <a name="next-steps"></a>次のステップ
 開発のヒントについては、「 [SQL Data Warehouse 開発の概要](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)」を参照してください。