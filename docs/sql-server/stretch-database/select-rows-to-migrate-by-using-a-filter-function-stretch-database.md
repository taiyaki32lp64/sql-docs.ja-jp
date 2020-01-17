---
title: フィルター関数を使用して移行する行を選択する
ms.date: 06/27/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, predicates
- predicates for Stretch Database
- Stretch Database, inline table-valued functions
- inline table-valued functions for Stretch Database
ms.assetid: 090890ee-7620-4a08-8e15-d2fbc71dd12f
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: f744dbde25bf5f7b307ccb44e03de70c1b60cc66
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844550"
---
# <a name="select-rows-to-migrate-by-using-a-filter-function-stretch-database"></a>フィルター関数を使用して移行する行を選択する (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  コールド データを別のテーブルに保存している場合、そのテーブル全体を移行するように Stretch Database を構成できます。 一方、テーブルにホット データとコールド データの両方が含まれている場合は、移行する行を選択するフィルター述語を指定できます。 フィルター述語はインライン テーブル値関数です。 この記事では、移行する行を選択するインライン テーブル値関数を作成する方法について説明します。  
  
> [!IMPORTANT]
> 指定したフィルター関数のパフォーマンスが低いと、データ移行のパフォーマンスも低くなります。 Stretch Database では、CROSS APPLY 演算子を使用してテーブルにフィルター関数を適用します。  
  
 フィルター関数を指定しない場合、テーブル全体が移行されます。  
  
 データベースのストレッチの有効化ウィザードを実行すると、テーブル全体を移行することも、ウィザードで単純なフィルター関数を指定することもできます。 移行する行を選択するために別の種類のフィルター関数を使用する場合、次のいずれかの操作を行います。  
  
-   ウィザードを終了し、ALTER TABLE ステートメントを実行してテーブルの Stretch を有効にして、フィルター関数を指定します。  
  
-   ウィザードを終了した後、ALTER TABLE ステートメントを実行してフィルター関数を指定します。  
  
 関数を追加するための ALTER TABLE 構文については、この記事で後述します。  
  
## <a name="basic-requirements-for-the-filter-function"></a>フィルター関数の基本的な要件  
 Stretch Database のフィルター述語に必要なインライン テーブル値関数は次の例のようになります。  
  
```sql  
CREATE FUNCTION dbo.fn_stretchpredicate(@column1 datatype1, @column2 datatype2 [, ...n])  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE <predicate>  
```  
  
 関数のパラメーターは、テーブルの列の識別子である必要があります。  
  
 フィルター関数で使用される列が削除または変更されるのを防ぐために、スキーマ バインドが必要となります。  
  
### <a name="return-value"></a>戻り値  
 関数から空ではない結果が返された場合、その行は移行の対象になります。 それ以外の場合 (結果が返されない場合)、その行は移行の対象にはなりません。  
  
### <a name="conditions"></a>[条件]  
 &lt;*predicate*&gt; は、1 つの条件で構成される場合もあれば、AND 論理演算子で結合された複数の条件で構成される場合もあります。  
  
```  
<predicate> ::= <condition> [ AND <condition> ] [ ...n ]  
```  
  
 各条件は、1 つのプリミティブ条件で構成される場合もあれば、OR 論理演算子で結合された複数のプリミティブ条件で構成される場合もあります。  
  
```  
<condition> ::= <primitive_condition> [ OR <primitive_condition> ] [ ...n ]  
```  
  
### <a name="primitive-conditions"></a>プリミティブ条件  
 プリミティブ条件では、次のいずれかの比較を実行できます。  
  
```  
<primitive_condition> ::=   
{  
<function_parameter> <comparison_operator> constant  
| <function_parameter> { IS NULL | IS NOT NULL }  
| <function_parameter> IN ( constant [ ,...n ] )  
}  
  
```  
  
-   関数パラメーターと定数式を比較します。 たとえば、 `@column1 < 1000`のようにします。  
  
     次の例では、 *date* 列の値が &lt; 1/1/2016 であるかどうかを確認します。  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate(@column1 datetime)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
    GO  
  
    ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(date),  
        MIGRATION_STATE = OUTBOUND  
    ) )  
  
    ```  
  
-   IS NULL または IS NOT NULL 演算子を関数パラメーターに適用します。  
  
-   IN 演算子を使用して、関数パラメーターと定数値のリストを比較します。  
  
     次の例では、 *shipment_status*  列の値が `IN (N'Completed', N'Returned', N'Cancelled')`であるかどうかを確認します。  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate(@column1 nvarchar(15))  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 IN (N'Completed', N'Returned', N'Cancelled')  
    GO  
  
    ALTER TABLE table1 SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(shipment_status),  
        MIGRATION_STATE = OUTBOUND  
    ) )  
  
    ```  
  
