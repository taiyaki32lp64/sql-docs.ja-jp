---
title: sp_executesql (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_executesql
- sp_executesql_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_executesql
- dynamic SQL
ms.assetid: a8d68d72-0f4d-4ecb-ae86-1235b962f646
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a548597b42bacdf5afaf7a2dc024156bd4ec3ad3
ms.sourcegitcommit: 40f3b1f2340098496d8428f50616095a190ae94b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2019
ms.locfileid: "68290352"
---
# <a name="sp_executesql-transact-sql"></a>sp_executesql (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  何回も再利用可能な、または動的に作成した [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントやバッチを実行します。 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントやバッチには、埋め込みパラメーターを含めることができます。  
  
> [!IMPORTANT]  
>  実行時にコンパイルされる[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントは、悪意のある攻撃にアプリケーションを公開できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_executesql [ @stmt = ] statement  
[   
  { , [ @params = ] N'@parameter_name data_type [ OUT | OUTPUT ][ ,...n ]' }   
     { , [ @param1 = ] 'value1' [ ,...n ] }  
]  
```  
  
## <a name="arguments"></a>引数  
 [ \@stmt =]*ステートメント*  
 含む Unicode 文字列には、[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントまたはバッチです。 \@stmt は、Unicode 定数または Unicode 変数のいずれかである必要があります。 \+ 演算子で 2 つの文字列を連結するなどの複雑な Unicode 式は使用できません。 文字定数も使用できません。 Unicode 定数が指定されている場合に付ける必要があります、 **N**します。Unicode 定数など**N 'sp_who'** が有効で、文字定数 **'sp_who'** はありません。 文字列のサイズは、使用可能なデータベース サーバーのメモリによってのみ制限されます。 64 ビット サーバーで、文字列のサイズが 2 GB の最大サイズに制限、 **nvarchar (max)** します。  
  
> [!NOTE]  
>  \@stmt には、たとえば、名前の変数と同じ形式を持つパラメーターを含めることができます。 `N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 含まれる各パラメーター \@stmt では、両方に対応するエントリがあります、 \@params パラメーター定義リストとパラメーター値の一覧。  
  
 [ \@params =] N'\@*parameter_name* *data_type* [,...*n* ] '  
 1 つの文字列に埋め込まれたすべてのパラメーターの定義を含む\@stmt します。この文字列は Unicode 定数または Unicode 変数にする必要があります。 各パラメーター定義は、パラメーター名とデータ型で構成されます。 *n*は追加のパラメーター定義を示すプレース ホルダーです。 すべてのパラメーターで指定された\@で stmt を定義する必要があります\@params します。 場合、[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントまたはバッチに\@stmt にパラメーターが含まれていない\@params は必要ありません。 このパラメーターの既定値は、NULL です。  
  
 [ \@param1 =] '*value1*'  
 パラメーター文字列に定義する最初のパラメーターの値を指定します。 Unicode 定数または Unicode 変数を指定できます。 含まれるすべてのパラメーターに指定されたパラメーター値が必要がある\@stmt します。ときに、値は必要ありません、[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントまたはバッチに\@stmt にパラメーターがありません。  
  
 [ OUT | OUTPUT ]  
 パラメーターが出力パラメーターであることを示します。 **text**、 **ntext**、および**image**パラメーターは、プロシージャが共通言語ランタイム (CLR) プロシージャでない限り、OUTPUT パラメーターとして使用できます。 OUTPUT キーワードを使用する出力パラメーターは、プロシージャが CLR プロシージャでない限り、カーソルのプレースホルダーにできます。  
  
 *n*  
 追加のパラメーターの値のプレース ホルダー。 定数または変数のみを指定できます。 値は、関数などのより複雑な式または演算子を使用して作成された式にすることはできません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) またはゼロ以外 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 SQL 文字列に組み込まれているすべての SQL ステートメントから結果セットが返されます。  
  
## <a name="remarks"></a>コメント  
 このトピックの「構文」セクションで説明した特定の順序で sp_executesql パラメーターを入力する必要があります。 パラメーターは、誤順序の入力は、エラー メッセージが発生します。  
  
 sp_executesql は、バッチ、名前の有効範囲、およびデータベース コンテキストに関して、EXECUTE と同じように動作します。 [!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントまたはバッチに sp_executesql \@stmt パラメーターは、sp_executesql ステートメントが実行されるまでコンパイルされません。 内容\@stmt がコンパイルされ、sp_executesql を呼び出したバッチの実行プランから別の実行プランとして実行します。 sp_executesql バッチから、sp_executesql を呼び出すバッチ内で宣言されている変数は参照できません。 sp_executesql バッチ内のローカル カーソルまたはローカル変数は、sp_executesql を呼び出すバッチでは認識されません。 コンテキストの変更データベース sp_executesql ステートメントの末尾にのみです。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのパラメーター値だけが変わる場合は、ストアド プロシージャの代わりに sp_executesql を使用して、ステートメントを何回でも実行できます。 この場合、パラメーター値が変わるだけで [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントそのものは変わらないため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ オプティマイザーではステートメントを最初に実行したときに生成した実行プランを再使用できます。  
  
> [!NOTE]  
>  完全に使用のパフォーマンスを向上させるために、ステートメント文字列内のオブジェクト名を修飾します。  
  
 sp_executesql では、次の例に示すように、[!INCLUDE[tsql](../../includes/tsql-md.md)] 文字列とは別にパラメーター値を設定できます。  
  
```  
DECLARE @IntVariable int;  
DECLARE @SQLString nvarchar(500);  
DECLARE @ParmDefinition nvarchar(500);  
  
/* Build the SQL string one time.*/  
SET @SQLString =  
     N'SELECT BusinessEntityID, NationalIDNumber, JobTitle, LoginID  
       FROM AdventureWorks2012.HumanResources.Employee   
       WHERE BusinessEntityID = @BusinessEntityID';  
SET @ParmDefinition = N'@BusinessEntityID tinyint';  
/* Execute the string with the first parameter value. */  
SET @IntVariable = 197;  
EXECUTE sp_executesql @SQLString, @ParmDefinition,  
                      @BusinessEntityID = @IntVariable;  
/* Execute the same string with the second parameter value. */  
SET @IntVariable = 109;  
EXECUTE sp_executesql @SQLString, @ParmDefinition,  
                      @BusinessEntityID = @IntVariable;  
```  
  
 出力パラメーターは、sp_executesql でも使用できます。 次の例では、`AdventureWorks2012.HumanResources.Employee` テーブルから役職名を取得し、それを出力パラメーター `@max_title` に返します。  
  
```  
DECLARE @IntVariable int;  
DECLARE @SQLString nvarchar(500);  
DECLARE @ParmDefinition nvarchar(500);  
DECLARE @max_title varchar(30);  
  
SET @IntVariable = 197;  
SET @SQLString = N'SELECT @max_titleOUT = max(JobTitle)   
   FROM AdventureWorks2012.HumanResources.Employee  
   WHERE BusinessEntityID = @level';  
SET @ParmDefinition = N'@level tinyint, @max_titleOUT varchar(30) OUTPUT';  
  
EXECUTE sp_executesql @SQLString, @ParmDefinition, @level = @IntVariable, @max_titleOUT=@max_title OUTPUT;  
SELECT @max_title;  
```  
  
 sp_executesql でパラメーター値を使用すると、EXECUTE ステートメントで文字列を実行する場合と比べて次のような利点があります。  
  
-   sp_executesql 文字列に指定される [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの実際のテキストは実行のたびに変わらないので、クエリ オプティマイザーでは、2 回目の実行で [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントと最初の実行時に作成した実行プランが照合される可能性があります。 したがって、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では 2 回目のステートメントをコンパイルする必要がありません。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]文字列が 1 回だけを作成します。  
  
-   整数パラメーターはネイティブ形式で指定します。 Unicode にキャストする必要はありません。  
  
## <a name="permissions"></a>アクセス許可  
 public ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-executing-a-simple-select-statement"></a>A. 簡単な SELECT ステートメントを実行する  
 次の例は、作成し、実行、単純な`SELECT`というパラメーターを含むステートメント`@level`します。  
  
```  
EXECUTE sp_executesql   
          N'SELECT * FROM AdventureWorks2012.HumanResources.Employee   
          WHERE BusinessEntityID = @level',  
          N'@level tinyint',  
          @level = 109;  
```  
  
### <a name="b-executing-a-dynamically-built-string"></a>B. 動的に作成した文字列の実行  
 次の例を使用して`sp_executesql`を動的に作成した文字列を実行します。 この例で使用するストアド プロシージャでは、特定の年の販売データをパーティション分割するために使用されるテーブル セットにデータを追加します。 形式は、その年の各月の 1 つのテーブルがあります。  
  
```  
CREATE TABLE May1998Sales  
    (OrderID int PRIMARY KEY,  
    CustomerID int NOT NULL,  
    OrderDate  datetime NULL  
        CHECK (DATEPART(yy, OrderDate) = 1998),  
    OrderMonth int  
        CHECK (OrderMonth = 5),  
    DeliveryDate datetime  NULL,  
        CHECK (DATEPART(mm, OrderDate) = OrderMonth)  
    )  
```  
  
 この例で使用するストアド プロシージャでは、新規の注文を正しいテーブルに追加する `INSERT` ステートメントを動的に作成し、実行します。 この例では、受注日を使用してデータを格納するテーブルの名前を作成し、この名前を `INSERT` ステートメントに組み込みます。  
  
> [!NOTE]  
>  これは、sp_executesql の簡単な例です。 この例では、エラー チェックや、テーブル間における注文番号の重複の確認などのビジネス ルール チェックは行いません。  
  
```  
CREATE PROCEDURE InsertSales @PrmOrderID INT, @PrmCustomerID INT,  
                 @PrmOrderDate DATETIME, @PrmDeliveryDate DATETIME  
AS  
DECLARE @InsertString NVARCHAR(500)  
DECLARE @OrderMonth INT  
  
-- Build the INSERT statement.  
SET @InsertString = 'INSERT INTO ' +  
       /* Build the name of the table. */  
       SUBSTRING( DATENAME(mm, @PrmOrderDate), 1, 3) +  
       CAST(DATEPART(yy, @PrmOrderDate) AS CHAR(4) ) +  
       'Sales' +  
       /* Build a VALUES clause. */  
       ' VALUES (@InsOrderID, @InsCustID, @InsOrdDate,' +  
       ' @InsOrdMonth, @InsDelDate)'  
  
/* Set the value to use for the order month because  
   functions are not allowed in the sp_executesql parameter  
   list. */  
SET @OrderMonth = DATEPART(mm, @PrmOrderDate)  
  
EXEC sp_executesql @InsertString,  
     N'@InsOrderID INT, @InsCustID INT, @InsOrdDate DATETIME,  
       @InsOrdMonth INT, @InsDelDate DATETIME',  
     @PrmOrderID, @PrmCustomerID, @PrmOrderDate,  
     @OrderMonth, @PrmDeliveryDate  
  
GO  
```  
  
 このプロシージャでは、sp_executesql を使用して文字列を実行しますが、これは EXECUTE を使用する場合と比べて効率的です。 Sp_executesql を使用すると、ときに、各月のテーブルごとに 1 つ生成される INSERT 文字列の 12 のバージョンがのみあります。 パラメーターの値が異なるため、EXECUTE で一意では各 INSERT 文字列です。 どちらの方法では、同じ数のバッチを生成、sp_executesql で作成される INSERT 文字列の類似性になります、クエリ オプティマイザーが実行プランを再利用する可能性が高くなります。  
  
### <a name="c-using-the-output-parameter"></a>C. OUTPUT パラメーターを使用する  
 次の例では、`OUTPUT`によって生成される結果セットを格納するパラメーター、`SELECT`内のステートメント、`@SQLString`パラメーター。2 つ`SELECT`の値を使用するステートメントを実行し、`OUTPUT`パラメーター。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @SQLString nvarchar(500);  
DECLARE @ParmDefinition nvarchar(500);  
DECLARE @SalesOrderNumber nvarchar(25);  
DECLARE @IntVariable int;  
SET @SQLString = N'SELECT @SalesOrderOUT = MAX(SalesOrderNumber)  
    FROM Sales.SalesOrderHeader  
    WHERE CustomerID = @CustomerID';  
SET @ParmDefinition = N'@CustomerID int,  
    @SalesOrderOUT nvarchar(25) OUTPUT';  
SET @IntVariable = 22276;  
EXECUTE sp_executesql  
    @SQLString  
    ,@ParmDefinition  
    ,@CustomerID = @IntVariable  
    ,@SalesOrderOUT = @SalesOrderNumber OUTPUT;  
-- This SELECT statement returns the value of the OUTPUT parameter.  
SELECT @SalesOrderNumber;  
-- This SELECT statement uses the value of the OUTPUT parameter in  
-- the WHERE clause.  
SELECT OrderDate, TotalDue  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderNumber = @SalesOrderNumber;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-executing-a-simple-select-statement"></a>D. 簡単な SELECT ステートメントを実行する  
 次の例は、作成し、実行、単純な`SELECT`というパラメーターを含むステートメント`@level`します。  
  
```  
-- Uses AdventureWorks  
  
EXECUTE sp_executesql   
          N'SELECT * FROM AdventureWorksPDW2012.dbo.DimEmployee   
          WHERE EmployeeKey = @level',  
          N'@level tinyint',  
          @level = 109;  
```  
  
## <a name="see-also"></a>関連項目  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
