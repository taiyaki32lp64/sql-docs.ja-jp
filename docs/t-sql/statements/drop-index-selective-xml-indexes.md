---
title: DROP INDEX (選択的 XML インデックス) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP XML INDEX statement
dev_langs:
- TSQL
ms.assetid: 4779ae84-e5f4-4d04-8fc1-e24a6631b428
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fc1a9b8b91d37359ce7dc2a4845d0d83e81f996a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044155"
---
# <a name="drop-index-selective-xml-indexes"></a>DROP INDEX (選択的 XML インデックス)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で既存の選択的 XML インデックスまたは選択的セカンダリ XML インデックスを削除します。 詳細については、「[選択的 XML インデックス &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
DROP INDEX index_name ON <object>  
    [ WITH ( <drop_index_option> [ ,...n ] ) ]  
  
<object> ::=  
{ database_name.schema_name.table_or_view_name | schema_name.table_or_view_name | table_or_view_name }  
  
<drop_index_option> ::=  
{  
    MAXDOP = max_degree_of_parallelism  
    | ONLINE = { ON | OFF }  
}  
```  
  
##  <a name="Arguments"></a> 引数  
 *index_name*  
 削除する既存のインデックスの名前です。  
  
 *\< object>* インデックスが作成されている XML 列が含まれるテーブルを指定します。 次のいずれかの形式を使用します。  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
-   `table_name`  
  
 *\<drop_index_option>* DROP INDEX のオプションについては、「[DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)」を参照してください。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 DROP INDEX を実行するには、テーブルまたはビューに対する ALTER 権限が必要です。 この権限は、固定サーバー ロール sysadmin と、固定データベース ロール db_ddladmin および db_owner に既定で許可されています。  
  
## <a name="example"></a>例  
 DROP INDEX ステートメントの例を次に示します。  
  
```  
DROP INDEX sxi_index ON tbl;  
```  
  
## <a name="see-also"></a>参照  
 [選択的 XML インデックス &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [選択的 XML インデックスの作成、変更、および削除](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)  
  
  

