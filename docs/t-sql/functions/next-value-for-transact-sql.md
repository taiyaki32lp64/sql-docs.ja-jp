---
title: NEXT VALUE FOR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NEXT_VALUE_TSQL
- NEXT
- NEXT VALUE
- NEXT VALUE FOR
- NEXT_TSQL
- NEXT_VALUE_FOR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- NEXT VALUE FOR function
- sequence number object, NEXT VALUE FOR function
ms.assetid: 92632ed5-9f32-48eb-be28-a5e477ef9076
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e37586d17a7b99d3dd191f63ed858805ef497a03
ms.sourcegitcommit: c70a0e2c053c2583311fcfede6ab5f25df364de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2019
ms.locfileid: "68670536"
---
# <a name="next-value-for-transact-sql"></a>NEXT VALUE FOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  指定したシーケンス オブジェクトからシーケンス番号を生成します。  
  
 シーケンスの作成と使用の詳細については、「[シーケンス番号](../../relational-databases/sequence-numbers/sequence-numbers.md)」を参照してください。 シーケンス番号の範囲を生成するには、[sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) を使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
NEXT VALUE FOR [ database_name . ] [ schema_name . ]  sequence_name  
   [ OVER (<over_order_by_clause>) ]  
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 シーケンス オブジェクトを含むデータベースの名前を指定します。  
  
 *schema_name*  
 シーケンス オブジェクトを含むスキーマの名前を指定します。  
  
 *sequence_name*  
 番号を生成するシーケンス オブジェクトの名前を指定します。  
  
 *over_order_by_clause*  
 シーケンス値がパーティション内の行に割り当てられる順序を決定します。 詳細については、「[OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)」を参照してください。  
  
## <a name="return-types"></a>戻り値の型  
 シーケンスの型を使用して数値を返します。  
  
## <a name="remarks"></a>Remarks  
 **NEXT VALUE FOR** 関数は、ストアド プロシージャやトリガーで使用できます。  
  
 ときに、 **NEXT VALUE FOR** 関数を使用するクエリや既定の制約で同じシーケンス オブジェクトが 2 回以上使用するかどうか、同じシーケンス オブジェクトは、または両方で使用される、値を提供するステートメントでと、結果セット内の行で同じシーケンスを参照するすべての列に対して実行されている既定の制約で同じ値が返されます。  
  
 **NEXT VALUE FOR** 関数は、非決定的であり、生成されるシーケンス値の数が定義されているコンテキストでのみ使用します。 特定のステートメントにおいて、参照されている各シーケンス オブジェクトに使用される値の数の定義を以下に示します。  
  
-   **SELECT** -参照されているシーケンス オブジェクトごとに、新しい値が 1 回生成、ステートメントの結果内の行ごとです。  
  
-   **INSERT** ...**VALUES** -参照されているシーケンス オブジェクトごとに、新しい値が 1 回生成、ステートメントで挿入された行はごとです。  
  
-   **UPDATE** -各参照されているシーケンス オブジェクトに対して、ステートメントによって更新された各行の新しい値が生成されます。  
  
-   手続き型ステートメント (**DECLARE**、**SET** など) - 参照されている各シーケンス オブジェクトに対して、ステートメントごとに新しい値が生成されます。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 **NEXT VALUE FOR** 関数は、次のような状況では使用できません。  
  
-   データベースが読み取り専用モードの場合。  
  
-   テーブル値関数の引数として使用する場合。  
  
-   集計関数の引数として使用する場合。  
  
-   共通テーブル式および派生テーブルを含むサブクエリ内で使用する場合。  
  
-   ビュー、ユーザー定義関数、または計算列内で使用する場合。  
  
-   ステートメントを使用して、**DISTINCT**, **UNION**, **UNION ALL**, **EXCEPT** or **INTERSECT** 演算子。  
  
-   **ORDER BY** 句を使用するステートメン内で使用する場合。ただし、**NEXT VALUE FOR** ...**OVER** (**ORDER BY** ...) が使用されている場合を除く。  
  
