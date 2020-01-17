---
title: sys.dm_pdw_nodes_exec_query_statistics_xml (Transact-sql) |Microsoft Docs
description: インフライト要求のクエリ実行プランを返す動的管理ビュー。 この DMV を使用すると、一時的な統計情報を含む showplan XML を取得できます。
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
ms.openlocfilehash: 2b12e1a1400ec2d9d4bb85466671cda446511f24
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73145647"
---
# <a name="dm_pdw_nodes_exec_query_statistics_xml-transact-sql"></a>sys.dm_pdw_nodes_exec_query_statistics_xml (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

インフライト要求のクエリ実行プランを返します。 この DMV を使用すると、一時的な統計情報を含む showplan XML を取得できます。

## <a name="table-returned"></a>返されたテーブル

|Column Name|[データ型]|Description|  
|-----------------|---------------|-----------------|
|node_id|**int**|ノードに関連付けられている一意の数値 ID。|
|session_id|**smallint**|セッションの ID。 Null 値は許容されません。|
|request_id|**int**|要求の ID。 Null 値は許容されません。|
|sql_handle|**varbinary(64)**|クエリが含まれているバッチまたはストアドプロシージャを一意に識別するトークンです。 Nullable.|
|plan_handle|**varbinary(64)**|現在実行中のバッチのクエリ実行プランを一意に識別するトークンです。 Nullable.|
|query_plan|**xml**|部分統計を含む*plan_handle*で指定されたクエリ実行プランのランタイム Showplan 表現を格納します。 Showplan は XML 形式です。 アドホック [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、ストアドプロシージャ呼び出し、ユーザー定義関数呼び出しなどを含むバッチごとに1つのプランが生成されます。 Nullable.|

## <a name="remarks"></a>備考
[sys.dm_exec_query_statistics_xml](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql?view=sql-server-ver15)でも同じ解説が適用されます。   

## <a name="permissions"></a>Permissions  
 サーバーに対する `VIEW SERVER STATE` 権限が必要です。  

## <a name="see-also"></a>参照  
 [SQL Data Warehouse および並列データウェアハウスの動的管理&#40;ビュー transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

 ## <a name="next-steps"></a>次のステップ
 開発のヒントについては、「 [SQL Data Warehouse 開発の概要](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)」を参照してください。

