---
title: sys.dm_fts_index_keywords_position_by_document (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document
- sys.dm_fts_index_keywords_position_by_document
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_keywords_position_by_document dynamic management view
ms.assetid: 0d70184f-baa2-411b-a32d-a4c5af890edd
author: pmasl
ms.author: pelopes
ms.openlocfilehash: feaf2a222df364a41e51969a2c95a978f2d0a289
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900956"
---
# <a name="sysdmftsindexkeywordspositionbydocument-transact-sql"></a>sys.dm_fts_index_keywords_position_by_document (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  インデックス付きドキュメント内のキーワードの位置情報を返します。  
  
## <a name="syntax"></a>構文  
  
```  
sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('database_name'),   
OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>引数  
 db_id('*database_name*')  
 呼び出し、 [DB_ID()](../../t-sql/functions/db-id-transact-sql.md)関数。 この関数は、データベース名を受け取り、どの sys.dm_fts_index_keywords_position_by_document は、指定されたデータベースの検索を使用して、データベースの ID を返します。  
  
 object_id('*table_name*')  
 呼び出し、 [OBJECT_ID()](../../t-sql/functions/object-id-transact-sql.md)関数。 この関数はテーブル名を受け取り、調べるフルテキスト インデックスが含まれているテーブルのテーブル ID を返します。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|[列]|データ型|説明|  
|------------|---------------|-----------------|  
|キーワード (keyword)|**varbinary (128)**|キーワードを表すバイナリ文字列。|  
|display_term|**nvarchar (4000)**|人間が判読できる形式のキーワードです。 この形式は、フルテキスト インデックスに格納されている内部形式から派生しています。|  
|column_id|**int**|現在のキーワードのフルテキスト インデックスが作成された列の ID です。|  
|document_id|**bigint**|現在の用語のフルテキスト インデックスが作成されたドキュメントまたは行の ID です。 この ID は、ドキュメントまたは行のフル テキスト キー値に対応します。|  
|position|**int**|ドキュメント内のキーワードの位置。|  
  
## <a name="remarks"></a>コメント  
 DMV を使用して、インデックス付きドキュメントにインデックス付けされた単語の場所を識別します。 この DMV のトラブルシューティングに使用できる際に問題**sys.dm_fts_index_keywords_by_document**単語は、フルテキスト インデックスが、それらの単語を使用してクエリを実行すると、ドキュメントは返されませんを示します。  
  
## <a name="permissions"></a>アクセス許可  
 フルテキスト インデックスに含まれる列に対する SELECT 権限と、CREATE FULL TEXT CATALOG 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、キーワードを返してのフルテキスト インデックスから、`Production.Document`のテーブル、`AdventureWorks`サンプル データベース。  
  
```  
USE AdventureWorks2012;  
GO   
  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
);   
GO  
```  
  
 さらに、場所を特定する、次の例クエリと同様に、その他の columns_id では、述語を追加できます。  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
)  
WHERE document_id = 7 AND display_term = 'performance';  
```  
  
## <a name="see-also"></a>関連項目  
 [フルテキスト検索](../../relational-databases/search/full-text-search.md)   
 [フルテキスト インデックスのパフォーマンスを向上させる](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)   
 [フルテキスト検索およびセマンティック検索関数&#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/full-text-search-and-semantic-search-functions-transact-sql.md)   
 [フルテキスト検索とセマンティック検索の動的管理ビューおよび関数&#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [フルテキスト検索およびセマンティック検索ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
  