-   次の各句で使用する場合。**FETCH**、**OVER**、**OUTPUT**、**ON**、**PIVOT**、**UNPIVOT**、**GROUP BY**、**HAVING**、**COMPUTE**、**COMPUTE BY**、**FOR XML**。  
  
-   使用して条件付きの式で **CASE**, **CHOOSE**, **COALESCE**, **IIF**, **ISNULL**, or **NULLIF**です。  
  
-   **VALUES** 句がない場合の一部では、 **INSERT** ステートメントです。  
  
-   CHECK 制約の定義で使用する場合。  
  
-   ルールまたは既存のオブジェクトの定義で使用する場合 (既定の制約では使用できます)。  
  
-   既定では、ユーザー定義テーブル型で使用します。  
  
-   ステートメントを使用して、 **TOP**, 、**OFFSET**, 、または、 **ROWCOUNT** オプションを設定します。  
  
-   **WHERE** 、ステートメントの句。  
  
-   **MERGE** ステートメントです。 (する場合を除く、 **NEXT VALUE FOR** 関数は、対象のテーブルの既定の制約で使用してで既定値が使用される、 **CREATE** のステートメント、 **MERGE** ステートメントです)。  
  
## <a name="using-a-sequence-object-in-a-default-constraint"></a>既定の制約でのシーケンス オブジェクトの使用  
 使用する場合、 **NEXT VALUE FOR** 関数既定の制約では、次の規則が適用されます。  
  
-   複数のテーブル内の既定の制約から 1 つのシーケンス オブジェクトを参照できます。  
  
-   テーブルとシーケンス オブジェクトは同じデータベースに置く必要があります。  
  
-   既定の制約を追加するユーザーには、シーケンス オブジェクトに対する REFERENCES 権限が必要です。  
  
-   既定の制約を削除する前に、既定の制約から参照されているシーケンス オブジェクトを削除することはできません。  
  
-   複数の既定の制約で同じシーケンス オブジェクトを使用する場合、または値を提供するステートメントと実行中の既定の制約の両方で同じシーケンス オブジェクトを使用する場合、行内のすべての列に対して同じシーケンス番号が返されます。  
  
-   参照、 **NEXT VALUE FOR** 既定の制約で関数が指定することはできません、 **OVER** 句。  
  
-   既定の制約で参照されているシーケンス オブジェクトは変更できます。  
  
-   `INSERT ... SELECT` ステートメントまたは `INSERT ... EXEC` ステートメントで、挿入されるデータを **ORDER BY** 句を使用してクエリから取得する場合、**NEXT VALUE FOR** 関数によって返される値は、**ORDER BY** 句で指定された順序で生成されます。  
  
## <a name="using-a-sequence-object-with-an-over-order-by-clause"></a>OVER ORDER BY 句でのシーケンス オブジェクトの使用  
 **NEXT VALUE FOR** 関数は、適用することで並べ替えられたシーケンス値の生成をサポートしています、 **OVER** 句を **NEXT VALUE FOR** 呼び出します。 **OVER** 句を使用することにより、返される値が **OVER** 句の **ORDER BY** サブ句の順序で生成されることが保証されます。 次の追加のルールの適用を使用する場合、 **NEXT VALUE FOR** で動作、 **OVER**で 句。  
  
-   複数回呼び出す、 **NEXT VALUE FOR** 関数の 1 つのステートメントで同じシーケンス ジェネレーター必要がありますすべてを使用してください、同じ **OVER** 句の定義。  
  
-   複数回呼び出す、 **NEXT VALUE FOR** 関数の 1 つのステートメントで異なるシーケンス ジェネレーターの参照を別に持つことができる **OVER** 句の定義。  
  
-   **OVER** 句に適用される、 **NEXT VALUE FOR** 関数がサポートされていません、 **PARTITION BY** サブ句。  
  
