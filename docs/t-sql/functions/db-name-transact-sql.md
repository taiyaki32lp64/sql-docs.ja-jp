---
title: DB_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DB_NAME
- DB_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database names [SQL Server], DB_NAME
- names [SQL Server], databases
- viewing database names
- displaying database names
- DB_NAME function
ms.assetid: e21fb33a-a3ea-49b0-bb6b-8f789a675a0e
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5aa5e2a60189a82fb60cd416b7f87b35824e236f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118977"
---
# <a name="dbname-transact-sql"></a>DB_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

この関数は、指定されたデータベースの名前を返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DB_NAME ( [ database_id ] )  
```  
  
## <a name="arguments"></a>引数  
*database_id*  

名前 `DB_NAME` が返されるデータベースの識別番号 (ID) です。 `DB_NAME` の呼び出しで *database_id* が省略された場合、`DB_NAME` は現在のデータベースの名前を返します。
  
## <a name="return-types"></a>戻り値の型
**nvarchar(128)**
  
## <a name="permissions"></a>アクセス許可  

`DB_NAME` の呼び出し元が、**マスター**以外または **tempdb** 以外の特定データベースを所有していない場合は、対応する `DB_ID` 行を確認するために、少なくとも、サーバー レベルの `ALTER ANY DATABASE` または `VIEW ANY DATABASE` 権限が必要です。 **マスター** データベースの場合、`DB_ID` には少なくとも `CREATE DATABASE` 権限が必要です。 呼び出し元が接続するデータベースは常に、**sys.databases** 内で確認できます。
  
> [!IMPORTANT]  
>  既定では、public ロールは、すべてのログインにデータベース情報の表示を許可する `VIEW ANY DATABASE` 権限を持っています。 ログインでデータベースが検出されるのを阻止するには、public から `VIEW ANY DATABASE` を `REVOKE` するか、または、個別のログインに対する `VIEW ANY DATABASE` を `DENY` します。
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-the-current-database-name"></a>A. 現在のデータベース名を返す  
この例では、現在のデータベース名を返します。
  
```sql
SELECT DB_NAME() AS [Current Database];  
GO  
```  
  
### <a name="b-returning-the-database-name-of-a-specified-database-id"></a>B. 指定したデータベース ID のデータベース名を返す  
この例では、データベース ID `3` のデータベース名を返します。
  
```sql
USE master;  
GO  
SELECT DB_NAME(3)AS [Database Name];  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-return-the-current-database-name"></a>C. 現在のデータベース名を取得する  
  
```sql
SELECT DB_NAME() AS [Current Database];  
```  
  
### <a name="d-return-the-name-of-a-database-by-using-the-database-id"></a>D. データベース ID を使用してデータベースの名前を返す  
次の例では、各データベースのデータベース名と database_id を返します。
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>参照
[DB_ID &#40;Transact-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)  
[メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  

