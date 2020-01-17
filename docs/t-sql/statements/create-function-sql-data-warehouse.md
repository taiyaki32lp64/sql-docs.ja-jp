---
title: CREATE FUNCTION (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8cad1b2c-5ea0-4001-9060-2f6832ccd057
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f5510d6c75380e48008740ab8a0f5b1c9f500fe5
ms.sourcegitcommit: e9c1527281f2f3c7c68981a1be94fe587ae49ee9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73064541"
---
# <a name="create-function-sql-data-warehouse"></a>CREATE FUNCTION (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] でユーザー定義関数を作成します。 ユーザー定義の関数は、パラメーターを受け取り、複雑な計算などの操作を実行する [!INCLUDE[tsql](../../includes/tsql-md.md)] ルーチンであり、そのアクションの結果を値として返します。 戻り値は、スカラー (単一) 値である必要があります。 このステートメントを使用して、次の方法で使用できる再利用可能なルーチンを作成します。  
  
-   SELECT などの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント内で使用する  
  
-   関数を呼び出すアプリケーション内で使用する  
  
-   別のユーザー定義関数の定義内で使用する  
  
-   列の CHECK 制約を定義する  
  
-   ストアド プロシージャを置換する  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
--Transact-SQL Scalar Function Syntax  
CREATE FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN scalar_expression  
    END  
[ ; ]  
  
<function_option>::=   
{  
    [ SCHEMABINDING ]  
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
}  
  
```  
  
## <a name="arguments"></a>引数  
 *schema_name*  
 ユーザー定義関数が属するスキーマの名前を指定します。  
  
 *function_name*  
 ユーザー定義関数の名前です。 関数名は、識別子の規則に準拠する必要があり、そのスキーマ、データベース内で一意である必要があります。  
  
> [!NOTE]  
>  パラメーターを指定しない場合でも、関数名の後にはかっこが必要です。  
  
 @*parameter_name*  
 ユーザー定義関数内のパラメーターです。 1 つ以上のパラメーターを宣言できます。  
  
 1 つの関数では、最高 2,100 個のパラメーターを使用できます。 宜言した各パラメーターの値は、関数の実行時に、ユーザーが指定する必要があります (そのパラメーターの既定値が定義されていない場合)。  
  
 最初の文字をアット マーク (@) にしてパラメーター名を指定します。 パラメーター名は識別子のルールに従っている必要があります。 パラメーターは関数に対してローカルです。同じパラメーター名を他の関数で使用できます。 パラメーターは定数の代わりとしてのみ使用できます。パラメーターは、テーブル名、列名、またはその他のデータベース オブジェクト名の代わりに使用することはできません。  
  
> [!NOTE]  
>  ストアド プロシージャまたはユーザー定義関数でパラメーターを渡すとき、あるいはバッチ ステートメントで変数を宣言して設定するときには、ANSI_WARNINGS が無視されます。 たとえば、変数を **char(3)** と定義し、これに 4 文字以上の値を設定すると、データが定義されたサイズに合わせて切り捨てられてから、INSERT または UPDATE ステートメントが成功します。  
  
 *parameter_data_type*  
 パラメーター データ型。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数は、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] でサポートされるすべてのスカラー データ型を許可します。 タイムスタンプ (rowversion) データ型はサポートされていません。  
  
 [ =*default* ]  
 パラメーターの既定値です。 *default* 値が定義されている場合は、パラメーターに値を指定せずに関数を実行できます。  
  
 関数のパラメーターに既定値がある場合に、既定値を取得する目的でその関数を呼び出すときは、DEFAULT キーワードを指定する必要があります。 この動作は、ストアド プロシージャで既定値を持つパラメーターを使用する場合とは異なります。ストアド プロシージャの場合は、パラメーターを省略すると既定値が暗黙的に使用されます。  
  
 *return_data_type*  
 スカラー ユーザー定義関数の戻り値です。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数は、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] でサポートされるすべてのスカラー データ型を許可します。 タイムスタンプ (rowversion) データ型はサポートされていません。 カーソルとテーブルの非スカラー型を指定することはできません。  
  
 *function_body*  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの連続。  Function_body は SELECT ステートメントを含めることはできませんし、データベースのデータを参照することはできません。  Function_body は、テーブルまたはビューを参照できません。 関数の本体では、その他の決定的な関数を呼び出すことができますが、非決定的関数を呼び出すことはできません。 
  
 スカラー関数の *function_body* は、総合してスカラー値と評価される一連の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントです。  
  
 *scalar_expression*  
 スカラー関数が返すスカラー値を指定します。  
  
 **\<function_option>::=** 
  
 関数に以下のオプションを 1 つ以上指定します。  
  
 SCHEMABINDING  
 参照するデータベース オブジェクトに対して、その関数がバインドされるように指定します。 SCHEMABINDING を指定した場合、ベース オブジェクトに対して関数定義に影響を与えるような変更は行えません。 まず関数定義を変更または削除して、変更するオブジェクトとの依存関係を解消する必要があります。  
  
 関数が参照するオブジェクトへのバインドは、次のいずれかの操作が行われた場合にのみ削除されます。  
  
-   関数を削除した場合。  
  
-   関数を、SCHEMABINDING オプションを指定せずに ALTER ステートメントを使用して変更した場合。  
  
 関数をスキーマにバインドできるのは、次の条件が満たされている場合に限られます。  
  
-   関数によって参照されているすべてのユーザー定義関数もスキーマにバインドします。  
  
-   関数と関数によって参照されるその他の UDF は、1 つのパーツまたは 2 つのパーツの名前を使用して参照されます。  
  
-   同じデータベース内の組み込み関数とその他の UDF のみを、UDF の本体内で参照することができます。  
  
-   CREATE FUNCTION ステートメントを実行したユーザーには、関数で参照するデータベース オブジェクトの REFERENCES 権限があります。  
  
 SCHEMABINDING を削除するには、ALTER を使用します。  
  
 RETURNS NULL ON NULL INPUT | **CALLED ON NULL INPUT**  
 スカラー値関数の **OnNULLCall** 属性を指定します。 指定しない場合は、既定で CALLED ON NULL INPUT が暗黙的に使用されます。 つまり、NULL が引数として渡された場合でも、関数本体が実行されます。  
  
## <a name="best-practices"></a>ベスト プラクティス  
 ユーザー定義関数が SCHEMABINDING 句を使って作成されていない場合、基になるオブジェクトに行った変更は関数の定義に影響し、呼び出されたときに予期しない結果が生じる可能性があります。 基になるオブジェクトに対する変更によって関数が古くならないように、次のいずれかの操作を行うことをお勧めします。  
  
-   関数を作成しているときに、WITH SCHEMABINDING 句を指定します。 これにより、関数定義で参照されているオブジェクトは、一緒に関数も変更しない限り変更できなくなります。  
  
## <a name="interoperability"></a>相互運用性  
 関数で有効なステートメントは以下のとおりです。  
  
-   代入ステートメント。  
  
-   TRY...CATCH ステートメント以外の流れ制御ステートメント。  
  
-   ローカル データ変数を定義する DECLARE ステートメント。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 ユーザー定義関数は、データベースの状態を変更するアクションの実行に使用することはできません。  
  
 ユーザー定義関数は入れ子にすることができます。つまり、1 つのユーザー定義関数で、別のユーザー定義関数を呼び出すことができます。 呼び出された関数が実行を開始すると入れ子レベルが 1 つ上がり、呼び出された関数が実行を終了するとレベルが 1 つ下がります。 ユーザー定義関数は、32 レベルまで入れ子にすることができます。 入れ子レベルが最大値を超えると、関数チェーン全体の呼び出しが失敗します。   
  
## <a name="metadata"></a>メタデータ  
 このセクションでは、ユーザー定義関数に関するメタデータを返すために使用できるシステム カタログ ビューを示します。  
  
 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) : [!INCLUDE[tsql](../../includes/tsql-md.md)] ユーザー定義関数の定義を表示します。 例:  
  
```sql  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o   
    ON m.object_id = o.object_id   
    AND type = ('FN');  
GO  
  
```  
  
 [sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md) : ユーザー定義関数で定義されているパラメーターの情報を表示します。  
  
 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) : 関数が参照する基になるオブジェクトを表示します。  
  
## <a name="permissions"></a>アクセス許可  
 データベースの CREATE FUNCTION 権限と、関数を作成するスキーマの ALTER 権限が必要です。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-a-scalar-valued-user-defined-function-to-change-a-data-type"></a>A. データ型を変更するために、スカラー値ユーザー定義関数を使用する  
 この単純な関数は、**int** データ型として入力を取り、**decimal(10,2)** データ型として出力を返します。  
  
```sql  
CREATE FUNCTION dbo.ConvertInput (@MyValueIn int)  
RETURNS decimal(10,2)  
AS  
BEGIN  
    DECLARE @MyValueOut int;  
    SET @MyValueOut= CAST( @MyValueIn AS decimal(10,2));  
    RETURN(@MyValueOut);  
END;  
GO  
  
SELECT dbo.ConvertInput(15) AS 'ConvertedValue';  
```  
  
## <a name="see-also"></a>参照  
 [ALTER FUNCTION (SQL Server PDW)](https://msdn.microsoft.com/25ff3798-eb54-4516-9973-d8f707a13f6c)   
 [DROP FUNCTION (SQL Server PDW)](https://msdn.microsoft.com/1792a90d-0d06-4852-9dec-6de1b9cd229e)  
  
  


