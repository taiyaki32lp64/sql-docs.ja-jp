---
title: sp_primarykeys (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_primarykeys_TSQL
- sp_primarykeys
dev_langs:
- TSQL
helpviewer_keywords:
- sp_primarykeys
ms.assetid: 0f76dd31-5b7b-4209-9e2e-b9ed5cac164d
author: stevestein
ms.author: sstein
ms.openlocfilehash: ccae0385ef8c9305f4972ff6dcbd7a7960200370
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056310"
---
# <a name="spprimarykeys-transact-sql"></a>sp_primarykeys (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定されたリモート テーブルの主キー列を、キー列ごとに 1 行ずつ返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_primarykeys [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @table_server = ] 'table_server'_` 主キーの情報を返すリンク サーバーの名前です。 *table_server*は**sysname**、既定値はありません。  
  
`[ @table_name = ] 'table_name'` 主キーの情報を提供する対象のテーブルの名前です。 *table_name*は**sysname**、既定値は NULL です。  
  
`[ @table_schema = ] 'table_schema'` テーブル スキーマを示します。 *table_schema、* は**sysname**、既定値は NULL です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境では、これはテーブル所有者に相当します。  
  
`[ @table_catalog = ] 'table_catalog'` カタログの名前は、指定した*table_name*が存在します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]環境では、これは、データベース名に対応します。 *table_catalog*は**sysname**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|テーブル カタログ。|  
|**TABLE_SCHEM**|**sysname**|テーブル スキーマ。|  
|**TABLE_NAME**|**sysname**|テーブルの名前。|  
|**COLUMN_NAME**|**sysname**|列の名前です。|  
|**KEY_SEQ**|**int**|複数列の主キー列のシーケンス番号。|  
|**PK_NAME**|**sysname**|主キー識別子。 データ ソースに適用されない場合は、NULL を返します。|  
  
## <a name="remarks"></a>コメント  
 **sp_primarykeys**の PRIMARY_KEYS 行セットのクエリを実行することによって実行される、 **IDBSchemaRowset**に対応する OLE DB プロバイダーのインターフェイス*table_server*します。 *Table_name*、 *、table_schema、* 、 *table_catalog*、および*列*行を制限するには、このインターフェイスに渡されるパラメーター返されます。  
  
 **sp_primarykeys**設定の PRIMARY_KEYS 行セットを指定したリンク サーバーの OLE DB プロバイダーがサポートしていない場合、空の結果を返します、 **IDBSchemaRowset**インターフェイス。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例の主キー列を返します、`LONDON1`用のサーバー、`HumanResources.JobCandidate`テーブルに、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]データベース。  
  
```  
EXEC sp_primarykeys @table_server = N'LONDON1',   
   @table_name = N'JobCandidate',  
   @table_catalog = N'AdventureWorks2012',   
   @table_schema = N'HumanResources';  
```  
  
## <a name="see-also"></a>関連項目  
 [分散クエリ ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_tables_ex &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