-   呼び出しはすべての場合、 **NEXT VALUE FOR** で機能、 を**SELECT** ステートメントを指定、 **OVER**で 句、 **ORDER BY** 句で使用できる、 を**SELECT** ステートメントです。  
  
-   **SELECT** ステートメントまたは `INSERT ... SELECT ...` ステートメントでは、**NEXT VALUE FOR** 関数と共に **OVER** 句を使用できます。 **UPDATE** ステートメントまたは **MERGE** ステートメントでは、**NEXT VALUE FOR** 関数で **OVER** 句は使用できません。  
  
-   別のプロセスが同時にシーケンス オブジェクトにアクセスしている場合は、非連続的な番号が返される可能性があります。  
  
## <a name="metadata"></a>メタデータ  
 シーケンスに関する情報を取得するには、[sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md) カタログ ビューに対してクエリを実行します。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 必要があります **更新** シーケンス オブジェクトまたはシーケンスのスキーマに対するアクセスを許可します。 権限を付与する例については、後の例 F を参照してください。  
  
### <a name="ownership-chaining"></a>所有権の継承  
 シーケンス オブジェクトでは、所有権の継承をサポートしています。 シーケンス オブジェクトの所有者が、(既定の制約としてシーケンス オブジェクトを所有する) 呼び出し元のストアド プロシージャ、トリガー、またはテーブルと同じ場合、シーケンス オブジェクトに対する権限チェックは必要ありません。 シーケンス オブジェクトの所有者が、呼び出し元のストアド プロシージャ、トリガー、またはテーブルと異なる場合、シーケンス オブジェクトに対する権限チェックが必要です。  
  
 ときに、 **NEXT VALUE FOR** テーブル内の既定値として関数を使用すると、ユーザーには、両方が必要とする **INSERT** 、テーブルに対する権限と **UPDATE** を既定値を使用してデータを挿入する、シーケンスのオブジェクトに対するアクセスを許可します。  
  
-   既定の制約の所有者がシーケンス オブジェクトと同じ場合、既定の制約を呼び出す際に、シーケンス オブジェクトに対する権限は必要ありません。  
  
-   既定の制約の所有者がシーケンス オブジェクトと異なる場合、既定の制約を使用してシーケンス オブジェクトを呼び出す際にも、シーケンス オブジェクトに対する権限が必要です。  
  
### <a name="audit"></a>監査  
 **NEXT VALUE FOR** 関数を監査するには、SCHEMA_OBJECT_ACCESS_GROUP を監視します。  
  
## <a name="examples"></a>使用例  
 シーケンスの作成と、**NEXT VALUE FOR** 関数を使用したシーケンス番号の生成の両方の使用例については、「[シーケンス番号](../../relational-databases/sequence-numbers/sequence-numbers.md)」を参照してください。  
  
 次の例では、`CountBy1` という名前のスキーマの `Test` という名前のシーケンスを使用します。 次のステートメントを実行して、`Test.CountBy1` シーケンスを作成します。 例 C および E では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースを使用します。そのため、`CountBy1` シーケンスはそのデータベースに作成されます。  
  
```  
USE AdventureWorks2012 ;  
GO  
  
CREATE SCHEMA Test;  
GO  
  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="a-using-a-sequence-in-a-select-statement"></a>A. SELECT ステートメントでシーケンスを使用する  
 次の例では、使用されるたびに 1 つずつ増加する `CountBy1` という名前のシーケンスを作成します。  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1 AS FirstUse;  
SELECT NEXT VALUE FOR Test.CountBy1 AS SecondUse;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FirstUse  
1  
  
SecondUse  
2
```  
  
### <a name="b-setting-a-variable-to-the-next-sequence-value"></a>B. 変数に次のシーケンス値を設定する  
 次の例では、変数にシーケンス番号の次の値を設定する 3 つの方法を示します。  
  