### <a name="comparison-operators"></a>比較演算子  
 次の比較演算子がサポートされています。  
  
 `<, <=, >, >=, =, <>, !=, !<, !>`  
  
```  
<comparison_operator> ::= { < | <= | > | >= | = | <> | != | !< | !> }  
```  
  
### <a name="constant-expressions"></a>定数式  
 関数を定義するときに、フィルター関数で使用する定数を、評価できる決定論的な式にすることができます。 定数式には以下を含めることができます。  
  
-   リテラル。 たとえば、 `N'abc', 123`のようにします。  
  
-   代数式。 たとえば、 `123 + 456`のようにします。  
  
-   決定論的関数。 たとえば、 `SQRT(900)`のようにします。  
  
-   CAST または CONVERT を使用した決定論的変換。 たとえば、 `CONVERT(datetime, '1/1/2016', 101)`のようにします。  
  
### <a name="other-expressions"></a>その他の式  
 BETWEEN 演算子と NOT BETWEEN 演算子を同等の AND 式と OR 式に置き換えた後、結果的に作成される関数がここで説明するルールに準拠する場合は、BETWEEN 演算子と NOT BETWEEN 演算子を使用できます。  
  
 サブクエリや非決定論的関数 (RAND() や GETDATE() など) は使用できません。  
  
## <a name="add-a-filter-function-to-a-table"></a>フィルター関数をテーブルに追加する  
 **ALTER TABLE** ステートメントを実行し、 **FILTER_PREDICATE** パラメーターの値として既存のインライン テーブル値関数を指定して、テーブルにフィルター関数を追加します。 例:  
  
```sql  
ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
    FILTER_PREDICATE = dbo.fn_stretchpredicate(column1, column2),  
    MIGRATION_STATE = <desired_migration_state>  
) )  
  
```  
  
 関数を述語としてテーブルにバインドすると、次のようになります。  
  
-   次回のデータ移行時に、関数から空ではない値が返された行だけが移行されます。  
  
-   関数で使用される列はスキーマ バインドされています。 テーブルで関数がフィルター述語として使用されている限り、これらの列を変更することはできません。  
  
 テーブルで関数がフィルター述語として使用されている限り、インライン テーブル値関数を削除することはできません。 

> [!TIP]
> フィルター関数のパフォーマンスを向上させるには、関数が使用する列にインデックスを作成します。

 ### <a name="passing-column-names-to-the-filter-function"></a>列名をフィルター関数に渡す
 
 テーブルにフィルター関数を割り当てるときは、1 部構成の名前を使用してフィルター関数に渡される列名を指定します。 列名を渡すときに、3 部構成の名前を指定すると、Stretch 対応テーブルに対する後続のクエリが失敗します。

たとえば、次の例のように 3 部構成の列名を指定すると、ステートメントは正常に実行されますが、テーブルに対する後続のクエリは失敗します。

```sql
ALTER TABLE SensorTelemetry 
  SET ( REMOTE_DATA_ARCHIVE = ON (
    FILTER_PREDICATE=dbo.fn_stretchpredicate(dbo.SensorTelemetry.ScanDate),
    MIGRATION_STATE = OUTBOUND )
  )
```

代わりに、次の例で示すように、1 部構成の列名を持つフィルター関数を指定します。

```sql
ALTER TABLE SensorTelemetry 
  SET ( REMOTE_DATA_ARCHIVE = ON  (
    FILTER_PREDICATE=dbo.fn_stretchpredicate(ScanDate),
    MIGRATION_STATE = OUTBOUND )
  )
```
  
## <a name="addafterwiz"></a>ウィザードの実行後、フィルター関数を追加する  
  
