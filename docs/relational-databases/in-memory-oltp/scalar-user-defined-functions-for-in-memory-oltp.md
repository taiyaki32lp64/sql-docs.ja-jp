---
title: インメモリ OLTP でのユーザー定義のスカラー関数 | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: d2546e40-fdfc-414b-8196-76ed1f124bf5
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f3614b1f9c058405c041aa2b4de27d97caadb8fd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111766"
---
# <a name="scalar-user-defined-functions-for-in-memory-oltp"></a>インメモリ OLTP でのユーザー定義のスカラー関数
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]で、ネイティブ コンパイル済みのスカラー ユーザー定義関数を作成および削除できます。 これらのユーザー定義関数を変更することもできます。 ネイティブ コンパイルでは、Transact-SQL でのユーザー定義関数の評価のパフォーマンスが向上します。  
  
 ネイティブ コンパイル済みのスカラー ユーザー定義関数を変更する際には、操作が実行されて新しいバージョンの関数がコンパイルされる間、アプリケーションを引き続き使用できます。  
  
 サポートされている T-SQL 構造については、「 [ネイティブ コンパイル T-SQL モジュールでサポートされる機能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)」を参照してください。  
  
## <a name="creating-dropping-and-altering-user-defined-functions"></a>ユーザー定義関数の作成、削除、および変更  
 ネイティブ コンパイル済みのスカラー ユーザー定義関数を作成するには CREATE FUNCTION、このユーザー定義関数を削除するには DROP FUNCTION、この関数を変更するには ALTER FUNCTION を使用します。 これらのユーザー定義関数には、BEGIN ATOMIC WITH が必要です。  
  
 サポートされている構文と制限については、次のトピックを参照してください。  
  
