---
title: 一時テーブルとテーブル変数の高速化のためのメモリ最適化
ms.custom: seo-dt-2019
ms.date: 06/01/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 38512a22-7e63-436f-9c13-dde7cf5c2202
author: Jodebrui
ms.author: jodebrui
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 833108cfc5e8a11f72e8b7cb7b628690b0050c58
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412680"
---
# <a name="faster-temp-table-and-table-variable-by-using-memory-optimization"></a>メモリ最適化を使用した一時テーブルとテーブル変数の高速化
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  
一時テーブル、テーブル変数、またはテーブル値パラメーターを使用する場合は、パフォーマンスを向上させるために、これらを変換してメモリ最適化テーブルとテーブル変数を活用することを検討してください。 通常、コードの変更はわずかです。  
  
この記事では、次の内容について説明します。  
  
- メモリ内への変換を優先すると主張するシナリオ  
- メモリ内への変換を実装するための技術的な手順  
- メモリ内に変換する前の前提条件  
- メモリ最適化のパフォーマンスの利点を強調表示するコード サンプル
  
  
## <a name="a-basics-of-memory-optimized-table-variables"></a>A. メモリ最適化テーブル変数の基本  
  
メモリ最適化テーブル変数は、メモリ最適化テーブルで使用されるのと同じメモリ最適化アルゴリズムとデータ構造を使用して、優れた効率性を提供します。 テーブル変数がネイティブ コンパイル モジュール内からアクセスされる場合に、効率が最大限になります。  
  
  
メモリ最適化テーブル変数:  
  
- メモリ内にのみ格納され、ディスク上にコンポーネントはありません。  
- IO アクティビティは関係しません。  
- tempdb の使用率または競合は関係しません。  
- テーブル値パラメーター (TVP) としてストアド プロシージャに渡すことができます。  
- ハッシュまたは非クラスター化の少なくとも 1 つのインデックスがある必要があります。  
  - ハッシュ インデックスの場合、バケット数は予期される一意のインデックス キーの数の 1 ～ 2 倍にするのが理想的ですが、バケット数を多めに設定しても通常は問題ありません (最大 10 倍)。 詳細については、「 [Indexes for Memory-Optimized Tables](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)」 (メモリ最適化テーブルのインデックス) をご覧ください。  

  
  
#### <a name="object-types"></a>オブジェクトの型  
  
インメモリ OLTP では、メモリ最適化一時テーブルおよびテーブル変数に使用できる次のオブジェクトを提供します。  
  
- メモリ最適化テーブル  
  - Durability = SCHEMA_ONLY  
