---
title: sp_fulltext_column (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_column_TSQL
- sp_fulltext_column
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_column
ms.assetid: a84cc45d-1b50-44af-85df-2ea033b8a6a9
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9e17a87a04c8c4286a66c6e7a0746f2d7de48d72
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124338"
---
# <a name="spfulltextcolumn-transact-sql"></a>sp_fulltext_column (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  テーブルの特定の列がフルテキスト インデックスに参加するかどうかを指定します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_fulltext_column [ @tabname= ] 'qualified_table_name' ,   
     [ @colname= ] 'column_name' ,   
     [ @action= ] 'action'   
     [ , [ @language= ] 'language_term' ]   
     [ , [ @type_colname= ] 'type_column_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @tabname = ] 'qualified_table_name'` 1 つまたは 2 つの部分のテーブル名です。 テーブルは、現在のデータベース内に存在している必要があります。 テーブルにフルテキスト インデックスがある。 *qualified_table_name*は**nvarchar (517)** 既定値はありません。  
  
`[ @colname = ] 'column_name'` 内の列の名前を指定*qualified_table_name*します。 列は、いずれかの文字である必要があります**varbinary (max)** または**イメージ**列、計算列にすることはできません。 *column_name*は**sysname**、既定値はありません。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列に格納されているテキスト データのフルテキスト インデックスを作成できます**varbinary (max)** または**イメージ**データ型。 画像と画像はインデックス作成されません。  
  
`[ @action = ] 'action'` 実行する操作です。 *アクション*は**varchar (20)** , で、なし、既定値は、次の値のいずれかを指定します。  
  
|値|説明|  
|-----------|-----------------|  
|**add**|追加*column_name*の*qualified_table_name*テーブルの非アクティブなフルテキスト インデックスにします。 これにより、フルテキスト インデックスの列。|  
|**drop**|削除*column_name*の*qualified_table_name*テーブルの非アクティブなフルテキスト インデックスから。|  
  
`[ @language = ] 'language_term'` 列に格納されたデータの言語です。 含まれる言語の一覧については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[sys.fulltext_languages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)します。  
  
> [!NOTE]  
>  列には、複数の言語またはサポートされていない言語でのデータが含まれている場合は、'ニュートラル' を使用します。 既定値は、構成オプション '既定のフルテキスト言語' によって指定されます。  
  
`[ @type_colname = ] 'type_column_name'` 内の列の名前を指定*qualified_table_name*のドキュメントの種類を保持している*column_name*します。 この列である必要があります**char**、 **nchar**、 **varchar**、または**nvarchar**します。 データ型の場合にのみ使用される*column_name*の種類は**varbinary (max)** または**イメージ**します。 *type_column_name*は**sysname**、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 フルテキスト インデックスがアクティブで、実行中の作成は停止します。 また、アクティブなフルテキスト インデックスを持つテーブルで変更の追跡が有効になっている場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では現在のインデックスが維持されます。 たとえば [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、あるテーブルに対して現在行われているインデックス作成がすべて停止され、既存のインデックスの削除、および新しいインデックスの作成が開始されます。  
  
 変更の追跡が、列を追加またはインデックスを保持するには、テーブルを非アクティブであり、必要な列を追加または削除する必要があります、フルテキスト インデックスから削除する必要がある場合。 この操作では、インデックスは変化しません。 テーブルは実用的では作成を開始するときに、後でアクティブにできます。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーのメンバーである必要があります、 **db_ddladmin**固定データベース ロール、またはのメンバー、 **db_owner**固定データベース ロール、またはテーブルの所有者。  
  
## <a name="examples"></a>使用例  
 次の例では、`DocumentSummary` テーブルの `Document` 列を、テーブルのフルテキスト インデックスに追加します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_column 'Production.Document', DocumentSummary, 'add';  
GO  
```  
  
 次の例では、`spanishTbl` というテーブルにフルテキスト インデックスが作成されていることを前提としています。 追加する、`spanishCol`フルテキスト インデックス列は、次のストアド プロシージャを実行します。  
  
```  
EXEC sp_fulltext_column 'spanishTbl', 'spanishCol', 'add', 0xC0A;  
GO  
```  
  
 このクエリを実行するとします。  
  
```  
SELECT *   
FROM spanishTbl   
WHERE CONTAINS(spanishCol, 'formsof(inflectional, trabajar)')  
```  
  
 結果セットには異なる形式の行が含まれます`trabajar`に (機能) するなど`trabajo`、 `trabajamos`、および`trabajan`します。  
  
> [!NOTE]  
>  1 つのフルテキスト クエリ関数句で示されているすべての列には、同じ言語を使用する必要があります。  
  
## <a name="see-also"></a>関連項目  
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [照会する&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)   
 [sp_help_fulltext_columns_cursor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [sp_help_fulltext_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [フルテキスト検索およびセマンティック検索ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