-   [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
  
-   [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)  
  
-   [DROP FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md)  
  
     ネイティブ コンパイル済みのスカラー ユーザー定義関数の DROP FUNCTION 構文は、解釈されたユーザー定義関数の場合と同じです。  
  
-   [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
  
 ネイティブ コンパイル済みのスカラー ユーザー定義関数には、[sp_recompile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md) ストアド プロシージャを使用できます。 その場合、メタデータ内に存在する定義を使用して関数が再コンパイルされます。  
  
 次のサンプルは、 [AdventureWorks2016CTP3](https://www.microsoft.com/download/details.aspx?id=49502) サンプル データベースのスカラー UDF を示しています。  
  
```sql  
CREATE FUNCTION [dbo].[ufnLeadingZeros_native](@Value int)   
RETURNS varchar(8)   
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS   
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')  
  
    DECLARE @ReturnValue varchar(8);  
    SET @ReturnValue = CONVERT(varchar(8), @Value);  
       DECLARE @i int = 0, @count int = 8 - LEN(@ReturnValue)  
  
    WHILE @i < @count  
       BEGIN  
            SET @ReturnValue = '0' + @ReturnValue;  
            SET @i += 1  
       END  
  
    RETURN (@ReturnValue);  
  
END  
```  
  
## <a name="calling-user-defined-functions"></a>ユーザー定義関数の呼び出し  
 ネイティブ コンパイル済みのスカラー ユーザー定義関数は、式 (組み込みスカラー関数および解釈されたスカラー ユーザー定義関数と同じ場所) に使用できます。 ネイティブ コンパイル済みのスカラー ユーザー定義関数は、EXECUTE ステートメント、Transact-SQL ステートメント、およびネイティブ コンパイル ストアド プロシージャでも使用できます。  
  
 このスカラー ユーザー定義関数は、ネイティブ コンパイル ストアド プロシージャ、ネイティブ コンパイル済みのユーザー定義関数、および組み込み関数が許可されている任意の場所で使用できます。 また、ネイティブ コンパイル済みのスカラー ユーザー定義関数は従来の Transact-SQL モジュールにも使用できます。  
  
 このスカラー ユーザー定義関数は、解釈されたスカラー ユーザー定義関数を使用できる任意の場所で相互運用モードで使用できます。 このような使用は、「 **Transactions with Memory-Optimized Tables (メモリ最適化テーブルでのトランザクション)** 」の「 [Supported Isolation Levels for Cross-Container Transactions (複数コンテナーにまたがるトランザクションでサポートされる分離レベル)](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)」セクションで説明されているとおり、コンテナーにまたがるトランザクションの制約に従う必要があります。 相互運用モードの詳細については、「 [解釈された Transact-SQL を使用したメモリ最適化テーブルへのアクセス](../../relational-databases/in-memory-oltp/accessing-memory-optimized-tables-using-interpreted-transact-sql.md)」を参照してください。  
  
 ネイティブ コンパイル済みのスカラー ユーザー定義関数には、明示的な実行コンテキストが必要です。 詳細については、「[EXECUTE AS Clause &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)」を参照してください。 EXECUTE AS CALLER はサポートされていません。 詳細については、「 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)」を参照してください。  
  
 Transact-SQL 実行ステートメントおよびネイティブ コンパイル済みのスカラー ユーザー定義関数でサポートされている構文については、「 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)」を参照してください。 ネイティブ コンパイル ストアド プロシージャでユーザー定義関数を実行するためにサポートされている構文については、「 [ネイティブ コンパイル T-SQL モジュールでサポートされる機能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)」を参照してください。  
  
## <a name="hints-and-parameters"></a>ヒントとパラメーター  
 ネイティブ コンパイル済みのスカラー ユーザー定義関数の内部でのテーブル、結合、およびクエリ ヒントに対するサポートは、ネイティブ コンパイル ストアド プロシージャでのこれらのヒントに対するサポートと同じです。 解釈されたスカラー ユーザー定義関数の場合と同様、ネイティブ コンパイル済みのスカラー ユーザー定義関数を参照する Transact-SQL クエリに含まれているクエリ ヒントは、このユーザー定義関数のクエリ プランに影響を与えません。  
  
 ネイティブ コンパイル済みのスカラー ユーザー定義関数でサポートされているパラメーターは、パラメーターがスカラー ユーザー定義関数で許可されている限り、ネイティブ コンパイル ストアド プロシージャでサポートされているすべてのパラメーターです。 サポートされているパラメーターの例には、テーブル値パラメーターがあります。  
  
## <a name="schema-bound"></a>スキーマ バインド  
 ネイティブ コンパイル済みのスカラー ユーザー定義関数には、次のことが当てはまります。  
  
-   CREATE FUNCTION および ALTER FUNCTION で WITH SCHEMABINDING 引数を使用して、スキーマ バインドにする必要があります。  
  
-   スキーマ バインドのストアド プロシージャまたはユーザー定義関数によって参照されているときは、削除または変更することができません。  
  
## <a name="showplanxml"></a>SHOWPLAN_XML  
 ネイティブ コンパイル済みのスカラー ユーザー定義関数は、SHOWPLAN_XML をサポートしています。 ネイティブ コンパイル ストアド プロシージャと同様、一般的な SHOWPLAN_XML スキーマに準拠しています。 ユーザー定義関数の基本要素は `<UDF>`です。  
  
 ネイティブ コンパイル済みのスカラー ユーザー定義関数では、STATISTICS XML はサポートされていません。 STATISTICS XML を有効にして、ユーザー定義関数を参照するクエリを実行すると、ユーザー定義関数の部分が欠如した XML コンテンツが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 ネイティブ コンパイル ストアド プロシージャと同様、ネイティブ コンパイル済みのスカラー ユーザー定義関数が作成される際に、この関数から参照されるオブジェクトのアクセス許可がチェックされます。 権限を借用したユーザーに適切なアクセス許可がない場合、CREATE FUNCTION は失敗します。 アクセス許可の変更により、権限を借用したユーザーに適切なアクセス許可がなくなった場合、以降のユーザー定義関数の実行は失敗します。  
  
 ネイティブ コンパイル ストアド プロシージャの内部でネイティブ コンパイル済みのスカラー ユーザー定義関数を使用する場合は、外部プロシージャが作成される際に、ユーザー定義関数を実行するためのアクセス許可がチェックされます。 外部プロシージャによって権限を借用したユーザーが、ユーザー定義関数の EXEC アクセス許可を持っていない場合、ストアド プロシージャの作成は失敗します。 アクセス許可の変更により、ユーザーに EXEC アクセス許可がなくなった場合、外部プロシージャの実行は失敗します。  
  
## <a name="see-also"></a>参照  
 [組み込み関数 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [XML 形式での実行プランの保存](../../relational-databases/performance/save-an-execution-plan-in-xml-format.md)  
  
  
