---
title: sp_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/17/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_columns_TSQL
- sp_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sp_columns
ms.assetid: 2dec79cf-2baf-4c0f-8cbb-afb1a8654e1e
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8eb18a81ff7910418e5b3c8a3b36a0e4cd94cc36
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070355"
---
# <a name="spcolumns-transact-sql"></a>sp_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  現在の環境でクエリを実行できる、指定したオブジェクトの列情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_columns [ @table_name = ] object  
     [ , [ @table_owner = ] owner ]   
     [ , [ @table_qualifier = ] qualifier ]   
     [ , [ @column_name = ] column ]   
     [ , [ @ODBCVer = ] ODBCVer ]  
```  
  
## <a name="arguments"></a>引数  
`[ \@table_name = ] object` カタログ情報を返すために使用するオブジェクトの名前です。 *オブジェクト*テーブル、ビュー、またはテーブル値関数などの列を持つその他のオブジェクトにすることができます。 *オブジェクト*は**nvarchar (384)** 、既定値はありません。 ワイルドカードによるパターン照合はサポートされています。  
  
`[ \@table_owner = ] owner` カタログ情報を返すために使用するオブジェクトのオブジェクトの所有者です。 *所有者*は**nvarchar (384)** 、既定値は NULL です。 ワイルドカードによるパターン照合はサポートされています。 場合*所有者*が指定されていない、基になる DBMS の既定のオブジェクトの可視性規則が適用されます。  
  
 指定した名前のオブジェクトを現在のユーザーが所有している場合は、そのオブジェクトの列が返されます。 場合*所有者*が指定されていない、現在のユーザーが指定したオブジェクトを所有していない*オブジェクト*、 **sp_columns**は、指定したオブジェクトを検索*オブジェクト*データベース所有者が所有します。 存在する場合は、そのオブジェクトの列が返されます。  
  
`[ \@table_qualifier = ] qualifier` オブジェクト修飾子の名前です。 *修飾子*は**sysname**、既定値は NULL です。 さまざまな DBMS 製品で、3 つの部分名オブジェクト (_修飾子_ **.** _所有者_ **.** _名前_)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、この列は、データベース名を表します。 一部の製品で、オブジェクトのデータベース環境のサーバー名を表します。  
  
`[ \@column_name = ] column` 1 つの列は、カタログ情報の 1 つだけの列が必要なときに使用されます。 *列*は**nvarchar (384)** 、既定値は NULL です。 場合*列*が指定されていないすべての列が返されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、*列*に表示される列の名前を表します、 **syscolumns**テーブル。 ワイルドカードによるパターン照合はサポートされています。 相互運用性を最大に、ゲートウェイのクライアントは、sql-92 標準のパターン照合 (% と _ ワイルドカード文字) のみを想定してください。  
  
`[ \@ODBCVer = ] ODBCVer` 使用されている ODBC のバージョンです。 *ODBCVer*は**int**、既定値は 2 です。 これは、ODBC のバージョン 2 を示します。 有効な値は、2 または 3 です。 バージョン 2 および 3 の間で動作の違いは、ODBC を参照してください。 **SQLColumns**仕様。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
 **Sp_columns**カタログ ストアド プロシージャは等価**SQLColumns** ODBC にします。 返される結果は並べ**TABLE_QUALIFIER**、 **TABLE_OWNER**、および**TABLE_NAME**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|オブジェクト修飾子の名前です。 このフィールドは NULL を指定できます。|  
|**TABLE_OWNER**|**sysname**|オブジェクト所有者の名前。 このフィールドは、常に値を返します。|  
|**TABLE_NAME**|**sysname**|オブジェクト名です。 このフィールドは、常に値を返します。|  
|**COLUMN_NAME**|**sysname**|各列の列名、 **TABLE_NAME**が返されます。 このフィールドは、常に値を返します。|  
|**DATA_TYPE**|**smallint**|ODBC データ型の整数コードです。 ODBC のデータ型にマップできないデータ型の場合は、NULL になります。 ネイティブ データ型の名前が返されます、 **TYPE_NAME**列。|  
|**TYPE_NAME**|**sysname**|データ型を表す文字列。 基になる DBMS は、このデータ型の名前を表示します。|  
|**PRECISION**|**int**|有効桁数の値。 戻り値、**精度**列は 10 進数。|  
|**LENGTH**|**int**|データのサイズを転送します。<sup>1</sup>|  
|**スケール**|**smallint**|小数点の右側にある数字の数。|  
|**RADIX**|**smallint**|数値データ型の基数。|  
|**NULLABLE**|**smallint**|Null 値許容属性を指定します。<br /><br /> 1 = NULL 値を許容します。<br /><br /> 0 = NULL 値を許容しません。|  
|**「解説」**|**varchar(254)**|このフィールドは常に NULL を返します。|  
|**COLUMN_DEF**|**nvarchar (4000)**|列の既定値です。|  
|**SQL_DATA_TYPE**|**smallint**|記述子の TYPE フィールドでの SQL データ型の値です。 この列と同じ、 **DATA_TYPE**列を除き、 **datetime**と sql-92**間隔**データ型。 この列は常に値が返されます。|  
|**SQL_DATETIME_SUB**|**smallint**|サブタイプ コード**datetime**と sql-92**間隔**データ型。 他のデータ型の場合、この列は NULL を返します。|  
|**CHAR_OCTET_LENGTH**|**int**|文字型または整数型の列の最大長 (バイト単位)。 その他のすべてのデータ型では、この列は NULL を返します。|  
|**ORDINAL_POSITION**|**int**|オブジェクト内の列の序数です。 オブジェクト内の最初の列には 1 です。 この列は常に値が返されます。|  
|**IS_NULLABLE**|**varchar(254)**|オブジェクト内の列の NULL 値の許容属性です。 NULL 値の許容属性の検査は ISO の規則に従います。 ISO SQL に準拠している DBMS では、空文字列を返すことはできません。<br /><br /> YES = 列に NULL を含むことができます。<br /><br /> いいえ = 列は null 値を含めることはできません。<br /><br /> NULL が許可されているかどうかがわからない列は、長さ 0 の文字列を返します。<br /><br /> この列は異なるに返される値から返される値、 **NULLABLE**列。|  
|**SS_DATA_TYPE**|**tinyint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用されるデータ型は拡張ストアド プロシージャです。 詳細については、「[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)」を参照してください。|  
  
 <sup>1</sup>詳細については、Microsoft ODBC のドキュメントを参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT および VIEW DEFINITION アクセス許可が必要です。  
  
## <a name="remarks"></a>コメント  
 **sp_columns**区切られた識別子の要件を満たしています。 詳細については、「[データベース識別子](../../relational-databases/databases/database-identifiers.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、指定されたテーブルの列情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_columns @table_name = N'Department',  
   @table_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次の例では、指定されたテーブルの列情報を返します。  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_columns @table_name = N'DimEmployee',  
   @table_owner = N'dbo';  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-transact-sql.md)   
 [ストアド プロシージャ カタログ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  


