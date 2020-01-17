---
title: sp_tables (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_tables
- sp_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tables
ms.assetid: 787a2fa5-87a1-49bd-938b-6043c245f46b
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 71aaa9e52cfca8435501695a4ebf60b2a6aa6ee4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096052"
---
# <a name="sptables-transact-sql"></a>sp_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  現在の環境でクエリを実行できるオブジェクトの一覧を返します。 これは、任意のテーブルまたはビュー、シノニム オブジェクトを除くことを意味します。  
  
> [!NOTE]  
>  シノニムのベース オブジェクトの名前を確認するのには、クエリ、 [sys.synonyms](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md)カタログ ビューです。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_tables [ [ @table_name = ] 'name' ]   
     [ , [ @table_owner = ] 'owner' ]   
     [ , [ @table_qualifier = ] 'qualifier' ]   
     [ , [ @table_type = ] "type" ]   
     [ , [@fUsePattern = ] 'fUsePattern'];  
```  
  
## <a name="arguments"></a>引数  
`[ @table_name = ] 'name'` カタログ情報を返すために使用するテーブル。 *名前*は**nvarchar (384)** 、既定値は NULL です。 ワイルドカードによるパターン照合はサポートされています。  
  
`[ @table_owner = ] 'owner'` カタログ情報を返すために使用するテーブルのテーブル所有者です。 *所有者*は**nvarchar (384)** 、既定値は NULL です。 ワイルドカードによるパターン照合はサポートされています。 所有者が指定されていない場合は、基になる DBMS の既定のテーブル可視性規則が適用されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、現在のユーザーが指定した名前のテーブルを所有している場合、そのテーブルの列が返されます。 所有者が指定されていない、現在のユーザーが指定した名前のテーブルを所有していない場合は、この手順は、データベースの所有者によって所有されている指定した名前のテーブルを探します。 そのテーブルが存在する場合、そのテーブルの列が返されます。  
  
`[ @table_qualifier = ] 'qualifier'` テーブル修飾子の名前です。 *修飾子*は**sysname**、既定値は NULL です。 さまざまな DBMS 製品は、3 つの部分がテーブルの名前付けをサポート (_修飾子_ **.** _所有者_ **.** _名前_)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、この列は、データベース名を表します。 一部の製品で、テーブルのデータベース環境のサーバー名を表します。  
  
``[ , [ @table_type = ] "'type', 'type'" ]`` 指定されているテーブルの種類のすべてのテーブルに関する情報をコンマで区切って、値の一覧を示します。 以下の**テーブル**、 **SYSTEMTABLE**、および**ビュー**します。 *型*は**varchar (100)** 、既定値は NULL です。  
  
> [!NOTE]  
>  各テーブル型を囲む必要があります単一引用符と二重引用符は、パラメーター全体を囲む必要があります。 テーブル型は、大文字である必要があります。 SET QUOTED_IDENTIFIER が ON の場合は、それぞれ単一引用符が 2 倍にする必要があり、パラメーター全体を単一引用符で囲む必要があります。  
  
`[ @fUsePattern = ] 'fUsePattern'` アンダー スコア (_)、パーセント (%) と角かっこ ([または]) の文字がワイルドカードとして解釈されるかどうかを判断します。 有効な値は 0 (パターン一致がオフ) および 1 (パターン一致では)。 *fUsePattern*は**ビット**、既定値は 1 です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|テーブル修飾子の名前。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、この列は、データベース名を表します。 このフィールドは NULL を指定できます。|  
|**TABLE_OWNER**|**sysname**|テーブルの所有者名です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、この列は、テーブルを作成したデータベース ユーザーの名前を表します。 このフィールドは、常に値を返します。|  
|**TABLE_NAME**|**sysname**|テーブル名です。 このフィールドは、常に値を返します。|  
|**TABLE_TYPE**|**varchar(32)**|テーブル、システム テーブルまたはビュー。|  
|**「解説」**|**varchar(254)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] この列の値は返されません。|  
  
## <a name="remarks"></a>コメント  
 相互運用性を最大に、ゲートウェイのクライアントは、92 標準 SQL のパターン照合 (% と _ ワイルドカード文字) のみを想定してください。  
  
 現在のユーザーの読み取りまたは書き込みアクセスを特定のテーブルに関する特権情報は、常にチェックされません。 そのためのアクセスは保証されません。 この結果セットには、だけでなくテーブル、ビューがもシノニム、およびそれらの型をサポートする DBMS 製品へのゲートウェイのエイリアスが含まれています。 場合、サーバー属性**ACCESSIBLE_TABLES**での結果セットが Y **sp_server_info**、現在のユーザーがアクセスできるテーブルのみが返されます。  
  
 **sp_tables**と等価**SQLTables** ODBC にします。 返される結果は並べ**TABLE_TYPE**、 **TABLE_QUALIFIER**、 **TABLE_OWNER**、および**TABLE_NAME**します。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-a-list-of-objects-that-can-be-queried-in-the-current-environment"></a>A. 現在の環境でクエリされるオブジェクトの一覧を返す  
 次の例では、現在の環境でクエリできるオブジェクトの一覧を返します。  
  
```  
EXEC sp_tables ;  
```  
  
### <a name="b-returning-information-about-the-tables-in-a-specified-schema"></a>B. 指定したスキーマ内のテーブルに関する情報を返す  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベース内の `Person` スキーマに属するテーブルに関する情報が返されます。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_tables   
   @table_name = '%',  
   @table_owner = 'Person',  
   @table_qualifier = 'AdventureWorks2012';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-a-list-of-objects-that-can-be-queried-in-the-current-environment"></a>C. 現在の環境でクエリされるオブジェクトの一覧を返す  
 次の例では、現在の環境でクエリできるオブジェクトの一覧を返します。  
  
```  
EXEC sp_tables ;  
```  
  
### <a name="d-returning-information-about-the-tables-in-a-specified-schema"></a>D. 指定したスキーマ内のテーブルに関する情報を返す  
 次の例は、ディメンション テーブルに情報を返します、`AdventureWorksPDW201`データベース。  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_tables   
   @table_name = 'Dim%',  
   @table_owner = 'dbo',  
   @table_qualifier = 'AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>関連項目  
 [sys.synonyms &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

