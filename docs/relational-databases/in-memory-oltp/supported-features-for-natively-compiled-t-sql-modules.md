---
title: ネイティブ コンパイル T-SQL モジュール用の機能
ms.custom: seo-dt-2019
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 05515013-28b5-4ccf-9a54-ae861448945b
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 472a654a0bee8b386c6573c8ab1ed8fdb0b4cf8d
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412520"
---
# <a name="supported-features-for-natively-compiled-t-sql-modules"></a>ネイティブ コンパイル T-SQL モジュールでサポートされる機能
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


  このトピックには、T-SQL 領域とネイティブ コンパイル T-SQL モジュールの本体でサポートされる機能が含まれています。ストアド プロシージャ ([CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md))、スカラー ユーザー定義機能、インライン テーブル値関数、トリガーなどです。  

 ネイティブ モジュールの定義でサポートされる機能については、「 [ネイティブ コンパイル T-SQL モジュールでサポートされる DDL](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md)」をご覧ください。  

-   [ネイティブ モジュールのクエリ領域](#qsancsp)  

-   [データの変更](#dml)  

-   [フロー制御言語](#cof)  

-   [サポートされている演算子](#so)  

-   [ネイティブ コンパイル モジュールの組み込み関数](#bfncsp)  

-   [監査](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#auditing)  

-   [テーブル ヒントとクエリ ヒント](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#tqh)  

-   [並べ替えに関する制限事項](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#los)  

 サポートされない構造に関する詳細と、ネイティブ コンパイル モジュールのサポートされない一部の機能に対処する方法については、「 [Migration Issues for Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)」を参照してください。 サポートされていない機能の詳細については、「 [インメモリ OLTP でサポートされていない Transact-SQL の構造](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)」をご覧ください。  

##  <a name="qsancsp"></a> ネイティブ モジュールのクエリ領域  

次のクエリ構造がサポートされます。  

CASE 式: CASE は、有効な式を使用できる任意のステートメントや句で使用できます。
   - **適用対象:** [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]。  
    [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 以降、CASE ステートメントはネイティブ コンパイル T-SQL モジュールに対してサポートされています。

SELECT 句:  

-   列と名前のエイリアス (AS または = 構文を使用)。  

-   スカラー サブクエリ
    - **適用対象:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]。
      [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 以降、スカラー サブクエリはネイティブ コンパイル モジュールでサポートされています。

-   TOP*  

-   SELECT DISTINCT  
    - **適用対象:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]。
      [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 以降、DISTINCT 演算子はネイティブ コンパイル モジュールでサポートされています。

              DISTINCT aggregates are not supported.  

-   UNION および UNION ALL
    - **適用対象:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]。
      [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 以降、UNION および UNION ALL 演算子はネイティブ コンパイル モジュールでサポートされています。

-   変数割り当て  

FROM 句:  

-   FROM \<メモリ最適化テーブルまたはテーブル変数>  

-   FROM \<ネイティブ コンパイル インライン TVF>  

-   LEFT OUTER JOIN、RIGHT OUTER JOIN、CROSS JOIN、INNER JOIN。
    - **適用対象:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]。
      [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 以降、JOINS はネイティブ コンパイル モジュールでサポートされています。

-   サブクエリ `[AS] table_alias`。 詳細については、「[FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)」を参照してください。 
    - **適用対象:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]。
      [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 以降、サブクエリはネイティブ コンパイル モジュールでサポートされています。

WHERE 句:  

-   フィルター述語 IS [NOT] NULL  

-   AND、BETWEEN  
-   OR、NOT、IN、EXISTS
    - **適用対象:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]。
      [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 以降、OR/NOT/IN/EXISTS 演算子はネイティブ コンパイル モジュールでサポートされています。


[GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md) 句:

- 集計関数 AVG、COUNT、COUNT_BIG、MIN、MAX、SUM。  

- MIN および MAX は、nvarchar、char、varchar、varchar、varbinary、および binary 型ではサポートされていません。  

[ORDER BY](../../t-sql/queries/select-order-by-clause-transact-sql.md) 句:


- **ORDER BY** 句での **DISTINCT** のサポートはありません。


- ORDER BY リスト内の式が [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md) リスト内にもそのまま出現する場合は、GROUP BY でサポートされます。
  - たとえば、GROUP BY a + b ORDER BY a + b はサポートされますが、GROUP BY a, b ORDER BY a + b はサポートされません。  


HAVING 句:

- WHERE 句と同じ式の制限が適用されます。


#### <a name="order-by-and-top-are-supported-in-natively-compiled-modules-with-some-restrictions"></a>ORDER BY と TOP はネイティブ コンパイル モジュールでサポートされますが、いくつかの制限があります。


- **WITH TIES** 句での **PERCENT** または **TOP** のサポートはありません。


- **ORDER BY** 句での **DISTINCT** のサポートはありません。  


- **TOP** と **ORDER BY** の組み合わせでは、 **TOP** 句内で定数を使用するときに 8,192 を超える値はサポートされません。
  - クエリに結合または集計関数が含まれている場合は、この制限値がさらに小さくなる場合があります (たとえば、1 回の結合 (2 つのテーブル) では、制限値は 4,096 行です。 2 回の結合 (3 つのテーブル) では、制限値は 2,730 行です)。  
  - 変数内に行の数を格納すると、8,192 より多くの結果を取得できます。  

```sql
DECLARE @v INT = 9000;
SELECT TOP (@v) ... FROM ... ORDER BY ...
```

ただし、変数を使用する場合に比べて、 **TOP** 句内で定数を使用する方がパフォーマンスが向上する結果になります。  

ネイティブにコンパイルされる [!INCLUDE[tsql](../../includes/tsql-md.md)] でのこれらの制限は、インタープリターによって処理される [!INCLUDE[tsql](../../includes/tsql-md.md)] によるメモリ最適化テーブルへのアクセスには適用されません。  


##  <a name="dml"></a> データの変更  

以下の DML ステートメントがサポートされています。  

-   INSERT VALUES (ステートメントごとに 1 行) と INSERT ...SELECT  

-   UPDATE  

-   DELETE  

-   WHERE は UPDATE ステートメントと DELETE ステートメントでサポートされています。  

##  <a name="cof"></a> フロー制御言語  
 次のフロー制御言語構成がサポートされています。  

-   [IF...ELSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)  

-   [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  

-   [RETURN &#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md)  

-   [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md) では、すべての[インメモリ OLTP に対してサポートされるデータ型](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)とメモリ最適化テーブル型を使用できます。 変数は NULL または NOT NULL として宣言できます。  

-   [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  

-   [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  

               To achieve optimal performance, use a single TRY/CATCH block for an entire natively compiled T-SQL module.  

-   [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)  

-   BEGIN ATOMIC (ストアド プロシージャの外部レベル)。 詳細については、「 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)」を参照してください。  

##  <a name="so"></a> サポートされている演算子  
 サポートされている演算子は次のとおりです。  

-   [比較演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md) (例: >、\<、>=、<=)  

-   単項演算子 (+、-)。  

-   二項演算子 (*、/、+、-、% (剰余))。  

               The plus operator (+) is supported on both numbers and strings.  

-   論理演算子 (AND、OR、NOT)。  

-   ビット演算子 ~、&、|、および ^  

-   APPLY 演算子
    - **適用対象:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。  
      [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 以降では、ネイティブ コンパイル モジュールで APPLY 演算子がサポートされます。

##  <a name="bfncsp"></a> ネイティブ コンパイル モジュールの組み込み関数  
 メモリ最適化テーブルの構造とネイティブ コンパイル T-SQL モジュールでは、次の関数がサポートされます。  

-   すべての[数学関数 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  

-   日付関数: CURRENT_TIMESTAMP、DATEADD、DATEDIFF、DATEFROMPARTS、DATEPART、DATETIME2FROMPARTS、DATETIMEFROMPARTS、DAY、EOMONTH、GETDATE、GETUTCDATE、MONTH、SMALLDATETIMEFROMPARTS、SYSDATETIME、SYSUTCDATETIME、YEAR。  

-   文字列関数: LEN、LTRIM、RTRIM、SUBSTRING。  
    - **適用対象:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。  
      [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 以降では、次の組み込み関数もサポートされます: TRIM、TRANSLATE、CONCAT_WS。  

-   ID 関数: SCOPE_IDENTITY  

-   NULL 関数: ISNULL  

-   一意識別子関数: NEWID および NEWSEQUENTIALID  

-   JSON 関数  
    - **適用対象:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。  
      [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 以降では、ネイティブ コンパイル モジュールで JSON 関数がサポートされます。

-   エラー関数: ERROR_LINE、ERROR_MESSAGE、ERROR_NUMBER、ERROR_PROCEDURE、ERROR_SEVERITY、ERROR_STATE  

-   システム関数: @@rowcount。 ネイティブ コンパイル ストアド プロシージャ内のステートメントによって、@@rowcount が更新されます。ネイティブ コンパイル ストアド プロシージャ内で @@rowcount を使用し、ネイティブ コンパイル ストアド プロシージャ内で実行された最後のステートメントによる影響を受けた行の数を決定することができます。 ただし、ネイティブ コンパイル ストアド プロシージャの実行の開始時および終了時に、@@rowcount は 0 にリセットされます。  

-   セキュリティ関数: IS_MEMBER({'group' | 'role'})、IS_ROLEMEMBER ('role' [, 'database_principal'])、IS_SRVROLEMEMBER ('role' [, 'login'])、ORIGINAL_LOGIN()、SESSION_USER、CURRENT_USER、SUSER_ID(['login'])、SUSER_SID(['login'] [, Param2])、SUSER_SNAME([server_user_sid])、SYSTEM_USER、SUSER_NAME、USER、USER_ID(['user'])、USER_NAME([id])、CONTEXT_INFO()。

-   ネイティブ モジュールの実行は入れ子にすることができます。

##  <a name="auditing"></a> 監査  
 プロシージャ レベルの監査はネイティブ コンパイル ストアド プロシージャでサポートされています。  

 監査の詳細については、「 [Create a Server Audit and Database Audit Specification](../../relational-databases/security/auditing/create-a-server-audit-and-database-audit-specification.md)」を参照してください。  

##  <a name="tqh"></a> テーブル ヒントとクエリ ヒント  
 サポート対象は次のとおりです。  

-   テーブル ヒント構文またはクエリの [OPTION 句 &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md) での INDEX、FORCESCAN、および FORCESEEK ヒント。 詳細については、「[テーブル ヒント &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)」を参照してください。  

-   FORCE ORDER  

-   LOOP 結合ヒント  

-   OPTIMIZE FOR  

 詳細については、「[クエリ ヒント &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)」を参照してください。  

##  <a name="los"></a> 並べ替えに関する制限事項  
 [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) および [ORDER BY 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md) を使用するクエリでは、8,000 を超える行の並べ替えを行うことができます。 ただし、[ORDER BY 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md) を使用しない場合、[TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) で並べ替えができる行数は最大で 8,000 です (結合がある場合は、より少ない行数になります)。  

 クエリが [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) 演算子および [ORDER BY 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md) を使用する場合、TOP 演算子には 8192 行まで指定できます。 8192 行を超える行を指定すると、エラー メッセージが表示されます: "**メッセージ 41398、レベル 16、状態 1、プロシージャ *\<procedureName>* 、行 *\<lineNumber>* TOP 演算子は、最大 8192 行を返すことができます。 *\<number>* が要求されました**"。  

 TOP 句がない場合は、ORDER BY で任意の数の行を並べ替えることができます。  

 ORDER BY 句を使用しない場合、TOP 演算子と共に任意の整数値を使用できます。  

 TOP N = 8192 の例: コンパイルできます。  

```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8192 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```

 TOP N > 8192 の例: コンパイルできません。  

```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8193 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```

 8192 行の制限は、 `TOP N` が定数の場合に、前の例のように、 `N` にのみ適用されます。  8192 より大きな `N` が必要である場合は、値を変数に割り当て、 `TOP`と共にその変数を使用することができます。  

 変数を使用した例: コンパイルできます。  

```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    DECLARE @v int = 8193   
    SELECT TOP (@v) ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```

 **返される行に関する制限事項:** TOP 演算子から返される行数を減らせる可能性がある場合が 2 つあります。  

-   クエリで JOIN を使用します。  制限における JOIN の影響は、クエリ プランによって異なります。  

-   ORDER BY 句で集計関数または集計関数への参照を使用する。  

 TOP N での最悪のケースでサポートされる最大 N を計算する式は次のとおりです: `N = floor ( 65536 / number_of_tables * 8 + total_size+of+aggs )`。  

## <a name="see-also"></a>参照  
 [ネイティブ コンパイル ストアド プロシージャ](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)   
 [ネイティブ コンパイル ストアド プロシージャの移行に関する問題](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)  


