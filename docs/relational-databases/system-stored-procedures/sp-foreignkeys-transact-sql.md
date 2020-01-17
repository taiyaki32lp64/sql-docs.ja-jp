---
title: sp_foreignkeys (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_foreignkeys_TSQL
- sp_foreignkeys
dev_langs:
- TSQL
helpviewer_keywords:
- sp_foreignkeys
ms.assetid: 935fe385-19ff-41a4-8d0b-30618966991d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2c1aaa12ed6ffb86b6e3f7979deac0e6f933dff8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124375"
---
# <a name="spforeignkeys-transact-sql"></a>sp_foreignkeys (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  リンク サーバー内のテーブルに主キーを参照する外部キーを返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_foreignkeys [ @table_server = ] 'table_server'   
     [ , [ @pktab_name = ] 'pktab_name' ]   
     [ , [ @pktab_schema = ] 'pktab_schema' ]   
     [ , [ @pktab_catalog = ] 'pktab_catalog' ]   
     [ , [ @fktab_name = ] 'fktab_name' ]   
     [ , [ @fktab_schema = ] 'fktab_schema' ]   
     [ , [ @fktab_catalog = ] 'fktab_catalog' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @table_server = ] 'table_server'` テーブル情報を返すリンク サーバーの名前です。 *table_server*は**sysname**、既定値はありません。  
  
`[ @pktab_name = ] 'pktab_name'` 主キーを持つテーブルの名前です。 *pktab_name*は**sysname**、既定値は NULL です。  
  
`[ @pktab_schema = ] 'pktab_schema'` 主キーを持つスキーマの名前です。 *pktab_schema*は**sysname**、既定値は NULL です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、所有者名に相当します。  
  
`[ @pktab_catalog = ] 'pktab_catalog'` 主キーを持つカタログの名前です。 *pktab_catalog*は**sysname**、既定値は NULL です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース名が含まれます。  
  
`[ @fktab_name = ] 'fktab_name'` 外部キー テーブルの名前です。 *fktab_name*は**sysname**、既定値は NULL です。  
  
`[ @fktab_schema = ] 'fktab_schema'` 外部キーを持つスキーマの名前です。 *fktab_schema*は**sysname**、既定値は NULL です。  
  
`[ @fktab_catalog = ] 'fktab_catalog'` 外部キーを持つカタログの名前です。 *fktab_catalog*は**sysname**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
 さまざまな DBMS 製品は、3 つの部分がテーブルの名前付けをサポート (_カタログ_ **.** _スキーマ_ **.** _テーブル_)、これは、結果セットで表されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**PKTABLE_CAT**|**sysname**|主キーが設定されたテーブルのカタログです。|  
|**PKTABLE_SCHEM**|**sysname**|主キーが設定されたテーブルのスキーマです。|  
|**PKTABLE_NAME**|**sysname**|(主キー) テーブルの名前です。 このフィールドは、常に値を返します。|  
|**PKCOLUMN_NAME**|**sysname**|各列の主キー列または列の名前、 **TABLE_NAME**が返されます。 このフィールドは、常に値を返します。|  
|**FKTABLE_CAT**|**sysname**|外部キーが設定されたテーブルのカタログです。|  
|**FKTABLE_SCHEM**|**sysname**|外部キーが設定されたテーブルのスキーマです。|  
|**FKTABLE_NAME**|**sysname**|外部キーが設定されたテーブルの名前です。 このフィールドは、常に値を返します。|  
|**FKCOLUMN_NAME**|**sysname**|TABLE_NAME の各列の外部キー列の名前が返されます。 このフィールドは、常に値を返します。|  
|**KEY_SEQ**|**smallint**|複数列の主キー列のシーケンス番号。 このフィールドは、常に値を返します。|  
|**UPDATE_RULE**|**smallint**|SQL 操作の更新時に、外部キーに適用される動作です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 0、1、またはこれらの列 2 を返します。<br /><br /> 0 = 外部キーに CASCADE 変更します。<br /><br /> 1 = 外部キーが存在する場合は NO ACTION の変更。<br /><br /> 2=SET_NULL: 外部キーを NULL に設定します。|  
|**DELETE_RULE**|**smallint**|SQL 操作の削除時に、外部キーに適用される動作です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 0、1、またはこれらの列 2 を返します。<br /><br /> 0 = 外部キーに CASCADE 変更します。<br /><br /> 1 = 外部キーが存在する場合は NO ACTION の変更。<br /><br /> 2=SET_NULL: 外部キーを NULL に設定します。|  
|**FK_NAME**|**sysname**|外部キーの識別子。 データ ソースに適用されない場合は NULL になります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、FOREIGN KEY 制約の名前を返します。|  
|**PK_NAME**|**sysname**|主キー識別子。 データ ソースに適用されない場合は NULL になります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 主キー制約の名前を返します。|  
|**遅延**|**smallint**|制約チェックを遅延可能にするかどうかを示します。|  
  
 結果セットの FK_NAME と pk_name の各列は常に NULL を返します。  
  
## <a name="remarks"></a>コメント  
 **sp_foreignkeys**の FOREIGN_KEYS 行セットのクエリ、 **IDBSchemaRowset**に対応する OLE DB プロバイダーのインターフェイス*table_server*します。 *Table_name*、 *、table_schema、* 、 *table_catalog*、および*列*行を制限するには、このインターフェイスに渡されるパラメーター返されます。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、外部キーの情報を返しますに関する、`Department`テーブルに、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 、リンク サーバー上のデータベース`Seattle1`します。  
  
```  
EXEC sp_foreignkeys @table_server = N'Seattle1',   
   @pktab_name = N'Department',   
   @pktab_catalog = N'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_catalogs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_primarykeys &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_tables_ex &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
