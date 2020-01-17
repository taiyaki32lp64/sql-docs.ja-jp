---
title: sp_indexes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_indexes_TSQL
- sp_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sp_indexes
ms.assetid: 25469e72-9d95-463f-912a-193471c8f5e2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 625b1b5bca3c76a0433e0b887d2c291a714c6f54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139920"
---
# <a name="spindexes-transact-sql"></a>sp_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定されたリモート テーブルに関するインデックス情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_indexes [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_db' ]   
     [ , [ @index_name = ] 'index_name' ]   
     [ , [ @is_unique = ] 'is_unique' ]  
```  
  
## <a name="arguments"></a>引数  
 [ @table_server= ] '*table_server*'  
 実行しているリンク サーバーの名前を指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表の情報を要求します。 *table_server*は**sysname**、既定値はありません。  
  
 [ @table_name= ] '*table_name*'  
 インデックス情報を提供する対象のリモート テーブルの名前です。 *table_name*は**sysname**、既定値は NULL です。 NULL の場合、指定したデータベースのすべてのテーブルが返されます。  
  
 [ @table_schema= ] '*table_schema*'  
 テーブル スキーマを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境では、これはテーブル所有者に相当します。 *table_schema、* は**sysname**、既定値は NULL です。  
  
 [ @table_catalog= ] '*table_db*'  
 データベースの名前を指定*table_name*が存在します。 *table_db*は**sysname**、既定値は NULL です。 NULL の場合、 *table_db*の既定値は**マスター**します。  
  
 [ @index_name=] '*index_name*'  
 情報を要求する対象のインデックスの名前です。 *インデックス*は**sysname**、既定値は NULL です。  
  
 [ @is_unique= ] '*is_unique*'  
 情報を返す対象のインデックスの種類です。 *is_unique*は**ビット**、既定値は null の場合、次の値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|1|一意なインデックスに関する情報を返します。|  
|0|一意でないインデックスに関する情報を返します。|  
|NULL|すべてのインデックスに関する情報を返します。|  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|TABLE_CAT|**sysname**|指定したテーブルが存在するデータベースの名前です。|  
|TABLE_SCHEM|**sysname**|テーブルのスキーマです。|  
|TABLE_NAME|**sysname**|リモート テーブルの名前。|  
|NON_UNIQUE|**smallint**|インデックスが一意または一意でないかどうか。<br /><br /> 0 = 一意<br /><br /> 1 = not unique|  
|INDEX_QUALIFER|**sysname**|インデックス所有者の名前。 一部の DBMS 製品は、インデックスを作成するテーブルの所有者以外のユーザーの許可します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、この列は常に同じ**TABLE_NAME**します。|  
|INDEX_NAME|**sysname**|インデックスの名前です。|  
|TYPE|**smallint**|インデックスの種類です。<br /><br /> 0 = テーブルの統計<br /><br /> 1 = クラスター化<br /><br /> 2 = Hashed<br /><br /> 3 = その他|  
|ORDINAL_POSITION|**int**|インデックス内の列の序数です。 インデックスの最初の列は 1 です。 この列は常に値が返されます。|  
|COLUMN_NAME|**sysname**|返される TABLE_NAME の各列の対応する列の名前です。|  
|ASC_OR_DESC|**varchar**|順序は、照合順序で使用されます。<br /><br /> A = 昇順<br /><br /> D = 降順<br /><br /> NULL = 適用なし<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は常に A を返します。|  
|CARDINALITY|**int**|テーブル内の行数またはインデックス内の一意な値の個数です。|  
|PAGES|**int**|インデックスまたはテーブルを格納するページの数です。|  
|FILTER_CONDITION|**nvarchar(** 4000 **)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では値は返されません。|  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例からのすべてのインデックス情報を返します、`Employees`のテーブル、`AdventureWorks2012`上のデータベース、`Seattle1`リンク サーバー。  
  
```  
EXEC sp_indexes @table_server = 'Seattle1',   
   @table_name = 'Employee',   
   @table_schema = 'HumanResources',  
   @table_catalog = 'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>関連項目  
 [分散クエリ ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_tables_ex &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