```  
DECLARE @myvar1 bigint = NEXT VALUE FOR Test.CountBy1  
DECLARE @myvar2 bigint ;  
DECLARE @myvar3 bigint ;  
SET @myvar2 = NEXT VALUE FOR Test.CountBy1 ;  
SELECT @myvar3 = NEXT VALUE FOR Test.CountBy1 ;  
SELECT @myvar1 AS myvar1, @myvar2 AS myvar2, @myvar3 AS myvar3 ;  
GO  
```  
  
### <a name="c-using-a-sequence-with-a-ranking-window-function"></a>C. 順位付け関数と共にシーケンスを使用する  
  
```  
USE AdventureWorks2012 ;  
GO  
  
SELECT NEXT VALUE FOR Test.CountBy1 OVER (ORDER BY LastName) AS ListNumber,  
    FirstName, LastName  
FROM Person.Contact ;  
GO  
```  
  
### <a name="d-using-the-next-value-for-function-in-the-definition-of-a-default-constraint"></a>D. 既定の制約の定義で NEXT VALUE FOR 関数を使用する  
 使用して、 **NEXT VALUE FOR** 関数は、既定の制約の定義ではサポートされています。 **CREATE TABLE** ステートメントでの **NEXT VALUE FOR** の使用例については、「[シーケンス番号](../../relational-databases/sequence-numbers/sequence-numbers.md)」を参照してください。 次の例では、`ALTER TABLE` を使用して、シーケンスを既定値として現在のテーブルに追加します。  
  
```  
CREATE TABLE Test.MyTable  
(  
    IDColumn nvarchar(25) PRIMARY KEY,  
    name varchar(25) NOT NULL  
) ;  
GO  
  
CREATE SEQUENCE Test.CounterSeq  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
ALTER TABLE Test.MyTable  
    ADD   
        DEFAULT N'AdvWorks_' +   
        CAST(NEXT VALUE FOR Test.CounterSeq AS NVARCHAR(20))   
        FOR IDColumn;  
GO  
  
INSERT Test.MyTable (name)  
VALUES ('Larry') ;  
GO  
  
SELECT * FROM Test.MyTable;  
GO  
```  
  
### <a name="e-using-the-next-value-for-function-in-an-insert-statement"></a>E. INSERT ステートメントで NEXT VALUE FOR 関数を使用する  
 次の例では、`TestTable` という名前のテーブルを作成した後、`NEXT VALUE FOR` 関数を使用して、行を挿入します。  
  
```  
CREATE TABLE Test.TestTable  
     (CounterColumn int PRIMARY KEY,  
    Name nvarchar(25) NOT NULL) ;   
GO  
  
INSERT Test.TestTable (CounterColumn,Name)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Syed') ;  
GO  
  
SELECT * FROM Test.TestTable;   
GO  
  
```  
  
### <a name="e-using-the-next-value-for-function-with-select--into"></a>E. SELECT ... INTO と共に NEXT VALUE FOR 関数を使用するINTO  
 次の例では、`SELECT ... INTO` ステートメントを使用して `Production.NewLocation` という名前のテーブルを作成し、`NEXT VALUE FOR` 関数を使用して各行に番号を付けます。  
  
```  
USE AdventureWorks2012 ;   
GO  
  
SELECT NEXT VALUE FOR Test.CountBy1 AS LocNumber, Name   
    INTO Production.NewLocation  
    FROM Production.Location ;  
GO  
  
SELECT * FROM Production.NewLocation ;  
GO  
```  
  
### <a name="f-granting-permission-to-execute-next-value-for"></a>F. NEXT VALUE FOR を実行する権限を付与する  
 次の例では、`Test.CounterSeq` シーケンスを使用して、`NEXT VALUE FOR` を実行できるように、 という名前のユーザーに **UPDATE** `AdventureWorks\Larry`権限を付与します。  
  
```  
GRANT UPDATE ON OBJECT::Test.CounterSeq TO [AdventureWorks\Larry] ;  
```  
  
## <a name="see-also"></a>参照  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [シーケンス番号](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
