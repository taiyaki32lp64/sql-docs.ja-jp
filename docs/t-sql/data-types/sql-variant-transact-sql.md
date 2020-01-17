---
title: sql_variant (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- sql_variant
- sql_variant_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sql_variant comparisons
- storing data [SQL Server], sql_variant
- sql_variant data type
- storage [SQL Server], sql_variant
ms.assetid: 01229779-8bc1-4c7d-890a-8246d4899250
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6a417d8240bb3360a13367230f0017762b51d659
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000506"
---
# <a name="sqlvariant-transact-sql"></a>sql_variant (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

このデータ型には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートしている各種データ型の値が格納されます。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
sql_variant  
```  
  
## <a name="remarks"></a>Remarks  
**sql_variant** 列、パラメーター、変数、およびユーザー定義関数の戻り値で使用できます。 **sql_variant** 他のデータ型の値をサポートするためにこれらのデータベース オブジェクトを使用します。
  
型の列 **sql_variant** 別のデータ型の行を含めることができます。 たとえば、列として定義されている **sql_varian**t 格納できる **int**, 、**バイナリ**, と **char** 値。
  
**sql_variant** 8,016 バイトの最大長を持つことができます。 これには、基本データ型に関する情報と値の両方が含まれます。 実際の基本データ型値の最大長は、8,000 バイトです。
  
A **sql_variant** 加算や減算などの操作に参加する前に、基本データ型の値にデータ型がキャスト最初にする必要があります。
  
**sql_variant** 既定値を割り当てることができます。 このデータ型は、基になる値として NULL を持つこともできますが、NULL 値には基本データ型は関連付けられていません。 また、 **sql_variant** 別に持つことはできません **sql_variant** をその基本型です。
  
一意、主キー、または外部キーは、型の列を含めることが **sql_variant**, 、でも、特定の行のキーを構成するデータ値の合計の長さは、インデックスの最大長を超えるを使用できないする必要があります。 この最大長は 900 バイトです。
  
テーブルは、任意の数を持つことができます **sql_variant** 列です。
  
**sql_variant** CONTAINSTABLE と FREETEXTTABLE では使用できません。
  
ODBC でサポートされていません **sql_variant**です。 クエリではそのため、 **sql_variant** Microsoft OLE DB Provider for ODBC (MSDASQL) を使用すると、列はバイナリ データとして返されます。 たとえば、 **sql_variant** "ps2091 という"文字列データが含まれている列は 0x505332303931 として返されます。
  
## <a name="comparing-sqlvariant-values"></a>sql_variant 値の比較  
**Sql_variant** データ型変換のためには、データ型階層リストの上部に属しています。 **Sql_variant** 、比較、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型階層の順序は、データ型ファミリにグループ化します。
  
|データ型階層|データ型ファミリ|  
|---|---|
|**sql_variant**|sql_variant |  
|**datetime2**|日付と時刻|  
|**datetimeoffset**|日付と時刻|  
|**datetime**|日付と時刻|  
|**smalldatetime**|日付と時刻|  
|**date**|日付と時刻|  
|**time**|日付と時刻|  
|**float**|概数値|  
|**real**|概数値|  
|**decimal**|正確な数値|  
|**money**|正確な数値|  
|**smallmoney**|正確な数値|  
|**bigint**|正確な数値|  
|**int**|正確な数値|  
|**smallint**|正確な数値|  
|**tinyint**|正確な数値|  
|**bit**|正確な数値|  
|**nvarchar**|Unicode|  
|**nchar**|Unicode|  
|**varchar**|Unicode|  
|**char**|Unicode|  
|**varbinary**|Binary|  
|**binary**|Binary|  
|**uniqueidentifier**|一意識別子 |  
  
次の規則が適用 **sql_variant** 比較します。
-   ときに **sql_variant** 異なる基本データ型の値が比較と基本データ型が、別のデータ型ファミリに、階層グラフでのデータ型ファミリがより高い値は 2 つの値の大きいと見なされます。  
-   ときに **sql_variant** 異なる基本データ型の値が比較し基本データ型が同じデータ型ファミリには、階層グラフで基本データ型が低位の値は、その他のデータ型に暗黙的に変換、および、比較が行われます。  
-   **char**、**varchar**、**nchar**、**nvarchar** データ型の **sql_variant** 値が比較されるとき、LCID、LCID バージョン、比較フラグ、並べ替え ID の各基準に基づいて、値の照合順序がまず比較されます。 これらの各基準は、示された順序に従って、それぞれ整数値として比較されます。 基準がすべて等しい場合は、照合順序に従って実際の文字列値が比較されます。  
  
## <a name="converting-sqlvariant-data"></a>sql_variant 型データの変換  
処理するときに、 **sql_variant** データ型の場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] するには、他のデータ型のオブジェクトの暗黙的な変換をサポートしている、 **sql_variant** 型です。 ただし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からの暗黙的な変換をサポートしていない **sql_variant** 別のデータ型のオブジェクトへのデータです。
  
## <a name="restrictions"></a>制限  
次の表は、種類の値を使用して格納することはできませんが **sql_variant**:
  
|||  
|-|-|  
|**varchar(max)**|**varbinary(max)**|  
|**nvarchar(max)**|**xml**|  
|**text**|**ntext**|  
|**image**|**rowversion** (**タイムスタンプ**)|  
|**sql_variant**|**geography**|  
|**hierarchyid**|**geometry**|  
|ユーザー定義データ型|**datetimeoffset**<sup>1</sup>| 

<sup>1</sup> SQL Server 2012 およびそれ以降では、**datetimeoffset** を制限していません。

## <a name="examples"></a>使用例  

### <a name="a-using-a-sqlvariant-in-a-table"></a>A. テーブルで sql_variant を使用する  
 次の例では、sql_variant データ型でテーブルを作成します。 次の例では、`colA` の `colB` =`1689` 値 `46279.1` に関する `SQL_VARIANT_PROPERTY` 情報を取得しています。 `tableA` には `sql_variant` 型の `colA` と、`colB` が含まれているものとします。  
  
```sql    
CREATE   TABLE tableA(colA sql_variant, colB int)  
INSERT INTO tableA values ( cast (46279.1 as decimal(8,2)), 1689)  
SELECT   SQL_VARIANT_PROPERTY(colA,'BaseType') AS 'Base Type',  
         SQL_VARIANT_PROPERTY(colA,'Precision') AS 'Precision',  
         SQL_VARIANT_PROPERTY(colA,'Scale') AS 'Scale'  
FROM      tableA  
WHERE      colB = 1689  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] これら 3 つの値の各ことに注意してください、 **sql_variant**です。  
  
```  
Base Type    Precision    Scale  
---------    ---------    -----  
decimal      8           2  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-a-sqlvariant-as-a-variable"></a>B. 変数として sql_variant を使用する   
 次の例では、sql_variant データ型を使用して変数を作成し、@v1 という名前の変数に関する `SQL_VARIANT_PROPERTY`情報を取得します。  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```    


## <a name="see-also"></a>参照
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[SQL_VARIANT_PROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sql-variant-property-transact-sql.md)
  
  
