---
title: SELECT 句 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SELECT Clause
- SELECT_Clause_TSQL
- DISTINCT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- parentheses [SQL Server]
- identity columns [SQL Server], SELECT clause
- SELECT clause
- $IDENTITY keyword
- user-defined types [SQL Server], invoking methods and properties
- SELECT statement [SQL Server], processing orders
- clauses [SQL Server], SELECT
- $ROWGUID keyword
- queries [SQL Server], results
ms.assetid: 2616d800-4853-4cf1-af77-d32d68d8c2ef
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 51707d97a738df13b7aae3c9e7208af76d440492
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141064"
---
# <a name="select-clause-transact-sql"></a>SELECT 句 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  クエリで返される列を指定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT [ ALL | DISTINCT ]  
[ TOP ( expression ) [ PERCENT ] [ WITH TIES ] ]   
<select_list>   
<select_list> ::=   
    {   
      *   
      | { table_name | view_name | table_alias }.*   
      | {  
          [ { table_name | view_name | table_alias }. ]  
               { column_name | $IDENTITY | $ROWGUID }   
          | udt_column_name [ { . | :: } { { property_name | field_name }   
            | method_name ( argument [ ,...n] ) } ]  
          | expression  
          [ [ AS ] column_alias ]   
         }  
      | column_alias = expression   
    } [ ,...n ]   
```  
  
## <a name="arguments"></a>引数  
 **ALL**  
 結果セットに重複した行を含むことを指定します。 ALL が既定値です。  
  
 DISTINCT  
 結果セットに一意な行のみを含むことを指定します。 NULL 値は、DISTINCT キーワードにおいて等しいと見なされます。  
  
 TOP (*expression* ) [ PERCENT ] [ WITH TIES ]  
 クエリの結果セットから、指定された最初の行セットまたは比率 (%) に相当する行だけが返されることを示します。 *expression* は行数または行の比率 (%) にすることができます。  
  
 旧バージョンとの互換性を維持するため、SELECT ステートメント内でかっこを使用しないで TOP *expression* を使用する方法もサポートされていますが、この方法は推奨されていません。 詳細については、「[TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)」を参照してください。  
  
\< select_list > 結果セットに選択される列です。 選択リストは、コンマで区切られた一連の式です。 選択リストに指定できる式の最大数は、4,096 です。  
  
 \*  
 FROM 句内のすべてのテーブルおよびビューの、すべての列を返すことを指定します。 列は、FROM 句に指定されているテーブルまたはビューの順に、テーブルまたはビュー内に並んでいる順序で返されます。  
  
 *table_name* | *view_name* | *table*_*alias*.*  
 \* のスコープを、指定したテーブルまたはビューに限定します。  
  
 *column_name*  
 返される列の名前です。 FROM 句内の 2 つのテーブルに同じ名前の列がある場合などに参照先が混乱しないように、*column_name* を修飾します。 たとえば、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内の SalesOrderHeader テーブルおよび SalesOrderDetail テーブルの両方に ModifiedDate という名前の列があります。 クエリでこれら 2 つのテーブルを結合した場合、SalesOrderDetail エントリの変更日付を選択リストで SalesOrderDetail.ModifiedDate として指定できます。  
  
 *式 (expression)*  
 定数、関数、または列名、定数、関数を演算子で組み合わせたもの、あるいはサブクエリを指定します。  
  
 $IDENTITY  
 ID 列を返します。 詳細については、「[IDENTITY &#40;プロパティ&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)」、「[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)」、および「[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)」を参照してください。  
  
 FROM 句内の複数のテーブルが IDENTITY プロパティを備えた列を持つ場合は、T1.$IDENTITY などのように、$IDENTITY を指定のテーブル名で修飾する必要があります。  
  
 $ROWGUID  
 行 GUID 列を返します。  
  
 FROM 句内の複数のテーブルが ROWGUIDCOL プロパティを持つ場合は、T1.$ROWGUID などのように、$ROWGUID を指定のテーブル名で修飾する必要があります。  
  
 *udt_column_name*  
 返される共通言語ランタイム (CLR) ユーザー定義型列の名前です。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、ユーザー定義型の値をバイナリ表記で返します。 ユーザー定義型の値を文字列または XML 形式で返すには、[CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) または [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) を使用します。  
  
 { . | :: }  
 CLR ユーザー定義型のメソッド、プロパティ、またはフィールドを指定します。 インスタンス (静的ではない) メソッド、プロパティ、フィールド には . を使用します。 静的なメソッド、プロパティ、フィールドには :: を使用します。 CLR ユーザー定義型のメソッド、プロパティ、またはフィールドを呼び出すには、その型に対する EXECUTE 権限が必要です。  
  
 *property_name*  
 *udt_column_name* のパブリック プロパティを指定します。  
  
 *field_name*  
 *udt_column_name* のパブリック データ メンバーを指定します。  
  
 *method_name*  
 1 つ以上の引数を使用する *udt_column_name* のパブリック メソッドを指定します。 *method_name* をミューテーター メソッドにすることはできません。  
  
 次の例では、`Location` という名前のメソッドを呼び出すことにより、`point` 型として定義されている `Cities` 列に対する値を `Distance` テーブルから選択します。  
  
```  
CREATE TABLE dbo.Cities (  
     Name varchar(20),  
     State varchar(20),  
     Location point );  
GO  
DECLARE @p point (32, 23), @distance float;  
GO  
SELECT Location.Distance (@p)  
FROM Cities;  
```  
  
 *column_alias*  
 クエリの結果セット内の列名を置き換える別名です。 たとえば、quantity という名前の列に対して、Quantity、Quantity to Date、Qty などの別名を指定できます。  
  
 別名を使用して、式の結果の名前を指定することもできます。たとえば、次のようにします。  
  
 ```sql
 USE AdventureWorks2012;  
 GO  
 SELECT AVG(UnitPrice) AS [Average Price]  
 FROM Sales.SalesOrderDetail;
 ```  
  
 *column_alias* は、ORDER BY 句の中で使用できます。 ただし、WHERE 句、GROUP BY 句、または HAVING 句の中では使用できません。 クエリ式が DECLARE CURSOR ステートメントに含まれている場合、FOR UPDATE 句の中で *column_alias* を使用することはできません。  
  
## <a name="remarks"></a>Remarks  
 選択リストに含まれる **text** または **ntext** 列に対して返されるデータの長さは、**text** 列の実際のサイズ、既定の TEXTSIZE セッションの設定値、またはハードコーディングされたアプリケーションの制限値のうちの最小値に設定されます。 セッション用に、返されるテキストの長さを変更するには、SET ステートメントを使ってください。 既定では、SELECT ステートメントが返すテキスト データの長さの制限は 4,000 バイトです。  
  
 次の動作のいずれかが発生した場合、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]では例外 511 が発生し、現在実行中のステートメントがロールバックされます。  
  
-   SELECT ステートメントで、8,060 バイトを超える結果行または中間作業テーブル行を生成した場合  
  
-   DELETE、INSERT、または UPDATE ステートメントを、8,060 バイトを超える行で実行しようとした場合  
  
 SELECT INTO ステートメントまたは CREATE VIEW ステートメントで作成された列に列名が付いていない場合は、エラーが発生します。  
  
## <a name="see-also"></a>参照  
 [SELECT の例 &#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md)   
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
