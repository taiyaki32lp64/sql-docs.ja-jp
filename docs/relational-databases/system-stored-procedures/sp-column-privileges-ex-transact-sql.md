---
title: sp_column_privileges_ex (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_ex
- sp_column_privileges_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_column_privileges_ex
ms.assetid: 98cb6e58-4007-40fc-b048-449fb2e7e6be
author: stevestein
ms.author: sstein
ms.openlocfilehash: cd4251c4b47f67d348b6978c05c07d0ae64d16c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070357"
---
# <a name="spcolumnprivilegesex-transact-sql"></a>sp_column_privileges_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定されたリンク サーバー上の指定されたテーブルの列の特権を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_column_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @table_server = ] 'table_server'` 情報を返すリンク サーバーの名前です。 *table_server*は**sysname**、既定値はありません。  
  
`[ @table_name = ] 'table_name'` 指定された列を含んでいるテーブルの名前です。 *table_name*は**sysname**、既定値は NULL です。  
  
`[ @table_schema = ] 'table_schema'` テーブル スキーマを示します。 *table_schema、* は**sysname**、既定値は NULL です。  
  
`[ @table_catalog = ] 'table_catalog'` データベースの名前は、指定した*table_name*が存在します。 *table_catalog*は**sysname**、既定値は NULL です。  
  
`[ @column_name = ] 'column_name'` 特権情報を提供する対象の列の名前です。 *column_name*は**sysname**、既定値は null です (すべて共通)。  
  
## <a name="result-sets"></a>結果セット  
 次の表は結果セットの列を示しています。 返される結果は並べ**TABLE_QUALIFIER**、 **TABLE_OWNER**、 **TABLE_NAME**、 **COLUMN_NAME**、および**特権**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|テーブル修飾子の名前。 さまざまな DBMS 製品は、3 つの部分がテーブルの名前付けをサポート (_修飾子_ **.** _所有者_ **.** _名前_)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、この列は、データベース名を表します。 一部の製品で、テーブルのデータベース環境のサーバー名を表します。 このフィールドは NULL を指定できます。|  
|**TABLE_SCHEM**|**sysname**|テーブルの所有者名です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、この列は、テーブルを作成したデータベース ユーザーの名前を表します。 このフィールドは、常に値を返します。|  
|**TABLE_NAME**|**sysname**|テーブル名です。 このフィールドは、常に値を返します。|  
|**COLUMN_NAME**|**sysname**|各列の列名、 **TABLE_NAME**が返されます。 このフィールドは、常に値を返します。|  
|**権限の許可者**|**sysname**|このアクセス許可が付与されるデータベース ユーザー名**COLUMN_NAME**を表示される**権限付与対象ユーザー**します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、この列が同じでは常に、 **TABLE_OWNER**します。 このフィールドは、常に値を返します。<br /><br /> **GRANTOR**列は、データベース所有者を指定できます (**TABLE_OWNER**) または他のユーザーに、データベース所有者が GRANT ステートメントで WITH GRANT OPTION 句を使用して、アクセス許可を許可します。|  
|**権限付与対象ユーザー**|**sysname**|このアクセス許可が与えられているデータベース ユーザー名**COLUMN_NAME**により**GRANTOR**します。 このフィールドは、常に値を返します。|  
|**特権**|**varchar(** 32 **)**|使用可能な列のアクセス許可の 1 つ。 列権限には、次の値 (または実装が定義されているときに、データ ソースでサポートされるその他の値) のいずれかを指定できます。<br /><br /> 選択 =**権限付与対象ユーザー**列のデータを取得できます。<br /><br /> 挿入 =**権限付与対象ユーザー**新しい行が挿入されたときに、この列のデータを提供できます (によって、**権限付与対象ユーザー**) テーブルにします。<br /><br /> 更新 =**権限付与対象ユーザー**列内の既存のデータを変更することができます。<br /><br /> 参照 =**権限付与対象ユーザー**主キー/外部キーのリレーションシップで外部テーブルで列を参照できます。 テーブルの制約と主キー/外部キーのリレーションシップが定義されます。|  
|**IS_GRANTABLE**|**varchar(** 3 **)**|示すかどうか、**権限付与対象ユーザー**で許可されている他のユーザー (「許可の許可」とも呼ばれます) にアクセス許可を付与します。 いいえ、はい、できますまたは NULL。 不明な値 (つまり NULL) は、"許可の許可" 権限が適用されないデータ ソースを示します。|  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、`HumanResources.Department` リンク サーバーにある [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの `Seattle1` テーブルの列特権情報を返します。  
  
```  
EXEC sp_column_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Department',   
   @table_schema = 'HumanResources',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_table_privileges_ex &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-ex-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
