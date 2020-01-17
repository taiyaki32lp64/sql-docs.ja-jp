---
title: sp_tables_ex (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_tables_ex
- sp_tables_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tables_ex
ms.assetid: 33755c33-7e1e-4ef7-af14-a9cebb1e2ed4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 77d1512c472005e59909342c94a88c4464c4fe5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096073"
---
# <a name="sptablesex-transact-sql"></a>sp_tables_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  テーブルの指定したリンク サーバーからのテーブルに関する情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_tables_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]  
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @table_type = ] 'table_type' ]   
     [ , [@fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @table_server = ] 'table_server'` テーブル情報を返すリンク サーバーの名前です。 *table_server*は**sysname**、既定値はありません。  
  
``[ , [ @table_name = ] 'table_name']`` データ型情報を返す対象のテーブルの名前です。 *table_name*は**sysname**、既定値は NULL です。  
  
`[ @table_schema = ] 'table_schema']` テーブル スキーマを示します。 *table_schema、* は**sysname**、既定値は NULL です。  
  
`[ @table_catalog = ] 'table_catalog'` データベースの名前は、指定した*table_name*が存在します。 *table_catalog*は**sysname**、既定値は NULL です。  
  
`[ @table_type = ] 'table_type'` 返されるテーブルの種類です。 *table_type*は**sysname**、既定値は null の場合、次の値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**エイリアス**|エイリアスの名前です。|  
|**グローバル一時**|使用可能なシステム全体の一時テーブルの名前です。|  
|**ローカル一時**|現在のジョブにのみ使用可能な一時テーブルの名前。|  
|**SYNONYM**|シノニムの名前です。|  
|**システム テーブル**|システム テーブルの名前です。|  
|**システム ビュー**|システム ビューの名前。|  
|**TABLE**|ユーザー テーブルの名前。|  
|**VIEW**|ビューの名前です。|  
  
`[ @fUsePattern = ] 'fUsePattern'` 決定かどうか、文字 **_** 、 **%** 、 **[** と **]** はワイルドカード文字として解釈されます。 有効な値は 0 (パターン一致がオフ) および 1 (パターン一致では)。 *fUsePattern*は**ビット**、既定値は 1 です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|テーブル修飾子の名前。 さまざまな DBMS 製品は、3 つの部分がテーブルの名前付けをサポート (_修飾子_ **.** _所有者_ **.** _名前_)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、この列は、データベース名を表します。 他の製品で、テーブルのデータベース環境のサーバー名を表します。 このフィールドは NULL を指定できます。|  
|**TABLE_SCHEM**|**sysname**|テーブルの所有者名です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、この列は、テーブルを作成したデータベース ユーザーの名前を表します。 このフィールドは、常に値を返します。|  
|**TABLE_NAME**|**sysname**|テーブル名です。 このフィールドは、常に値を返します。|  
|**TABLE_TYPE**|**varchar(32)**|テーブル、システム テーブルまたはビュー。|  
|**「解説」**|**varchar(254)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] この列の値は返されません。|  
  
## <a name="remarks"></a>コメント  
 **sp_tables_ex**の TABLES 行セットのクエリを実行することによって実行される、 **IDBSchemaRowset**に対応する OLE DB プロバイダーのインターフェイス*table_server*します。 *Table_name*、 *、table_schema、* 、 *table_catalog*、および*列*行を制限するには、このインターフェイスに渡されるパラメーター返されます。  
  
 **sp_tables_ex**設定の TABLES 行セットを指定したリンク サーバーの OLE DB プロバイダーがサポートしていない場合、空の結果を返します、 **IDBSchemaRowset**インターフェイス。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例に含まれているテーブルに関する情報を返します、`HumanResources`内のスキーマ、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]上のデータベース、`LONDON2`リンク サーバー。  
  
```  
EXEC sp_tables_ex @table_server = 'LONDON2',   
@table_catalog = 'AdventureWorks2012',   
@table_schema = 'HumanResources',   
@table_type = 'TABLE';  
```  
  
## <a name="see-also"></a>関連項目  
 [分散クエリ ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_columns_ex &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [sp_column_privileges &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_table_privileges &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
