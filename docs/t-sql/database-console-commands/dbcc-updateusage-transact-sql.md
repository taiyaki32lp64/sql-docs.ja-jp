---
title: DBCC UPDATEUSAGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UPDATEUSAGE
- UPDATEUSAGE_TSQL
- DBCC_UPDATEUSAGE_TSQL
- DBCC UPDATEUSAGE
dev_langs:
- TSQL
helpviewer_keywords:
- inaccurate page or row counts [SQL Server]
- space [SQL Server], usage reports
- updating space usage information
- updating row counts
- disk space [SQL Server], inaccurate counts
- counting pages
- reporting count inaccuracies
- updating page counts
- synchronization [SQL Server], inaccurate counts
- incorrect space usage reports [SQL Server]
- DBCC UPDATEUSAGE statement
- integrity [SQL Server], database objects
- counting rows
- row count accuracy [SQL Server]
- page count accuracy [SQL Server]
ms.assetid: b8752ecc-db45-4e23-aee7-13b8bc3cbae2
author: pmasl
ms.author: umajay
ms.openlocfilehash: 7d983f2e7e370ec9fe385e6d46602c4703ca6d1e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040466"
---
# <a name="dbcc-updateusage-transact-sql"></a>DBCC UPDATEUSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

カタログ ビューのページと行数の情報に不一致がある場合、それらをレポートおよび修正します。 情報に不一致があると、sp_spaceused システム ストアド プロシージャによって間違った領域使用状況レポートが返される原因となります。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DBCC UPDATEUSAGE   
(   { database_name | database_id | 0 }   
    [ , { table_name | table_id | view_name | view_id }   
    [ , { index_name | index_id } ] ]   
) [ WITH [ NO_INFOMSGS ] [ , ] [ COUNT_ROWS ] ]   
```  
  
## <a name="arguments"></a>引数  
*database_name* | *database_id* | 0  
領域使用状況の統計をレポートおよび修正するデータベースの名前または ID を指定します。 0 を指定すると、現在のデータベースが選択されます。 データベース名は、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。  
  
*table_name* | *table_id* | *view_name* | *view_id*  
領域使用状況の統計をレポートおよび修正するテーブルやインデックス付きビューの名前または ID を指定します。 テーブル名とビュー名は、識別子の規則に従っている必要があります。  
  
*index_id* | *index_name*  
使用するインデックスの ID または名前を指定します。 これらを指定しない場合、ステートメントでは指定したテーブルまたはビューのすべてのインデックスが処理されます。  
  
WITH  
オプションの指定を許可します。  
  
NO_INFOMSGS  
すべての情報メッセージを表示しないようにします。  
  
COUNT_ROWS  
row count 列に、テーブルまたはビューの現在の行数カウントを反映します。  
  
## <a name="remarks"></a>Remarks  
DBCC UPDATEUSAGE では、テーブルまたはインデックスのパーティションごとに、行、使用済みページ、予約済みページ、リーフ ページ、およびデータ ページのカウントが修正されます。 システム テーブルに情報の不一致がない場合、DBCC UPDATEUSAGE ではデータは返されません。 情報の不一致が検出および修正され、WITH NO_INFOMSGS が使用されていない場合、DBCC UPDATEUSAGE ではシステム テーブル内の更新された行と列が返されます。
  
DBCC CHECKDB が強化され、ページや行のカウントが負になったことを検出します。 この問題が検出されると、DBCC CHECKDB の出力に警告が表示され、推奨される解決方法として DBCC UPDATEUSAGE を実行するよう示されます。
  
## <a name="best-practices"></a>ベスト プラクティス  
次をお勧めします。
-   DBCC UPDATEUSAGE を定期的に実行しないでください。 DBCC UPDATEUSAGE は、大規模なテーブルやデータベースで実行すると時間がかかるため、sp_spaceused で返される値が正しくないと思われる場合以外は使用しないようにします。
-   データベースでデータ定義言語 (DDL) の変更 (CREATE、ALTER、DROP などのステートメント) が頻繁に実行されている場合に限り、DBCC UPDATEUSAGE を定期的 (毎週など) に実行することを検討します。  
  
## <a name="result-sets"></a>結果セット  
DBCC UPDATEUSAGE では次の情報が返されます (値は変わることがあります)。
  
`DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
## <a name="permissions"></a>アクセス許可  
**sysadmin** 固定サーバー ロールまたは **db_owner** 固定データベース ロールのメンバーシップが必要です。
  
## <a name="examples"></a>使用例  
  
### <a name="a-updating-page-or-row-counts-or-both-for-all-objects-in-the-current-database"></a>A. 現在のデータベースのすべてのオブジェクトに対し、ページ数または行数、あるいはその両方を更新する  
次の例では、データベース名に `0` を指定し、`DBCC UPDATEUSAGE` で現在のデータベースに対する更新されたページ数または行数をレポートします。
  
```sql
DBCC UPDATEUSAGE (0);  
GO  
```  
  
### <a name="b-updating-page-or-row-counts-or-both-for-adventureworks-and-suppressing-informational-messages"></a>B. AdventureWorks に対してページ数または行数、あるいはその両方を更新し、情報メッセージを表示しない  
次の例では、データベース名に [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] を指定し、すべての情報メッセージを表示しないよう指定します。
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012) WITH NO_INFOMSGS;   
GO  
```  
  
### <a name="c-updating-page-or-row-counts-or-both-for-the-employee-table"></a>C. Employee テーブルに対してページ数または行数、あるいはその両方を更新する  
次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの `Employee` テーブルに関して、更新されたページ数または行数をレポートします。
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012,'HumanResources.Employee');  
GO  
```  
  
### <a name="d-updating-page-or-row-counts-or-both-for-a-specific-index-in-a-table"></a>D. テーブル内の特定のインデックスに対してページ数または行数、あるいはその両方を更新する  
 次の例では、インデックス名に `IX_Employee_ManagerID` を指定します。  
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012, 'HumanResources.Employee', IX_Employee_OrganizationLevel_OrganizationNode);  
GO  
```  
  
## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)  
[UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)
  
  
