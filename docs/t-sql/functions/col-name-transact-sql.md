---
title: COL_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COL_NAME
- COL_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column properties [SQL Server]
- COL_NAME function
- column names [SQL Server]
- names [SQL Server], columns
ms.assetid: 214144ab-f2bc-4052-83cf-caf0a85c4cc6
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 91e36569f32f75e5b5328974f0df870c7814f251
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064718"
---
# <a name="colname-transact-sql"></a>COL_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

この関数は、テーブルの ID 番号とそのテーブルの列の ID 番号に基づいて、テーブルの列の名前を返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
COL_NAME ( table_id , column_id )  
```  
  
## <a name="arguments"></a>引数  
*table_id*  
その列を含むテーブルの ID 番号。 *table_id* 引数は **int** データ型です。
  
*column_id*  
列の ID 番号。 *column_id* 引数は **int** データ型です。
  
## <a name="return-types"></a>戻り値の型
**sysname**
  
## <a name="exceptions"></a>例外  
エラーが発生した場合、または呼び出し元にオブジェクトを表示するための適切な権限がない場合は、NULL が返されます。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、そのユーザーが所有している、または権限を与えられている、セキュリティ保護可能なアイテムのメタデータのみを表示できます。 つまり、オブジェクトに対する適切な権限がユーザーに与えられていない場合、メタデータを生成する組み込み関数 (`COL_NAME` など) が NULL を返す可能性があります。 詳細については、「[メタデータ表示の構成](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。
  
## <a name="remarks"></a>Remarks  
*Table_id* と *column_id* パラメーターが同時に、列名文字列を生成します。
  
テーブルおよび列の ID 番号の取得の詳細については、「[OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)」を参照してください。
  
## <a name="examples"></a>使用例  
この例では、サンプルの `Employee` テーブル内の最初の列の名前を返します。
  
```sql
-- Uses AdventureWorks  
  
SELECT COL_NAME(OBJECT_ID('dbo.FactResellerSales'), 1) AS FirstColumnName,  
COL_NAME(OBJECT_ID('dbo.FactResellerSales'), 2) AS SecondColumnName;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
ColumnName          
------------   
BusinessEntityID  
```  
  
## <a name="see-also"></a>参照
[式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)  
[COL_LENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/col-length-transact-sql.md)
  
  

