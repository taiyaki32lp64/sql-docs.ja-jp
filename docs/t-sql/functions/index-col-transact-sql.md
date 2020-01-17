---
title: INDEX_COL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- INDEX_COL_TSQL
- INDEX_COL
dev_langs:
- TSQL
helpviewer_keywords:
- displaying column names
- INDEX_COL function
- viewing column names
- column names [SQL Server]
- names [SQL Server], columns
ms.assetid: 4db1fb3b-e46f-43fb-b269-a5b6e8b39ed0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a308225e96c740680b2df243f35cac216f53e3e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024303"
---
# <a name="indexcol-transact-sql"></a>INDEX_COL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  インデックス付きの列名を返します。 XML インデックスに対して NULL を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
INDEX_COL ( '[ database_name . [ schema_name ] .| schema_name ]  
    table_or_view_name', index_id , key_id )   
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 データベースの名前です。  
  
 *schema_name*  
 インデックスが組み込まれているスキーマの名前です。  
  
 *table_or_view_name*  
 テーブルまたはインデックス付きビューのスキーマです。 *table_or_view_name* 単一引用符で区切る必要があるあり、データベース名とスキーマ名で完全に修飾することができます。  
  
 *index_id*  
 インデックスの ID です。 *index_ID* は **int**です。  
  
 *key_id*  
 インデックス キー列の位置です。 *key_ID* is **int**.  
  
## <a name="return-types"></a>戻り値の型  
 **nvarchar (128** **)**  
  
## <a name="exceptions"></a>例外  
 エラーが発生した場合、または呼び出し元にオブジェクトの表示権限がない場合は、NULL が返されます。  
  
 ユーザーが所有しているか、または権限を与えられている、セキュリティ保護可能なリソースのメタデータのみを表示できます。 つまり、オブジェクトに対する権限がユーザーに与えられていない場合、メタデータを生成する組み込み関数 (INDEX_COL など) が NULL を返す可能性があります。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-indexcol-to-return-an-index-column-name"></a>A. INDEX_COL を使用してインデックス列名を返す  
 この例では、インデックス `PK_SalesOrderDetail_SalesOrderID_LineNumber` の 2 つのキー列の列名を返します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   
    INDEX_COL (N'AdventureWorks2012.Sales.SalesOrderDetail', 1,1) AS  
        [Index Column 1],   
    INDEX_COL (N'AdventureWorks2012.Sales.SalesOrderDetail', 1,2) AS  
        [Index Column 2]  
;  
GO  
```  
  
 以下に結果セットを示します。  
  
```  
Index Column 1      Index Column 2  
-----------------------------------------------  
SalesOrderID        SalesOrderDetailID  
```  
  
## <a name="see-also"></a>参照  
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
