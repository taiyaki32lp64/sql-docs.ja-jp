---
title: "外部テーブルを削除 (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 02a6a236-0756-4570-abfa-6f677a7df042
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0e560c5341abd440f641a988751a6ca2875b9bbb
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="drop-external-table-transact-sql"></a>外部テーブル (TRANSACT-SQL) を削除します。
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  PolyBase 外部テーブルを削除します。 これには、外部のデータは削除されません。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
DROP EXTERNAL TABLE [ database_name . [schema_name ] . | schema_name . ] table_name   
[;]  
```  
  

## <a name="arguments"></a>引数  
 [ *database_name*です。 [*schema_name*] です。 | *schema_name*です。 *table_name*  
 削除する外部テーブルの 1 つか 3 部構成の名前。 テーブル名は、スキーマ、または、データベースとスキーマ オプションで含めることができます。  
  
## <a name="permissions"></a>Permissions  
  
-   必要があります**ALTER**テーブルが所属するスキーマに対する権限。  
  
## <a name="general-remarks"></a>全般的な解説  
 外部のテーブルを削除するには、すべてのテーブルに関連するメタデータを削除します。 外部のデータは削除されません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-basic-syntax"></a>A. 基本的な構文を使用します。  
  
```  
DROP EXTERNAL TABLE SalesPerson;  
DROP EXTERNAL TABLE dbo.SalesPerson;  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
### <a name="b-dropping-an-external-table-from-the-current-database"></a>B. 現在のデータベースから、外部テーブルを削除します。  
 次の例では、削除、`ProductVendor1`テーブル、そのデータ、インデックス、および現在のデータベースからすべての従属ビューです。  
  
```  
DROP EXTERNAL TABLE ProductVendor1;  
```  
  
### <a name="c-dropping-a-table-from-another-database"></a>C. 別のデータベースからテーブルを削除します。  
 次の例では、`EasternDivision` データベースにある `SalesPerson` テーブルを削除します。  
  
```  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]と[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-basic-syntax"></a>D. 基本的な構文を使用します。  
  
```  
DROP EXTERNAL TABLE SalesPerson;  
DROP EXTERNAL TABLE dbo.SalesPerson;  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
### <a name="e-dropping-an-external-table-from-the-current-database"></a>E. 現在のデータベースから、外部テーブルを削除します。  
 次の例では、削除、`ProductVendor1`テーブル、そのデータ、インデックス、および現在のデータベースからすべての従属ビューです。  
  
```  
DROP EXTERNAL TABLE ProductVendor1;  
```  
  
### <a name="f-dropping-a-table-from-another-database"></a>F. 別のデータベースからテーブルを削除します。  
 次の例では、`EasternDivision` データベースにある `SalesPerson` テーブルを削除します。  
  
```  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
## <a name="see-also"></a>参照  
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  

