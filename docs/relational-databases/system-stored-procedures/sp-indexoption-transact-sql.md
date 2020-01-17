---
title: sp_indexoption (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_indexoption
- sp_indexoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_indexoption
ms.assetid: 75f836be-d322-4a53-a45d-25bee6b42a52
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6d1231b4411e11de65cfe99d209ed231db79b5db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030910"
---
# <a name="spindexoption-transact-sql"></a>sp_indexoption (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ロックのユーザー定義のクラスター化および非クラスター化インデックスまたはクラスター化インデックスのテーブルのオプションの値を設定しません。  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]は、ページレベル、行レベル、またはテーブルレベルのロックを自動的に選択します。 これらのオプションを手動で設定する必要はありません。 **sp_indexoption**のために、特定の種類のロックは常に確実に理解している上級ユーザーに適切な提供されます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)] 代わりに、 [ALTER INDEX &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_indexoption [ @IndexNamePattern = ] 'table_or_index_name'   
    , [ @OptionName = ] 'option_name'   
    , [ @OptionValue = ] 'value'  
```  
  
## <a name="arguments"></a>引数  
`[ @IndexNamePattern = ] 'table_or_index_name'` ユーザー定義テーブルまたはインデックスの修飾付きまたは修飾なしの名前です。 *table_or_index_name*は**nvarchar (1035)** 、既定値はありません。 引用符は、インデックスまたはテーブルの修飾名が指定されている場合にのみ必要です。 データベース名も含めてフル パスで指定した場合は、そのデータベース名は現在のデータベース名である必要があります。 インデックスのないテーブル名を指定すると場合、指定したオプションの値でクラスター化インデックスが存在しない場合のテーブルとテーブル自体の設定のすべてのインデックスされます。  
  
`[ @OptionName = ] 'option_name'` インデックスのオプション名です。 *option_name*は**varchar (35)** 、既定値はありません。 *option_name*値は次のいずれかであることができます。  
  
|値|説明|  
|-----------|-----------------|  
|**AllowRowLocks**|TRUE の場合、インデックスへのアクセス時に行ロックが許可されます。 いつ行ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって決定されます。 FALSE の場合、行ロックは使用されません。 既定では TRUE です。|  
|**AllowPageLocks**|TRUE の場合、インデックスにアクセスするときにページ ロックが許可されます。 いつページ ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)] によって決定されます。 FALSE の場合、ページ ロックは使用されません。 既定では TRUE です。|  
|**DisAllowRowLocks**|TRUE の場合、行ロックは使用されません。 FALSE の場合、インデックスにアクセスするときに行ロックが許可されます。 いつ行ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって決定されます。|  
|**DisAllowPageLocks**|TRUE の場合、ページ ロックは使用されません。 FALSE の場合、インデックスへのアクセス時にページ ロックが許可されます。 いつページ ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)] によって決定されます。|  
  
`[ @OptionValue = ] 'value'` 指定するかどうか、 *option_name*設定が有効になっている (TRUE、ON、はい、または 1) か無効 (FALSE、OFF、いいえ、または 0)。 *値*は**varchar (12)** 、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 0 (失敗) より大きい  
  
## <a name="remarks"></a>コメント  
 XML インデックスはサポートされていません。 XML インデックスを指定すると、またはテーブル名をインデックス名なしで指定して、テーブルに XML インデックスが含まれています、ステートメントが失敗します。 これらのオプションを設定する[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)代わりにします。  
  
 現在の行とページ ロックのプロパティを表示する使用[INDEXPROPERTY](../../t-sql/functions/indexproperty-transact-sql.md)または[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)カタログ ビューです。  
  
-   インデックスへのアクセス時に行、ページ、およびテーブル レベルのロックが許可されるときに**AllowRowLocks** = TRUE または**DisAllowRowLocks** = FALSE、および**AllowPageLocks** = TRUE"または" **DisAllowPageLocks** = FALSE。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]は適切なロックを選択し、行ロックまたはページ ロックをテーブル ロックにエスカレートすることができます。  
  
 インデックスにアクセスするときにテーブル レベルのロックのみが許可されているときに**AllowRowLocks** = FALSE または**DisAllowRowLocks** = TRUE と**AllowPageLocks** = FALSE または**DisAllowPageLocks** = TRUE。  
  
 テーブル名をインデックスなしで指定すると、設定はそのテーブルのすべてのインデックスに適用されます。 基になるテーブルにクラスター化インデックスがない (つまりヒープである) 場合、設定は次のように適用されます。  
  
-   ときに**AllowRowLocks**または**DisAllowRowLocks**は TRUE または FALSE に設定すると、設定が、ヒープに適用され、関連するすべての非クラスター化インデックス。  
  
-   ときに**AllowPageLocks**オプションが TRUE に設定または**DisAllowPageLocks**設定が FALSE に設定が、ヒープに適用され、関連するすべての非クラスター化インデックス。  
  
-   ときに**AllowPageLocks**オプションが FALSE に設定または**DisAllowPageLocks**が TRUE に設定、設定は、完全に非クラスター化インデックスにします。 つまり、非クラスター化インデックスのすべてのページ ロックが許可されていません。 ヒープで許可されないのは、ページに対する共有 (S)、更新 (U)、および排他 (X) ロックのみです。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]では内部目的用にインテント ページ ロック (IS、IU、または IX) を引き続き取得できます。  
  
## <a name="permissions"></a>アクセス許可  
 テーブルに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-setting-an-option-on-a-specific-index"></a>A. 特定のインデックスに対してオプションを設定  
 次の例でページ ロックが許可されていません、`IX_Customer_TerritoryID`のインデックス、`Customer`テーブル。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_indexoption N'Sales.Customer.IX_Customer_TerritoryID',  
    N'disallowpagelocks', TRUE;  
```  
  
### <a name="b-setting-an-option-on-all-indexes-on-a-table"></a>B. テーブルのすべてのインデックスに対してオプションを設定する  
 次の例には、行ロックに関連付けられているすべてのインデックスが許可されていません、`Product`テーブル。 `sys.indexes` プロシージャの実行前と後に `sp_indexoption` カタログ ビューに対するクエリを実行して、ステートメントの結果を表示します。  
  
```sql  
USE AdventureWorks2012;  
GO  
--Display the current row and page lock options for all indexes on the table.  
SELECT name, type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE object_id = OBJECT_ID(N'Production.Product');  
GO  
-- Set the disallowrowlocks option on the Product table.   
EXEC sp_indexoption N'Production.Product',  
    N'disallowrowlocks', TRUE;  
GO  
--Verify the row and page lock options for all indexes on the table.  
SELECT name, type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE object_id = OBJECT_ID(N'Production.Product');  
GO  
```  
  
### <a name="c-setting-an-option-on-a-table-with-no-clustered-index"></a>C. クラスター化インデックスのないテーブルに対してオプションを設定する  
 次の例では、クラスター化インデックスを持たないテーブル (ヒープ) について、ページ ロックを許可していません。 `sys.indexes`カタログ ビューのクエリが実行前に、と後、`sp_indexoption`ステートメントの結果を表示するプロシージャを実行します。  
  
```sql  
USE AdventureWorks2012;  
GO  
--Display the current row and page lock options of the table.   
SELECT OBJECT_NAME (object_id) AS [Table], type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE OBJECT_NAME (object_id) = N'DatabaseLog';  
GO  
-- Set the disallowpagelocks option on the table.   
EXEC sp_indexoption DatabaseLog,  
    N'disallowpagelocks', TRUE;  
GO  
--Verify the row and page lock settings of the table.  
SELECT OBJECT_NAME (object_id) AS [Table], allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE OBJECT_NAME (object_id) = N'DatabaseLog';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
