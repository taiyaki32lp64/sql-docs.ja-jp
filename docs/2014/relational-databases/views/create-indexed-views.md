---
title: インデックス付きビューの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexed views [SQL Server], creating
- clustered indexes, views
- CREATE INDEX statement
- large_value_types_out_of_row option
- indexed views [SQL Server]
- views [SQL Server], indexed views
ms.assetid: f86dd29f-52dd-44a9-91ac-1eb305c1ca8d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2159178c2fd26aca54d099f7345dbb62039ee34e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68196429"
---
# <a name="create-indexed-views"></a>インデックス付きビューの作成
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で、 [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用し、インデックス付きビューを作成する方法について説明します。 ビューに作成する最初のインデックスは、一意なクラスター化インデックスにする必要があります。 一意のクラスター化インデックスを作成した後は、非クラスター化インデックスを追加で作成できます。 ビューに一意のクラスター化インデックスを作成すると、そのビューは、クラスター化インデックスが定義されているテーブルと同じ方法でデータベースに格納されるので、クエリのパフォーマンスが向上します。 クエリ オプティマイザーではインデックス付きビューを使って、クエリの実行速度を高めることができます。 オプティマイザーでビューを代用するかどうかを判別するために、ビューがクエリで参照されている必要はありません。  
  
  
  
##  <a name="BeforeYouBegin"></a> はじめに  
 次の手順は、インデックス付きビューの作成に必要な手順であり、インデックス付きビューの正常な実装に不可欠です。  
  
1.  SET オプションが、ビューで参照されるすべての既存のテーブルに対して正しいことを確認します。  
  
2.  テーブルやビューを作成する前に、そのセッション用の SET オプションが正しく設定されていることを確認します。  
  
3.  ビュー定義が決定的であることを確認します。  
  
4.  WITH SCHEMABINDING オプションを使ってビューを作成します。  
  
5.  ビューに一意のクラスター化インデックスを作成します。  
  
###  <a name="Restrictions"></a> インデックス付きビューに必要な SET オプション  
 クエリの実行時、異なる SET オプションがアクティブになっている場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は同じ式を評価しても異なる結果を生成することがあります。 たとえば、SET オプションの CONCAT_NULL_YIELDS_NULL を ON に設定した後、式 **'** abc **'** + NULL を実行すると NULL 値が返されます。 CONCAT_NULL_YIELDS_NULL を OFF に設定した後、同じ式を実行すると値 **'** abc **'** が返されます。  
  
 ビューが正しく維持され、一貫性のある結果が返されるようにするには、インデックス付きビューで、いくつかの SET オプションに固定値が必要となります。 次の表の SET オプションに表示される値に設定する必要があります、 **RequiredValue**次の条件が発生するたびに、列。  
  
-   ビューが作成され、そのビューのインデックスも作成されている。  
  
-   テーブルの作成時にビューで参照されるベース テーブル。  
  
-   インデックス付きビューに関与するテーブルで実行される挿入、更新、または削除操作がある。 この要件には一括コピー、レプリケーション、分散クエリなどの操作も含まれます。  
  
-   クエリ オプティマイザーで、クエリ プランの生成にインデックス付きビューが使用される。  
  
    |SET オプション|必要な値|既定のサーバー値|既定<br /><br /> OLE DB および ODBC 値|既定<br /><br /> DB-Library 値|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ON|ON|ON|OFF|  
    |ANSI_PADDING|ON|ON|ON|OFF|  
    |ANSI_WARNINGS*|ON|ON|ON|OFF|  
    |ARITHABORT|ON|ON|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ON|ON|ON|OFF|  
  
     *ANSI_WARNINGS を ON に設定すると、ARITHABORT は暗黙的に ON に設定されます。  
  
 OLE DB または ODBC サーバー接続を使用している場合、変更する必要があるのは ARITHABORT 設定の値だけです。 すべての DB-Library 値は、サーバー レベルで **sp_configure** を使用するか、アプリケーションから SET コマンドを使用して、正しく設定する必要があります。  
  
> [!IMPORTANT]  
>  ARITHABORT ユーザー オプションは、そのサーバーのデータベースで初めてインデックス付きビューまたは計算列のインデックスが作成されたときすぐに、サーバー全体で ON に設定することを強くお勧めします。  
  
### <a name="deterministic-views"></a>決定的なビュー  
 インデックス付きビューの定義は決定的である必要があります。 選択リストのすべての式と、WHERE 句および GROUP BY 句が決定的である場合、ビューは決定的であるといえます。 決定的な式では、特定の入力値セットで評価するとき常に同じ結果が返されます。 決定的な式には、決定的な関数のみを含めることができます。 たとえば、DATEADD 関数は、3 つのパラメーターの任意の引数値セットに対して常に同じ結果を返すため、決定的であるといえます。 GETDATE は、常に同じ引数で起動されるにもかかわらず、返す値は実行のたびに変化するため、非決定的であるといえます。  
  
 ビュー列が決定的かどうかを判断するには、 **COLUMNPROPERTY** 関数の [IsDeterministic](/sql/t-sql/functions/columnproperty-transact-sql) プロパティを使用します。 スキーマ バインドを含むビューの決定的な列が正確であるかどうかを判断するには、COLUMNPROPERTY 関数の **IsPrecise** プロパティを使用します。 COLUMNPROPERTY では、TRUE の場合は 1、FALSE の場合は 0、有効でない入力に対しては NULL が返されます。 これは、列が決定的でないか、正確でないことを表します。  
  
 式が決定的でも、浮動小数点式が含まれる場合は、正確な結果はプロセッサのアーキテクチャまたはマイクロコードのバージョンによって異なる可能性があります。 データの整合性を確保するため、このような式は、インデックス付きビューの非キー列としてのみ含めることができます。 浮動小数点式を含まない決定的な式は、正確な式です。 インデックス ビューのキー列と WHERE または GROUP BY 句には、正確で決定的な式だけを含めることができます。  
  
### <a name="additional-requirements"></a>その他の要件  
 SET オプションと決定的な関数の要件に加えて、次の要件を満たす必要があります。  
  
-   CREATE INDEX を実行するユーザーが、ビューの所有者であること。  
  
-   インデックスを作成する場合は、IGNORE_DUP_KEY オプションを OFF に設定する必要があります (既定の設定)。  
  
-   ビュー定義では、 _schema_ **.** _tablename_ という 2 つの部分から構成される名前でテーブルが参照されていること。  
  
-   ビューで参照されているユーザー定義関数が、WITH SCHEMABINDING オプションを使用して作成されていること。  
  
-   ビューで参照されているユーザー定義関数が、 _schema_ **.** _function_という 2 つの部分から構成される名前で参照されていること。  
  
-   ユーザー定義関数のデータ アクセス プロパティが NO SQL に、外部アクセス プロパティが NO に設定されている必要があります。  
  
-   共通言語ランタイム (CLR) 関数をビューの選択リストに使用することはできますが、クラスター化インデックス キーの定義に含めることはできません。 CLR 関数は、ビューの WHERE 句や、ビューの JOIN 操作の ON 句では使用できません。  
  
-   ビュー定義で使用する CLR ユーザー定義型の CLR 関数やメソッドは、次の表のようにプロパティが設定されている必要があります。  
  
    |プロパティ|注|  
    |--------------|----------|  
    |DETERMINISTIC = TRUE|Microsoft .NET Framework メソッドの属性として、明示的に宣言する必要があります。|  
    |PRECISE = TRUE|.NET Framework メソッドの属性として、明示的に宣言する必要があります。|  
    |DATA ACCESS = NO SQL|DataAccess 属性を DataAccessKind.None に、SystemDataAccess 属性を SystemDataAccessKind.None に設定することで決定されます。|  
    |EXTERNAL ACCESS = NO|CLR ルーチンの場合は、このプロパティの既定値は NO です。|  
  
-   ビューが、WITH SCHEMABINDING オプションを使って作成されていること。  
  
-   ビューが、ビューと同じデータベース内のベース テーブルのみを参照していること。 ビューでは、他のビューを参照できません。  
  
-   ビュー定義の SELECT ステートメントには、次の Transact-SQL 要素を使用できません。  
  
    ||||  
    |-|-|-|  
    |[COUNT]|行セット関数 (OPENDATASOURCE、OPENQUERY、OPENROWSET、および OPENXML)|外部結合 (LEFT、RIGHT、または FULL)|  
    |派生テーブル (FROM 句で SELECT ステートメントを指定することで定義される)|自己結合|SELECT \* または SELECT *table_name*を使用して、列を指定します。*|  
    |DISTINCT|STDEV、STDEVP、VAR、VARP、または AVG|共通テーブル式 (CTE)|  
    |`float`\*、 `text`、 `ntext`、 `image`、 `XML`、または`filestream`列|サブクエリ|順位付け関数または集計関数が含まれている OVER 句|  
    |フルテキスト述語 (CONTAIN、FREETEXT)|NULL 値を許容する式を参照する SUM 関数|ORDER BY|  
    |CLR ユーザー定義集計関数|TOP|CUBE、ROLLUP、または GROUPING SETS 演算子|  
    |MIN、MAX|UNION、EXCEPT、または INTERSECT 演算子。|TABLESAMPLE|  
    |テーブル変数|OUTER APPLY または CROSS APPLY|PIVOT、UNPIVOT|  
    |スパース列セット|インラインまたは複数ステートメントのテーブル値関数|OFFSET|  
    |CHECKSUM_AGG|||  
  
     \*インデックス付きビューに含めることができます`float`列。 ただし、このような列はクラスター化インデックス キーに含めることができません。  
  
-   GROUP BY が存在する場合、VIEW 定義には COUNT_BIG(*) を含める必要があります。HAVING を含めることはできません。 このような GROUP BY 制限は、インデックス付きビュー定義にのみ適用されます。 クエリがこの GROUP BY 制限を満たしていない場合でも、実行プランでインデックス付きビューを使用することはできます。  
  
-   ビュー定義に GROUP BY 句を指定した場合、一意のクラスター化インデックスのキーでは、GROUP BY 句で指定した列のみを参照できること。  
  
###  <a name="Recommendations"></a> 推奨事項  
 インデックス付きビューで `datetime` 文字リテラルと `smalldatetime` 文字列リテラルを参照するときは、決定的な日付形式スタイルを使用して、そのリテラルを目的の日付型に明示的に変換することをお勧めします。 決定的な日付形式の一覧については、「[CAST および CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)」を参照してください。 `datetime` 型または `smalldatetime` 型への文字列の暗黙的な変換が必要な式は非決定的であると見なされます。 これは、サーバー セッションの LANGUAGE および DATEFORMAT の設定によって結果が異なるためです。 たとえば、式 `CONVERT (datetime, '30 listopad 1996', 113)` では、言語が異なると文字列 '`listopad`' が異なる月を意味するので、結果が LANGUAGE の設定によって異なります。 同様に、式 `DATEADD(mm,3,'2000-12-01')`の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では DATEFORMAT の設定に基づいて、文字列 `'2000-12-01'` が解釈されます。  
  
 照合順序間で行われる Unicode 以外の文字データの暗黙的な変換も非決定的であると見なされます。  
  
###  <a name="Considerations"></a> 考慮事項  
 インデックス付きビューの列の **large_value_types_out_of_row** オプションの設定は、ベース テーブルの対応する列の設定が継承されます。 この値は、 [sp_tableoption](/sql/relational-databases/system-stored-procedures/sp-tableoption-transact-sql)を使用して設定します。 式から形成される列に対する既定の設定は 0 です。 つまり、大きい値の型は行内に格納されます。  
  
 インデックス付きビューはパーティション分割されたテーブルに作成でき、インデックス付きビュー自体をパーティション分割できます。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] でインデックス付きビューが使用されないようにするには、クエリに OPTION (EXPAND VIEWS) ヒントを含めます。 これによって、オプションの 1 つが正しく設定されていない場合、オプティマイザーもビューのインデックスを使用できません。 OPTION (EXPAND VIEWS) ヒントの詳細については、「[SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)」を参照してください。  
  
 ビューが削除されると、ビューのすべてのインデックスも削除されます。 クラスター化インデックスが削除されると、ビューのすべての非クラスター化インデックスと自動的に作成された統計も削除されます。 ユーザーが作成したビューの統計は、保持されます。 非クラスター化インデックスは、個別に削除できます。 ビュー上のクラスター化インデックスを削除すると、格納された結果セットも削除され、オプティマイザーは、ビューの処理を標準的なビューと同様の処理に戻します。  
  
 テーブルとビューのインデックスは無効にされる可能性があります。 テーブルのクラスター化インデックスが無効になると、そのテーブルに関連するビューのインデックスも無効になります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースの CREATE VIEW 権限と、ビューが作成されているスキーマの ALTER 権限が必要です。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-an-indexed-view"></a>インデックス付きビューを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、ビューとそのビューのインデックスを作成します。 ここでは、インデックス付きビューを使用する 2 つのクエリを実行します。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    --Set the options to support indexed views.  
    SET NUMERIC_ROUNDABORT OFF;  
    SET ANSI_PADDING, ANSI_WARNINGS, CONCAT_NULL_YIELDS_NULL, ARITHABORT,  
        QUOTED_IDENTIFIER, ANSI_NULLS ON;  
    GO  
    --Create view with schemabinding.  
    IF OBJECT_ID ('Sales.vOrders', 'view') IS NOT NULL  
    DROP VIEW Sales.vOrders ;  
    GO  
    CREATE VIEW Sales.vOrders  
    WITH SCHEMABINDING  
    AS  
        SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Revenue,  
            OrderDate, ProductID, COUNT_BIG(*) AS COUNT  
        FROM Sales.SalesOrderDetail AS od, Sales.SalesOrderHeader AS o  
        WHERE od.SalesOrderID = o.SalesOrderID  
        GROUP BY OrderDate, ProductID;  
    GO  
    --Create an index on the view.  
    CREATE UNIQUE CLUSTERED INDEX IDX_V1   
        ON Sales.vOrders (OrderDate, ProductID);  
    GO  
    --This query can use the indexed view even though the view is   
    --not specified in the FROM clause.  
    SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev,   
        OrderDate, ProductID  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND ProductID BETWEEN 700 and 800  
            AND OrderDate >= CONVERT(datetime,'05/01/2002',101)  
    GROUP BY OrderDate, ProductID  
    ORDER BY Rev DESC;  
    GO  
    --This query can use the above indexed view.  
    SELECT  OrderDate, SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND DATEPART(mm,OrderDate)= 3  
            AND DATEPART(yy,OrderDate) = 2002  
    GROUP BY OrderDate  
    ORDER BY OrderDate ASC;  
    GO  
    ```  
  
 詳細については、「[CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)   
 [SET ARITHABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql)   
 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql)   
 [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-numeric-roundabort-transact-sql)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql)  
  
  