**データベースのストレッチの有効化** ウィザードで作成できない関数を使用したい場合は、ウィザードを終了してから **ALTER TABLE** ステートメントを実行して関数を指定できます。 ただし、関数を適用する前に、既に進行中のデータ移行を停止し、移行されたデータを戻す必要があります。 (これが必要な理由については、「 [既存のフィルター関数の置き換え](#replacePredicate)」を参照してください)。
  
1. 移行の方向を反転し、既に移行されたデータを戻します。 この操作は開始すると取り消すことはできません。 また、送信データ転送 (エグレス) のための Azure のコストも発生します。 詳細については、「 [Data Transfers (データ転送) の料金詳細](https://azure.microsoft.com/pricing/details/data-transfers/)」を参照してください。  
  
    ```sql  
    ALTER TABLE <table name>  
        SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ;   
    ```  
  
2. 移行が完了するまで待ちます。 状態は、SQL Server Management Studio から **Stretch Database モニター** で確認することも、 **sys.dm_db_rda_migration_status** ビューでクエリを実行して確認することもできます。 詳細については、「 [データ移行の監視とトラブルシューティング](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) 」または「 [sys.dm_db_rda_migration_status](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md)」を参照してください。  
  
3. テーブルに適用するフィルター関数を作成します。  
  
4. 関数をテーブルに追加し、Azure へのデータ移行を再開します。  
  
    ```sql  
    ALTER TABLE <table name>  
        SET ( REMOTE_DATA_ARCHIVE  
            (           
                FILTER_PREDICATE = <predicate>,  
                MIGRATION_STATE = OUTBOUND  
            )  
            );   
    ```  
  
## <a name="filter-rows-by-date"></a>日付による行のフィルター  
 次の例では、 **date** 列に 2016 年 1 月 1 日より前の値が含まれている行を移行します。  
  
```sql  
-- Filter by date  
--  
CREATE FUNCTION dbo.fn_stretch_by_date(@date datetime2)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
       RETURN SELECT 1 AS is_eligible WHERE @date < CONVERT(datetime2, '1/1/2016', 101)  
GO  
  
```  
  
## <a name="filter-rows-by-the-value-in-a-status-column"></a>status 列の値による行のフィルター  
 次の例では、 **status** 列に指定した値のいずれかが含まれている行を移行します。  
  
```sql  
-- Filter by status column  
--  
CREATE FUNCTION dbo.fn_stretch_by_status(@status nvarchar(128))  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
       RETURN SELECT 1 AS is_eligible WHERE @status IN (N'Completed', N'Returned', N'Cancelled')  
GO  
  
```  
  
## <a name="filter-rows-by-using-a-sliding-window"></a>スライディング ウィンドウを使用した行のフィルター  
 スライディング ウィンドウを使用して行をフィルター処理する場合は、フィルター関数の次の要件に注意してください。  
  
-   関数は決定論的である必要があります。 そのため、時間の経過に伴って、スライディング ウィンドウを自動的に再計算する関数を作成することはできません。  
  
-   関数ではスキーマ バインドを使用します。 そのため、 **ALTER FUNCTION** を呼び出してスライディング ウィンドウを移動することで、"配置済みの" 関数を毎日更新することはできません。  
  
 **systemEndTime** 列に 2016 年 1 月 1 日より前の値が含まれている行を移行する、次の例のようなフィルター関数から始めます。  
  
```sql  
CREATE FUNCTION dbo.fn_StretchBySystemEndTime20160101(@systemEndTime datetime2)   
RETURNS TABLE   
WITH SCHEMABINDING    
AS    
RETURN SELECT 1 AS is_eligible   
  WHERE @systemEndTime < CONVERT(datetime2, '2016-01-01T00:00:00', 101) ;  
  
```  
  
 フィルター関数をテーブルに適用します。  
  
```sql  
ALTER TABLE <table name>   
SET (   
        REMOTE_DATA_ARCHIVE = ON   
                (   
                        FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20160101(SysEndTime)  
                                , MIGRATION_STATE = OUTBOUND   
                )  
        )   
;  
  
```  
  
 スライディング ウィンドウを更新する場合は、次の手順に従います。  
  
1.  新しいスライディング ウィンドウを指定する新しい関数を作成します。 次の例では、2016 年 1 月 1 日ではなく、2016 年 1 月 2日より前の日付を選択します。  
  
2.  次の例に示すように、 **ALTER TABLE**を呼び出して、以前のフィルター関数を新しい関数で置き換えます。  
  
3.  必要に応じて、 **DROP FUNCTION**を呼び出して不要になった以前のフィルター関数を削除します。 (この手順は例には含まれていません)。  
  
```sql  
BEGIN TRAN  
GO  
        /*(1) Create new predicate function definition */  
        CREATE FUNCTION dbo.fn_StretchBySystemEndTime20160102(@systemEndTime datetime2)  
        RETURNS TABLE  
        WITH SCHEMABINDING   
        AS   
        RETURN SELECT 1 AS is_eligible  
               WHERE @systemEndTime < CONVERT(datetime2,'2016-01-02T00:00:00', 101)  
        GO  
  
        /*(2) Set the new function as the filter predicate */  
        ALTER TABLE <table name>  
        SET   
        (  
               REMOTE_DATA_ARCHIVE = ON  
               (  
                       FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20160102(SysEndTime),  
                       MIGRATION_STATE = OUTBOUND  
               )  
        )   
COMMIT ;  
  
```  
  
## <a name="more-examples-of-valid-filter-functions"></a>有効なフィルター関数のその他の例  
  
-   次の例では、AND 論理演算子を使用して 2 つのプリミティブ条件を結合しています。  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate((@column1 datetime, @column2 nvarchar(15))  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
      WHERE @column1 < N'20150101' AND @column2 IN (N'Completed', N'Returned', N'Cancelled')  
    GO  
  
    ALTER TABLE table1 SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(date, shipment_status),  
        MIGRATION_STATE = OUTBOUND  
    ) )  
  
    ```  
  
-   次の例では、複数の条件と CONVERT による決定論的変換を使用しています。  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example1(@column1 datetime, @column2 int, @column3 nvarchar)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2015', 101) AND (@column2 < -100 OR @column2 > 100 OR @column2 IS NULL) AND @column3 IN (N'Completed', N'Returned', N'Cancelled')  
    GO  
  
    ```  
  
-   次の例では、算術演算子と関数を使用しています。  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example2(@column1 float)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < SQRT(400) + 10  
    GO  
  
    ```  
  
-   次の例では、BETWEEN 演算子と NOT BETWEEN 演算子を使用しています。 BETWEEN 演算子と NOT BETWEEN 演算子を同等の AND 式と OR 式に置き換えた後、結果的に作成される関数がここで説明するルールに準拠するため、この使用方法は有効です。  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example3(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 BETWEEN 0 AND 100  
                AND (@column2 NOT BETWEEN 200 AND 300 OR @column1 = 50)  
    GO  
  
    ```  
  
     BETWEEN 演算子と NOT BETWEEN 演算子を同等の AND 式と OR 式に置き換えた結果、置換前の関数は置換後の関数と等しくなっています。  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example4(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 >= 0 AND @column1 <= 100 AND (@column2 < 200 OR @column2 > 300 OR @column1 = 50)  
    GO  
  
    ```  
  
## <a name="examples-of-filter-functions-that-arent-valid"></a>無効なフィルター関数の例  
  
-   非決定論的変換が含まれているため、次の関数は無効です。  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example5(@column1 datetime)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < CONVERT(datetime, '1/1/2016')  
    GO  
  
    ```  
  
-   非決定論的な関数呼び出しが含まれているため、次の関数は無効です。  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example6(@column1 datetime)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < DATEADD(day, -60, GETDATE())  
    GO  
  
    ```  
  
-   サブクエリが含まれているため、次の関数は無効です。  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example7(@column1 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 IN (SELECT SupplierID FROM Supplier WHERE Status = 'Defunct')  
    GO  
  
    ```  
  
-   関数を定義するときに、代数演算子または組み込み関数を使用する式は定数に評価する必要があるため、次の関数は無効です。 代数式や関数呼び出しに列参照を含めることはできません。  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example8(@column1 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 % 2 =  0  
    GO  
  
    CREATE FUNCTION dbo.fn_example9(@column1 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE SQRT(@column1) = 30  
    GO  
  
    ```  
  
-   BETWEEN 演算子を同等の AND 式に置き換えると、ここで説明するルールに違反するため、次の関数は無効です。  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example10(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING  
    AS  
    RETURN  SELECT 1 AS is_eligible  
            WHERE (@column1 BETWEEN 1 AND 200 OR @column1 = 300) AND @column2 > 1000  
    GO  
  
    ```  
  
     BETWEEN 演算子を同等の AND 式に置き換えた結果、置換前の関数は置換後の関数と等しくなっています。 プリミティブ条件で使用できるのは OR 論理演算子だけであるため、この関数は無効です。  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example11(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE (@column1 >= 1 AND @column1 <= 200 OR @column1 = 300) AND @column2 > 1000  
    GO  
  
    ```  
  
## <a name="how-stretch-database-applies-the-filter-function"></a>Stretch Database がフィルター関数を適用するしくみ  
 Stretch Database では、CROSS APPLY 演算子を使用してテーブルにフィルター関数を適用し、対象となる行を決定します。 例:  
  
```sql  
SELECT * FROM stretch_table_name CROSS APPLY fn_stretchpredicate(column1, column2)  
```  
  
 関数から行の空ではない結果が返された場合、その行は移行の対象になります。  
  
## <a name="replacePredicate"></a>既存のフィルター関数の置き換え  
 以前に指定したフィルター関数を置き換えるには、 **ALTER TABLE** ステートメントをもう一度実行し、 **FILTER_PREDICATE** パラメーターに新しい値を指定します。 例:  
  
```sql  
ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
    FILTER_PREDICATE = dbo.fn_stretchpredicate2(column1, column2),  
    MIGRATION_STATE = <desired_migration_state>  
  
```  
  
 新しいインライン テーブル値関数には、次の要件があります。  
  
-   新しい関数では、前の関数よりも制約を減らす必要があります。  
  
-   古い関数に含まれていたすべての演算子を新しい関数に含める必要があります。  
  
-   古い関数に含まれていない演算子を新しい関数に含めることはできません。  
  
-   演算子の引数の順序は変更できません。  
  
-   `<, <=, >, >=`  比較に含まれる定数値のみ、関数の制約が減るように変更できます。  
  
### <a name="example-of-a-valid-replacement"></a>有効な置換の例  
 次の関数が現在のフィルター関数であると仮定します。  
  
```sql  
CREATE FUNCTION dbo.fn_stretchpredicate_old(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
            AND (@column2 < -100 OR @column2 > 100)  
GO  
  
```  
  
 (元の決算日よりも後の日付を指定した) 新しい日付定数によって関数の制約が減るため、次の関数は有効な置換です。  
  
```sql  
CREATE FUNCTION dbo.fn_stretchpredicate_new(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '2/1/2016', 101)  
            AND (@column2 < -50 OR @column2 > 50)  
GO  
  
```  
  
### <a name="examples-of-replacements-that-arent-valid"></a>無効な置換の例  
 (元の決算日よりも前の日付を指定した) 新しい日付定数によって関数の制約が減らないため、次の関数は無効な置換です。  
  
```sql  
CREATE FUNCTION dbo.fn_notvalidreplacement_1(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2015', 101)  
            AND (@column2 < -100 OR @column2 > 100)  
GO  
  
```  
  
 比較演算子の 1 つが削除されているため、次の関数は無効な置換です。  
  
```sql  
CREATE FUNCTION dbo.fn_notvalidreplacement_2(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
            AND (@column2 < -50)  
GO  
  
```  
  
 AND 論理演算子を使用して新しい条件が追加されているため、次の関数は無効な置換です。  
  
```sql  
CREATE FUNCTION dbo.fn_notvalidreplacement_3(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
            AND (@column2 < -100 OR @column2 > 100)  
            AND (@column2 <> 0)  
GO  
  
```  
  
## <a name="remove-a-filter-function-from-a-table"></a>テーブルからのフィルター関数の削除  
 選択した行ではなく、テーブル全体を移行するには、 **FILTER_PREDICATE**  を null に設定して既存の関数を削除します。 例:  
  
```sql  
ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
    FILTER_PREDICATE = NULL,  
    MIGRATION_STATE = <desired_migration_state>  
) )  
  
```  
  
 フィルター関数を削除すると、テーブルのすべての行が移行の対象になります。 そのため、Azure からテーブルのすべてのリモート データを先に戻しておかない限り、後で同じテーブルにフィルター関数を指定することはできません。 この制限は、新しいフィルター関数を指定したときに移行の対象外になっている行が既に Azure に移行されているという状況を回避するために設けられています。  
  
## <a name="check-the-filter-function-applied-to-a-table"></a>テーブルに適用されたフィルター関数の確認  
 テーブルに適用されたフィルター関数を確認するには、カタログ ビュー **sys.remote_data_archive_tables** を開き、 **filter_predicate** 列の値を確認します。 値が null の場合、テーブル全体がアーカイブの対象になります。 詳細については、「[sys.remote_data_archive_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md)」を参照してください。  
  
## <a name="security-notes-for-filter-functions"></a>フィルター関数のセキュリティに関する注意事項  
db_owner 権限を持つ侵害されたアカウントは、次の操作を実行できます。  
  
-   大量のサーバー リソースを消費したり、長期間にわたって待機したりするテーブル値関数を作成し適用して、サービス拒否攻撃を仕掛ける。  
  
-   読み取りアクセスを明示的に拒否されているユーザーが、テーブルの内容を推測できるようにするテーブル値関数を作成して適用する。  
  
## <a name="see-also"></a>参照  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
