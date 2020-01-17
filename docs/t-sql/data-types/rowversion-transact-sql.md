---
title: rowversion (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- timestamp_TSQL
- timestamp
dev_langs:
- TSQL
helpviewer_keywords:
- rowversion data type
- size [SQL Server], rowversion
- row version-stamping [SQL Server]
- rowversion columns
- version-stamping table rows
- unique rowversion numbers
- unique timestamp numbers
- timestamp data type
- timestamp columns
- size [SQL Server], timestamp
ms.assetid: 65c9cf0e-3e8a-45f8-87b3-3460d96afb0b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0129999e61e1df1c61c3a0fb58eab1b3a1cca7b6
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245300"
---
# <a name="rowversion-transact-sql"></a>rowversion (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

自動的に生成された、データベース内で一意の 2 進数を公開するデータ型です。 **rowversion** は、通常、テーブルの行のバージョンを記録するためのメカニズムとして使用します。 ストレージ サイズは 8 バイトです。 **rowversion** データ型は数値を加算していくだけであり、日付や時刻では保持されません。 日付または時刻を記録するには、 **datetime2** データ型を使用してください。
  
## <a name="remarks"></a>解説  
各データベースを含むテーブルで実行される update 操作または挿入ごとにインクリメントされるカウンターには、 **rowversion** 、データベース内の列です。 このカウンターは、データベース rowversion です。 これにより、クロックへの関連付けが可能な実際の時間ではなく、データベース内の相対時間が追跡されます。 テーブルには、1 つだけ保持できます **rowversion** 列です。 たびにを持つ行、 **rowversion** で増加したデータベース rowversion 値が挿入される、列が変更または挿入、 **rowversion** 列です。 このため、 **rowversion** 列、不適切なキーとして、特に主キー。 行を更新すると rowversion 値が変わるので、キーの値も変わります。 列が主キー内にある場合、以前のキーの値は無効になり、この以前の値を参照する外部キーも無効になります。 動的カーソルでテーブルを参照する場合、すべての更新操作はカーソル上の行の位置を変更します。 列がインデックス キーの場合は、データ行に対するすべての更新によって、インデックスの更新も生成されます。  行の値が変更されない場合でも、**rowversion** 値は、update ステートメントによって増分されます (たとえば、列の値が 5 のときに、update ステートメントによって値が 5 に設定された場合、この操作は値の変更がないにもかかわらず更新とみなされ、**rowversion** は増分されます)。
  
**timestamp** は、**rowversion** データ型のシノニムであり、データ型のシノニムの動作が適用されます。 DDL ステートメントでは、可能な限り **timestamp** の代わりに **rowversion** を使用してください。 詳しくは、「[データ型のシノニム &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-synonyms-transact-sql.md)」をご覧ください。
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] の **timestamp** データ型は、ISO 標準で定義されている **timestamp** データ型とは異なります。
  
> [!NOTE]  
>  **timestamp** 構文は非推奨とされます。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
CREATE TABLE または ALTER TABLE ステートメントでは、 **timestamp** データ型の列名を指定する必要はありません。次に例を示します。
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, timestamp);  
```  
  
列名を指定しない場合、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  が **timestamp** 列名を生成します。 ただし、 **rowversion** シノニムはこの動作に従っていません。 **rowversion** を使用するときは、列名を指定する必要があります。次に例を示します。
  
```sql
CREATE TABLE ExampleTable2 (PriKey int PRIMARY KEY, VerCol rowversion) ;  
```  
  
> [!NOTE]  
>  **rowversion** 列が SELECT リストに含まれる SELECT INTO ステートメントを使用すると、重複した **rowversion** の値を生成することができます。 このように **rowversion** を使うことはお勧めしません。  
  
Null 値非許容の **rowversion** 列は、 **binary(8)** 列と同じ意味です。 Null 値許容の **rowversion** 列は、 **varbinary(8)** 列と同じ意味です。
  
行の **rowversion** 列を使用して、最後の読み取り以降、その行に対して update ステートメントが実行されているかどうかを簡単に判断できます。 行に対して update ステートメントが実行されていれば、rowversion 値は更新されています。 行に対して update ステートメントが実行されていなければ、rowversion 値は前回の読み取り時と同じです。 データベースの現在の rowversion 値を返すには、[@@DBTS](../../t-sql/functions/dbts-transact-sql.md) を使用します。
  
複数のユーザーが同時に行を更新するときに、データベースの整合性を維持するために、 **rowversion** 列をテーブルに追加することができます。 テーブルに対するクエリを再度実行せずに、行数や更新された行を把握する必要がある場合もあります。
  
たとえば、`MyTest` という名前のテーブルを作成するとします。 以下の [!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントを実行して、テーブル内のデータを設定します。
  
```sql
CREATE TABLE MyTest (myKey int PRIMARY KEY  
    ,myValue int, RV rowversion);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (2, 0);  
GO  
```  
  
次に、以下のサンプル [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用して、更新中に `MyTest` テーブルにオプティミスティック コンカレンシーを実装します。
  
```sql
DECLARE @t TABLE (myKey int);  
UPDATE MyTest  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND RV = myRv;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  
`myRv` は、その行の前回の読み取り時間を示す、行の **rowversion** 列の値です。 この値を実際の **rowversion** 値に置き換える必要があります。 実際の **rowversion** 値の例は、0x00000000000007d3 などになります。
  
また、サンプル [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントをトランザクションに置くことができます。 トランザクションの範囲内で `@t` 変数に対してクエリを実行すると、`MyTest` テーブルに対するクエリを再度実行しなくても、テーブルの更新済みの `myKey` 列を取得できます。
  
**timestamp** 構文を使用した同じ例を次に示します。
  
```sql
CREATE TABLE MyTest2 (myKey int PRIMARY KEY  
    ,myValue int, TS timestamp);  
GO   
INSERT INTO MyTest2 (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest2 (myKey, myValue) VALUES (2, 0);  
GO  
DECLARE @t TABLE (myKey int);  
UPDATE MyTest2  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND TS = myTS;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  
## <a name="see-also"></a>参照
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)  
[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40;Transact-SQL&#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)
  
  
