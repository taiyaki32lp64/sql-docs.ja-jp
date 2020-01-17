---
title: sys.column_store_segments (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_store_segments
- sys.column_store_segments_TSQL
- sys.column_store_segments
- column_store_segments_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_segments catalog view
ms.assetid: 1253448c-2ec9-4900-ae9f-461d6b51b2ea
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b8d476e2f21693254eac5fc4712d53ac854e74ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140002"
---
# <a name="syscolumnstoresegments-transact-sql"></a>sys.column_store_segments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

列ストア インデックス内の各列セグメントの 1 つの行を返します。 行グループごとに各列の 1 つの列セグメントがあります。 たとえば、10 個の行グループと 34 列を含むテーブルは、340 行を返します。 
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|パーティション ID を示します。 データベース内で一意です。|  
|**hobt_id**|**bigint**|この列ストア インデックスを保持するテーブルのヒープまたは B ツリー インデックス (hobt) の ID。|  
|**column_id**|**int**|列ストア列の ID。|  
|**segment_id**|**int**|行グループの ID。 旧バージョンと互換性のため、列名が行グループ ID です。 この場合でも、segment_id を呼び出せる続けます 使用してセグメントを一意に識別できる\<hobt_id で、partition_id、column_id >、< segment_id >。|  
|**version**|**int**|列セグメント形式のバージョンです。|  
|**encoding_type**|**int**|そのセグメントを使用するエンコードの種類です。<br /><br /> 1 = VALUE_BASED - 非文字列/バイナリないディクショナリ (内部のいくつかのバリエーションを 4 によく似ています)<br /><br /> 2 = VALUE_HASH_BASED - の一般的な値がディクショナリ内の文字列/バイナリ列<br /><br /> 3 = STRING_HASH_BASED - の一般的な値がディクショナリ内の文字列/バイナリ列<br /><br /> 4 = STORE_BY_VALUE_BASED - 非文字列/バイナリない辞書で<br /><br /> 5 = STRING_STORE_BY_VALUE_BASED - ない辞書で文字列/バイナリ<br /><br /> すべてのエンコーディングでは、可能な場合のエンコード ビット パッキングと実行の長さの活用します。|  
|**row_count**|**int**|行グループ内の行の数。|  
|**has_nulls**|**int**|列セグメントに null 値がある場合は 1。|  
|**base_id**|**bigint**|エンコードの種類 1 が使用されている場合は、ベース値 id。  エンコードの種類 1 が使用されていない、base_id が-1 に設定します。|  
|**magnitude**|**float**|エンコードの種類 1 が使用されている場合は大きさ。  エンコードの種類 1 が使用されていない、magnitude が-1 に設定します。|  
|**primary_dictionary_id**|**int**|値 0 は、グローバルのディクショナリを表します。 値-1 は、この列用に作成されたグローバル辞書がないことを示します。|  
|**secondary_dictionary_id**|**int**|0 以外の値は、この列に現在のセグメント (つまり行グループ) のローカルのディクショナリを指します。 値-1 は、このセグメントのローカルのディクショナリがないことを示します。|  
|**min_data_id**|**bigint**|列セグメントの最小データ ID。|  
|**max_data_id**|**bigint**|列セグメントの最大データ id。|  
|**null_value**|**bigint**|NULL を表すために使用される値。|  
|**on_disk_size**|**bigint**|(バイト単位) セグメントのサイズ。|  
  
## <a name="remarks"></a>コメント  
 次のクエリでは、列ストア インデックスのセグメントに関する情報を返します。  
  
```sql  
SELECT i.name, p.object_id, p.index_id, i.type_desc,   
    COUNT(*) AS number_of_segments  
FROM sys.column_store_segments AS s   
INNER JOIN sys.partitions AS p   
    ON s.hobt_id = p.hobt_id   
INNER JOIN sys.indexes AS i   
    ON p.object_id = i.object_id  
WHERE i.type = 5 OR i.type = 6  
GROUP BY i.name, p.object_id, p.index_id, i.type_desc ;  
GO  
```  
  
## <a name="permissions"></a>アクセス許可  
 すべての列が少なくとも必要**VIEW DEFINITION**テーブルに対する権限。 ユーザーがあるない限り、列は null を返します**選択**アクセス許可: has_nulls、base_id、magnitude、min_data_id、max_data_id、および null_value します。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server のシステム カタログよく寄せられる質問のクエリを実行します。](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [列ストア インデックス ガイド](~/relational-databases/indexes/columnstore-indexes-overview.md)    
 [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
  
  

