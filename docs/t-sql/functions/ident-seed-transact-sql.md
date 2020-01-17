---
title: IDENT_SEED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IDENT_SEED_TSQL
- IDENT_SEED
dev_langs:
- TSQL
helpviewer_keywords:
- identity columns [SQL Server], IDENT_SEED function
- seed values [SQL Server]
- IDENT_SEED function
ms.assetid: e4cb8eb8-affb-4810-a8a9-0110af3c247a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9685c68127b5370d007981a2f01e67f8d22df5da
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843690"
---
# <a name="ident_seed-transact-sql"></a>IDENT_SEED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  テーブルやビューでの ID 列の作成時に指定された元のシード値を返します。 DBCC CHECKIDENT を使用して ID 列の現在の値を変更しても、この関数で返される値は変更されません。  
  
 ![記事リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "記事リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
IDENT_SEED ( 'table_or_view' )  
```  
  
## <a name="arguments"></a>引数  
 **'** *table_or_view* **'**  
 ID シード値を確認するためのテーブルまたはビューを表す[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。 *されることはありません* 引用符、変数、関数の場合、または列名で囲まれた文字列定数を指定できます。 *table_or_view* は **char**、**nchar**、**varchar**、または **nvarchar**です。  
  
## <a name="return-types"></a>戻り値の型  
**numeric**([@@MAXPRECISION](../../t-sql/functions/max-precision-transact-sql.md),0))  
  
## <a name="exceptions"></a>例外  
 エラーが発生した場合、または呼び出し元にオブジェクトの表示権限がない場合は、NULL が返されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ユーザーは自身が所有している、または権限を与えられている、セキュリティ保護可能なアイテムのメタデータのみを表示できます。 このセキュリティは、オブジェクトに対する権限がユーザーに与えられていない場合、メタデータを生成する組み込み関数 (IDENT_SEED など) が NULL を返す可能性があることを意味します。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-the-seed-value-from-a-specified-table"></a>A. 指定したテーブルのシード値を返す  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベース内の `Person.Address` テーブルのシード値を返します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT IDENT_SEED('Person.Address') AS Identity_Seed;  
GO  
```  
  
### <a name="b-returning-the-seed-value-from-multiple-tables"></a>B. 複数のテーブルのシード値を返す  
 次の例では、シード値の ID 列を含む、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースのテーブルを返します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT TABLE_SCHEMA, TABLE_NAME,   
   IDENT_SEED(TABLE_SCHEMA + '.' + TABLE_NAME) AS IDENT_SEED  
FROM INFORMATION_SCHEMA.TABLES  
WHERE IDENT_SEED(TABLE_SCHEMA + '.' + TABLE_NAME) IS NOT NULL;  
GO  
```  
  
 次に結果セットの一部を示します。  
  
 ```
 TABLE_SCHEMA       TABLE_NAME                   IDENT_SEED  
------------       ---------------------------  -----------  
Person             Address                                1  
Production         ProductReview                          1  
Production         TransactionHistory                100000  
Person             AddressType                            1  
Production         ProductSubcategory                     1  
Person             vAdditionalContactInfo                 1  
dbo                AWBuildVersion                         1
```  
  
## <a name="see-also"></a>参照  
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [IDENT_INCR &#40;Transact-SQL&#41;](../../t-sql/functions/ident-incr-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [sys.identity_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-identity-columns-transact-sql.md)  
  
