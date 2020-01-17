---
title: sys.dm_exec_distributed_requests (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_REQUESTS
- DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- sys.dm_exec_distributed_sql_requests management view
- PolyBase
- dm_exec_distributed_sql_requests management view
ms.assetid: c041d416-d8c6-435e-a563-6a310abd33e3
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 37fd17f17d8b6aa1a30f48d75258d27f4a45561a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097805"
---
# <a name="sysdmexecdistributedrequests-transact-sql"></a>sys.dm_exec_distributed_requests (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  現在または最近アクティブでは、PolyBase クエリのすべての要求に関する情報を保持します。 要求/クエリごとに 1 行が一覧表示します。  
  
 セッションに基づいており、要求 ID、ユーザーことができますし、取得、実際の分散要求 sys.dm_exec_distributed_requests を使用して、実行するために生成します。 たとえば、正規 SQL および SQL テーブルの外部に関連するクエリに分解して、さまざまなコンピューティング ノードで実行されるさまざまなステートメント/要求。 すべてのコンピューティング ノード間で分散の手順を追跡するには、それぞれ 1 つの特定の要求と演算子に関連付けられているコンピューティング ノードのすべての操作を追跡するために使用できる 'global' の実行 ID を紹介します。  
  
|列名|データ型|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|sql_handle|**varbinary(64)**|このビューのキー。 要求に関連付けられている一意の数値 id です。|システム内のすべての要求間で一意です。|  
|execution_id|**nvarchar(32**|このクエリが実行されたセッションに関連付けられた一意の数値 id です。||  
|status|**nvarchar(32**|要求の現在の状態。|'保留中'、'承認'、'AcquireSystemResources'、'初期化'、'プラン'、'解析'、'AquireResources'、'Running'、'キャンセル'、'完了'、' 失敗 '、'キャンセル'。|  
|error_id|**nvarchar(36)**|存在する場合、要求に関連するエラーの一意の id。|エラーが発生していない場合は NULL に設定します。|  
|start_time|**datetime**|要求の実行が開始された時刻。|キューに置かれた要求の場合は 0それ以外の場合、有効な datetime より小さいまたは現在の時刻と同じです。|  
|end_time|**datetime**|エンジンが、要求のコンパイルを完了した時刻。|キューまたはアクティブな要求の場合は nullそれ以外の場合、有効な datetime より小さいまたは現在の時刻と同じです。|  
|total_elapsed_time|**int**|ミリ秒単位で、要求を開始からの実行で経過時間。|0 ~ start_time と end_time の違い範囲。Total_elapsed_time では、整数の最大値を超えている場合、最大値になります total_elapsed_time では引き続きします。 この状態が"、最大値を超過しました"警告を生成します。 最大値をミリ秒単位は 24.8 日に相当します。|  
  
## <a name="see-also"></a>関連項目  
 [PolyBase 動的管理ビューでのトラブルシューティング](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [データベース関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
