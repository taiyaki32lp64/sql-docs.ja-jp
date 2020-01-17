---
title: sys.fulltext_index_fragments (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_index_fragments
- sys.fulltext_index_fragments_TSQL
- fulltext_index_fragments_TSQL
- sys.fulltext_index_fragments
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], fragments
- full-text indexes [SQL Server], metadata
- troubleshooting [SQL Server], full-text search
- sys.fulltext_index_fragments catalog view
ms.assetid: a82e5018-5d88-45c0-9a47-c251e17a6cdb
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 295d924422410bbf247d9b96d27b705fdfe3b5d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133817"
---
# <a name="sysfulltextindexfragments-transact-sql"></a>sys.fulltext_index_fragments (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  フルテキスト インデックスと呼ばれる内部テーブルを使用して *、フルテキスト インデックス フラグメント*逆インデックスのデータを格納します。 このビューを使用すると、これらのフラグメントに関するメタデータをクエリできます。 このビューは、フルテキスト インデックスが含まれているすべてのテーブルのフルテキスト インデックス フラグメントごとに 1 行のデータを格納しています。  
 
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|table_id|**int**|フルテキスト インデックス フラグメントが含まれているテーブルのオブジェクト ID。|  
|fragment_object_id|**int**|フラグメントに関連付けられている内部テーブルのオブジェクト ID。|  
|fragment_id|**int**|フルテキスト インデックス フラグメントの論理 ID。 テーブルのすべてのフラグメントで一意です。|  
|TIMESTAMP|**timestamp**|フラグメントの作成に関連付けられているタイムスタンプ。 新しいフラグメントのタイムスタンプは、古いフラグメントのタイムスタンプよりも大きくなります。|  
|data_size|**int**|フラグメントの論理サイズ (バイト単位)。|  
|row_count|**int**|フラグメント内の個々 の行の数。|  
|status|**int**|フラグメントのいずれかの状態:<br /><br /> 0 = 新たに作成され、まだ使用されていません。<br /><br /> 1 = フルテキスト インデックスの作成またはマージ中に挿入のために使用されています。<br /><br /> 4 = 閉じています。 クエリを実行できます。<br /><br /> 6 = マージ入力のために使用されています。クエリを実行できます。<br /><br /> 8 = 削除用にマークします。 クエリやマージ ソースは使用されません。<br /><br /> 状態が 4 または 6 の場合、フラグメントは論理フルテキスト インデックスの一部であるし、クエリを実行できます。つまりは、*クエリ可能な*フラグメント。|  
  
## <a name="remarks"></a>コメント  
 sys.fulltext_index_fragments カタログ ビューを使用すると、フルテキスト インデックスを構成するフラグメントの数を照会できます。 フルテキスト クエリのパフォーマンスに問題がある場合は、次のように、sys.fulltext_index_fragments を使用してフルテキスト インデックス内のクエリ可能なフラグメント (状態が 4 または 6 のフラグメント) の数を照会します。  
  
```  
SELECT table_id, status FROM sys.fulltext_index_fragments  
   WHERE status=4 OR status=6;  
```  
  
 多くのクエリ可能なフラグメントが存在しない場合は、フラグメントをマージする、フルテキスト インデックスを含むフルテキスト カタログを再編成することをお勧めします。 再編成する、フルテキスト カタログの使用[ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)*catalog_name*を再構成します。 たとえば、という名前のフルテキスト カタログを再編成する`ftCatalog`で、`AdventureWorks2012`データベースを入力します。  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT CATALOG ftCatalog REORGANIZE;  
GO  
```  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [フルテキスト インデックスの作成](../../relational-databases/search/populate-full-text-indexes.md)  
  
  