- メモリ最適化テーブル変数  
  - 次の 2 つの手順 (インラインでなく) で宣言する必要があります。  
    - `CREATE TYPE my_type AS TABLE ...;` 、その後  
    - [https://login.microsoftonline.com/consumers/](`DECLARE @mytablevariable my_type;`)  
  
  
## <a name="b-scenario-replace-global-tempdb-x23x23table"></a>B. シナリオ:グローバル tempdb &#x23;&#x23;table の置換  
  
グローバル一時テーブルとメモリ最適化 SCHEMA_ONLY テーブルの置換は非常に単純です。 最大の変更は、テーブルを実行時ではなく展開時に作成することです。 メモリ最適化テーブルの作成は、コンパイル時に最適化されるため、従来のテーブルの作成よりも時間がかかります。 メモリ最適化テーブルをオンライン ワークロードの一部として作成およびドロップすると、ワークロードのパフォーマンスだけでなく、AlwaysOn セカンダリおよびデータベース復旧の再実行のパフォーマンスにも影響します。

次のグローバル一時テーブルがあると想定します。  
  
  
```sql
CREATE TABLE ##tempGlobalB  
    (  
        Column1   INT   NOT NULL ,  
        Column2   NVARCHAR(4000)  
    );  
```
  
  
  
DURABILITY = SCHEMA_ONLY を含む、次のメモリ最適化テーブルを使用して、グローバル一時テーブルを置換することを検討します。  
  
  
  
```sql
CREATE TABLE dbo.soGlobalB  
(  
    Column1   INT   NOT NULL   INDEX ix1 NONCLUSTERED,  
    Column2   NVARCHAR(4000)  
)  
    WITH  
        (MEMORY_OPTIMIZED = ON,  
        DURABILITY        = SCHEMA_ONLY);  
```  
  
  
  
#### <a name="b1-steps"></a>B.1 手順  
  
グローバル一時から SCHEMA_ONLY へ変換する手順は、次のとおりです。  
  
  
1. 従来のディスク上のテーブルと同様に、一度、**dbo.soGlobalB** テーブルを作成します。  
2. Transact-SQL から、 **&#x23;&#x23;tempGlobalB** テーブルの作成を削除します。  テーブルの作成から生じるコンパイルのオーバーヘッドを回避するには、メモリ最適化テーブルを実行時ではなく展開時に作成することが重要です。
3. T-SQL で、 **&#x23;&#x23;tempGlobalB** のすべてのメンションを **dbo.soGlobalB** に置き換えます。  
  
  
## <a name="c-scenario-replace-session-tempdb-x23table"></a>C. シナリオ:セッション tempdb &#x23;table の置換  
  
セッションの一時テーブルを置換するための準備には、以前のグローバル一時テーブルのシナリオよりも多く T-SQL が含まれます。 追加の T-SQL で、変換を行うために必要な労力が増えるということではありません。  

グローバル一時テーブルのシナリオと同様、最も大きな変更はコンパイルのオーバーヘッドを回避するため、テーブルを実行時ではなく展開時に作成することです。
  
次のセッションの一時テーブルがあると想定します。  
  
  
  
```sql  
CREATE TABLE #tempSessionC  
(  
    Column1   INT   NOT NULL ,  
    Column2   NVARCHAR(4000)  
);  
```
  
  
  
まず、次のテーブル値関数を作成して、 **\@\@spid** にフィルターを適用します。 この関数は、セッションの一時テーブルから変換するすべての SCHEMA_ONLY テーブルで使用可能になります。  
  
  
  
```sql  
CREATE FUNCTION dbo.fn_SpidFilter(@SpidFilter smallint)  
    RETURNS TABLE  
    WITH SCHEMABINDING , NATIVE_COMPILATION  
AS  
    RETURN  
        SELECT 1 AS fn_SpidFilter  
            WHERE @SpidFilter = @@spid;  
```
  
  
  
次に、テーブルのセキュリティ ポリシーに加えて、SCHEMA_ONLY テーブルを作成します。  
  
  
それぞれのメモリ最適化テーブルには、1 つ以上のインデックスが必要なことに注意してください。  
  
- テーブル dbo.soSessionC では、適切な BUCKET_COUNT を計算する場合、HASH インデックスが望ましいことがあります。 ただし、このサンプルでは、NONCLUSTERED インデックスに簡略化します。  
  
  
  
```sql
CREATE TABLE dbo.soSessionC  
(  
    Column1     INT         NOT NULL,  
    Column2     NVARCHAR(4000)  NULL,  

    SpidFilter  SMALLINT    NOT NULL   DEFAULT (@@spid),  

    INDEX ix_SpidFiler NONCLUSTERED (SpidFilter),  
    --INDEX ix_SpidFilter HASH  
    --    (SpidFilter) WITH (BUCKET_COUNT = 64),  
        
    CONSTRAINT CHK_soSessionC_SpidFilter  
        CHECK ( SpidFilter = @@spid ),  
)  
    WITH  
        (MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA_ONLY);  
go  
  
  
CREATE SECURITY POLICY dbo.soSessionC_SpidFilter_Policy  
    ADD FILTER PREDICATE dbo.fn_SpidFilter(SpidFilter)  
    ON dbo.soSessionC  
    WITH (STATE = ON);  
go  
```  
  
  
  
その次に、一般的な T-SQL コードで、  
  
1. Transact-SQL ステートメントの一時テーブルのすべての参照をメモリ最適化テーブルに変更します。
    - _旧:_ &#x23;tempSessionC  
    - _新:_ dbo.soSessionC  
2. コードの `CREATE TABLE #tempSessionC` ステートメントを `DELETE FROM dbo.soSessionC` に置換し、同じ session_id の前のセッションにより挿入されるテーブル コンテンツにセッションが公開されないようにします。 テーブルの作成から生じるコンパイルのオーバーヘッドを回避するには、メモリ最適化テーブルを実行時ではなく展開時に作成することが重要です。
3. コードから `DROP TABLE #tempSessionC` ステートメントを削除します。メモリ サイズが問題となる可能性がある場合、任意で `DELETE FROM dbo.soSessionC` ステートメントを挿入できます。
  
  
  
  
## <a name="d-scenario-table-variable-can-be-memory_optimizedon"></a>D. シナリオ:テーブル変数は MEMORY_OPTIMIZED=ON にすることができます  
  
  
従来のテーブル変数は、tempdb データベース内のテーブルを表します。 パフォーマンスが高速化するには、テーブル変数のメモリを最適化することができます。  
  
従来のテーブル変数の T-SQL を次に示します。 バッチまたはセッションのいずれかが終了すると、そのスコープが終了します。  
  
  
  
```sql
DECLARE @tvTableD TABLE  
    ( Column1   INT   NOT NULL ,  
      Column2   CHAR(10) );  
```
  
  
  
#### <a name="d1-convert-inline-to-explicit"></a>D.1 インラインを明示的に変換  
  
上記の構文は、テーブル変数 *inline*を作成すると考えられます。 インライン構文は、メモリ最適化をサポートしません。 そのため、インライン構文を TYPE の明示的な構文に変換します。  
  
*スコープ:* 最初の go の区切り文字のバッチによって作成された TYPE 定義は、サーバーがシャットダウンして再起動された後でも保持されます。 ただし、最初の go 区切り文字の後に、宣言されたテーブル @tvTableC は、次の go に到達してバッチが終了するまでのみ保持されます。  
  
  
  
```sql  
CREATE TYPE dbo.typeTableD  
    AS TABLE  
    (  
        Column1  INT   NOT NULL ,  
        Column2  CHAR(10)  
    );  
go  
        
SET NoCount ON;  
DECLARE @tvTableD dbo.typeTableD  
;  
INSERT INTO @tvTableD (Column1) values (1), (2)  
;  
SELECT * from @tvTableD;  
go  
```
  
  
  
#### <a name="d2-convert-explicit-on-disk-to-memory-optimized"></a>D.2 ディスク上の明示的をメモリ最適化に変換  
  
メモリ最適化テーブル変数は tempdb 内にありません。 通常、メモリ最適化で速度が 10 倍以上速くなります。  
  
メモリ最適化への変換は、1 つだけの手順で行えます。 明示的な TYPE の作成を次のように強化します。以下を追加します。  
  
- インデックス。 それぞれのメモリ最適化テーブルには、1 つ以上のインデックスが必要です。  
- MEMORY_OPTIMIZED = ON.  
  
  
  
```sql
CREATE TYPE dbo.typeTableD  
    AS TABLE  
    (  
        Column1  INT   NOT NULL   INDEX ix1,  
        Column2  CHAR(10)  
    )  
    WITH  
        (MEMORY_OPTIMIZED = ON);  
```  
  
  
  
完了しました。  
  
  
## <a name="e-prerequisite-filegroup-for-sql-server"></a>E. SQL Server の前提条件となる FILEGROUP  
  
Microsoft SQL Server では、メモリ最適化機能を使用するために、データベースに **MEMORY_OPTIMIZED_DATA**で宣言された FILEGROUP がある必要があります。  
  
- Azure SQL Database では、この FILEGROUP を作成する必要はありません。  
  
  
*前提条件:* 次の FILEGROUP の Transact-SQL コードは、この記事の以降のセクションにある長い T-SQL コード サンプルの前提条件です。  
  
1. SSMS.exe または T-SQL を送信できる他のツールを使用する必要があります。  
2. サンプルの FILEGROUP T-SQL コードを SSMS に貼り付けます。  
3. T-SQL を編集して、自分のリンクへの特定の名前とディレクトリ パスを変更します。  
  - 最後のディレクトリが前から存在する必要がない場合を除いて、FILENAME 値のすべてのディレクトリは前から存在する必要があります。  
4. 編集した T-SQL を実行します。  
  - 次のサブセクションで速度を比較する T-SQL を繰り返し調整および再実行する場合でも、FILEGROUP T-SQL を複数回実行する必要はありません。  
  
  
  
 
```sql
ALTER DATABASE InMemTest2  
    ADD FILEGROUP FgMemOptim3  
        CONTAINS MEMORY_OPTIMIZED_DATA;  
go  
ALTER DATABASE InMemTest2  
    ADD FILE  
    (  
        NAME = N'FileMemOptim3a',  
        FILENAME = N'C:\DATA\FileMemOptim3a'  
                    --  C:\DATA\    preexisted.  
    )  
    TO FILEGROUP FgMemOptim3;  
go  
```  


次のスクリプトでは、お客様のファイルグループを作成し、推奨されるデータベースの設定を構成します ( [enable-in-memory-oltp.sql](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/in-memory-database/in-memory-oltp/t-sql-scripts/enable-in-memory-oltp.sql))。
  
FILE と FILEGROUP の `ALTER DATABASE ... ADD` の詳細については、次を参照してください。  
  
- [ALTER DATABASE の File および Filegroup オプション (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
- [メモリ最適化ファイルグループ](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)    
  
  
## <a name="f-quick-test-to-prove-speed-improvement"></a>F. 速度の向上を証明するための簡単なテスト  
  
  
このセクションでは、使用しているメモリ最適化テーブル変数から、INSERT-DELETE の速度の向上をテストおよび比較するために実行できるように、Transact-SQL コードを提供します。 このコードは、前半のテーブル型がメモリ最適化である場合を除いて、2 つのほぼ同じ要素で構成されます。  
  
比較テストには、約 7 秒かかります。 サンプルを実行するには  
  
1. *前提条件:* 前のセクションで既に FILEGROUP T-SQL を実行している必要があります。  
2. 次の T-SQL INSERT-DELETE スクリプトを実行します。  
  - 'GO 5001' ステートメントは、T-SQL を 5001 回再送信します。 この数字は調整して、再実行することができます。  
  
Azure SQL Database でスクリプトを実行している場合、同じリージョン内の VM から実行することを確認します。

  
```sql
PRINT ' ';  
PRINT '---- Next, memory-optimized, faster. ----';  

DROP TYPE IF EXISTS dbo.typeTableC_mem;  
go  
CREATE TYPE dbo.typeTableC_mem  -- !!  Memory-optimized.  
        AS TABLE  
        (  
            Column1  INT NOT NULL INDEX ix1,  
            Column2  CHAR(10)  
        )  
        WITH  
            (MEMORY_OPTIMIZED = ON);  
go  
DECLARE @dateString_Begin nvarchar(64) =  
    Convert(nvarchar(64), GetUtcDate(), 121);  
PRINT Concat(@dateString_Begin, '  = Begin time, _mem.');  
go  
SET NoCount ON;  
DECLARE @tvTableC dbo.typeTableC_mem;  -- !!  

INSERT INTO @tvTableC (Column1) values (1), (2);  
INSERT INTO @tvTableC (Column1) values (3), (4);  
DELETE @tvTableC;  

GO 5001  

DECLARE @dateString_End nvarchar(64) =  
    Convert(nvarchar(64), GetUtcDate(), 121);  
PRINT Concat(@dateString_End, '  = End time, _mem.');  
go  
DROP TYPE IF EXISTS dbo.typeTableC_mem;  
go  

---- End memory-optimized.  
-------------------------------------------------  
---- Start traditional on-disk.  

PRINT ' ';  
PRINT '---- Next, tempdb based, slower. ----';  

DROP TYPE IF EXISTS dbo.typeTableC_tempdb;  
go  
CREATE TYPE dbo.typeTableC_tempdb  -- !!  Traditional tempdb.  
    AS TABLE  
    (  
        Column1  INT NOT NULL ,  
        Column2  CHAR(10)  
    );  
go  
DECLARE @dateString_Begin nvarchar(64) =  
    Convert(nvarchar(64), GetUtcDate(), 121);  
PRINT Concat(@dateString_Begin, '  = Begin time, _tempdb.');  
go  
SET NoCount ON;  
DECLARE @tvTableC dbo.typeTableC_tempdb;  -- !!  

INSERT INTO @tvTableC (Column1) values (1), (2);  
INSERT INTO @tvTableC (Column1) values (3), (4);  
DELETE @tvTableC;  

GO 5001  

DECLARE @dateString_End nvarchar(64) =  
    Convert(nvarchar(64), GetUtcDate(), 121);  
PRINT Concat(@dateString_End, '  = End time, _tempdb.');  
go  
DROP TYPE IF EXISTS dbo.typeTableC_tempdb;  
go  
----  

PRINT '---- Tests done. ----';  

go  

/*** Actual output, SQL Server 2016:  

---- Next, memory-optimized, faster. ----  
2016-04-20 00:26:58.033  = Begin time, _mem.  
Beginning execution loop  
Batch execution completed 5001 times.  
2016-04-20 00:26:58.733  = End time, _mem.  

---- Next, tempdb based, slower. ----  
2016-04-20 00:26:58.750  = Begin time, _tempdb.  
Beginning execution loop  
Batch execution completed 5001 times.  
2016-04-20 00:27:05.440  = End time, _tempdb.  
---- Tests done. ----  
***/
```
  
  
  
## <a name="g-predict-active-memory-consumption"></a>G. アクティブなメモリ消費量の予測  
  
次のリソースを使用して、メモリ最適化テーブルの必要なアクティブ メモリを予測する方法を学習できます。  
  
- [メモリ最適化テーブルのメモリ必要量の推定](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)  
- [メモリ最適化テーブルのテーブルと行のサイズ:計算の例](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
より大きなテーブル変数の場合、非クラスター化のインデックスは、メモリ最適化 " *テーブル*" よりも多くメモリを使用します。 行の数やインデックス キーが多くなるほど、その違いは大きくなります。  
  
メモリ最適化テーブル変数がアクセスごとに正確なキー値でのみアクセスされる場合、非クラスター化インデックスよりもハッシュ インデックスを選択する方が望ましい可能性があります。 ただし、適切な BUCKET_COUNT を予想できない場合は、NONCLUSTERED インデックスを選択することをお勧めします。  
  
## <a name="h-see-also"></a>H. 参照  
  
- [メモリ最適化テーブル。](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)

- [メモリ最適化オブジェクトの持続性の定義。](../../relational-databases/in-memory-oltp/defining-durability-for-memory-optimized-objects.md)

- [2017 年 9 月のブログで発表された、不適切なメモリ不足エラーの可能性を除去するための累積的な更新プログラム。](https://support.microsoft.com/help/4025208/fix-memory-leak-occurs-when-you-use-memory-optimized-tables-in-microso)
    - 「[SQL Server 2016 のビルド バージョン](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions)」には、リリース、サービス パック、および累積的な更新プログラムの詳細が示されています。
    - このような不定期の不適切なエラーは、SQL Server Enterprise Edition では発生しませんでした。

