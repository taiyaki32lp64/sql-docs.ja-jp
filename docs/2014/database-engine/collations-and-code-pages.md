---
title: Collations and Code Pages |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c626dcac-0474-432d-acc0-cfa643345372
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1969a3e30b31a21c380559a3e8898f87eb8848b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62786737"
---
# <a name="collations-and-code-pages"></a>照合順序とコード ページ
  [!INCLUDE[hek_2](../includes/hek-2-md.md)] には、メモリ最適化テーブルの (var)char 型の列のサポートされているコード ページと、インデックスおよびネイティブ コンパイル ストアド プロシージャで使用されるサポートされている照合順序に関して制限事項があります。  
  
 (var)char 値のコード ページにより、テーブルに格納されているバイト表現と文字との間のマッピングが決定されます。 たとえば、Windows の Latin 1 コード ページ (1252、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の既定値) の場合、文字 "a" はバイト 0x61 に対応します。  
  
 (var)char 値のコード ページは、値に関連付けられた照合順序によって決まります。 たとえば、照合順序 SQL_Latin1_General_CP1_CI_AS に関連付けられたコード ページは 1252 です。  
  
 値の照合順序は、データベースの照合順序から継承されるか、または COLLATE キーワードを使用して明示的に指定できます。 データベースの照合順序は、データベースがメモリ最適化テーブルまたはネイティブ コンパイル ストアド プロシージャを含む場合は変更できません。 次の例では、データベースの照合順序を設定し、異なる照合順序を持つ列を含むテーブルを作成します。 このデータベースでは、ラテン文字の大文字と小文字が区別されない照合順序が使用されます。  
  
 BIN2 照合順序が使用されている場合、インデックスは文字列型の列にのみ作成できます。 LastName 変数では、BIN2 照合順序を使用しています。 FirstName では、データベースの既定値である CI_AS (大文字と小文字を区別しない、アクセントを区別する) を使用しています。  
  
> [!IMPORTANT]  
>  BIN2 照合順序を使用しないインデックス文字列の列に対して、order by や group by を使用することはできません。  
  
```sql  
CREATE DATABASE IMOLTP  
  
ALTER DATABASE IMOLTP ADD FILEGROUP IMOLTP_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE IMOLTP ADD FILE( NAME = 'IMOLTP_mod' , FILENAME = 'c:\data\IMOLTP_mod') TO FILEGROUP IMOLTP_mod;  
--GO  
  
--  set the database collations  
ALTER DATABASE IMOLTP COLLATE Latin1_General_100_CI_AS  
GO  
  
--  
USE IMOLTP   
GO  
  
-- create a table with collation  
CREATE TABLE Employees (  
  EmployeeID int NOT NULL ,   
  LastName nvarchar(20) COLLATE Latin1_General_100_BIN2 NOT NULL INDEX IX_LastName NONCLUSTERED,   
  FirstName nvarchar(10) NOT NULL ,  
  CONSTRAINT PK_Employees PRIMARY KEY NONCLUSTERED HASH(EmployeeID)  WITH (BUCKET_COUNT=1024)  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_AND_DATA)  
GO  
```  
  
 メモリ最適化テーブルとネイティブ コンパイル ストアド プロシージャに対して、次の制限が適用されます。  
  
-   メモリ最適化テーブルの (var)char 型の列では、コード ページ 1252 照合順序を使用する必要があります。 この制限は、n(var)char 型の列には適用されません。 次のコードは、すべての 1252 照合順序を取得します。  
  
    ```sql  
    -- all supported collations for (var)char columns in memory-optimized tables  
    select * from sys.fn_helpcollations()  
    where collationproperty(name, 'codepage') = 1252;  
    ```  
  
     ラテン文字以外の文字を格納する必要がある場合は、n(var)char 型の列を使用します。  
  
-   (n)(var)char 型の列のインデックスは、BIN2 照合順序でのみ指定できます (最初の例を参照してください)。 次のクエリは、すべてのサポートされている BIN2 照合順序を取得します。  
  
    ```sql  
    -- all supported collations for indexes on memory-optimized tables and   
    -- comparison/sorting in natively compiled stored procedures  
    select * from sys.fn_helpcollations() where name like '%BIN2'  
    ```  
  
     解釈された [!INCLUDE[tsql](../includes/tsql-md.md)] を介してテーブルにアクセスする場合は、`COLLATE` キーワードを使用して、式または並べ替え操作による照合順序を変更できます。 この例については、最後の例を参照してください。  
  
-   データベースの照合順序がコード ページ 1252 照合順序でない場合、ネイティブ コンパイル ストアド プロシージャは、パラメーター、ローカル変数、または (var)char 型の文字列定数を使用できません。  
  
-   ネイティブ コンパイル ストアド プロシージャ内のすべての式および並べ替え操作で BIN2 照合順序を使用する必要があります。 これは、すべての比較および並べ替え操作が文字の Unicode コード ポイント (バイナリ表現) に基づいていることを表します。 たとえば、すべての並べ替えで大文字と小文字が区別されます ("Z" が "a" より前に来ます)。 必要に応じて、解釈された [!INCLUDE[tsql](../includes/tsql-md.md)] を使用して、大文字と小文字が区別されない並べ替えと比較を行います。  
  
-   ネイティブ コンパイル ストアド プロシージャ内では、UTF-16 データの切り捨てはサポートされません。 つまり、n (var) char (*n*) 値は n (var) char 型に変換することはできません (*は*) 場合は、*は* < *n*場合、照合順序では、_SC プロパティがあります。 たとえば、次の操作はサポートされません。  
  
    ```sql  
    -- column definition using an _SC collation  
     c2 nvarchar(200) collate Latin1_General_100_CS_AS_SC not null   
    -- assignment to a smaller variable, requiring truncation  
     declare @c2 nvarchar(100) = '';  
     select @c2 = c2  
    ```  
  
     UTF-16 データを使った LEN、SUBSTRING、LTRIM、RTRIM などの文字列操作関数は、ネイティブ コンパイル ストアド プロシージャ内ではサポートされていません。 _SC 照合順序を保持する n(var)char 値に対してこれらの文字列操作関数は使用できません。  
  
     切り捨てを回避するのに十分な大きさの型を使用して、変数を宣言します。  
  
 次の例に、インメモリ OLTP での照合順序の制限の影響と回避策を示します。 この例では、前の例で指定した Employees テーブルを使用しています。 このサンプルは、すべての従業員を一覧表示します。 LastName については、バイナリ照合順序に基づいて、大文字の名前が小文字の名前の前に並べ替えられます。 したがって、"Thomas" は "nolan" の前に来ます。これは、大文字のコード ポイントの方が小さいためです。 FirstName には、大文字と小文字が区別されない照合順序が設定されています。 したがって、並べ替えは、文字のコード ポイントではなくアルファベット順に基づいて行われます。  
  
```sql  
-- insert a number of values  
INSERT Employees VALUES (1,'thomas', 'john')  
INSERT Employees VALUES (2,'Thomas', 'rupert')  
INSERT Employees VALUES (3,'Thomas', 'Jack')  
INSERT Employees VALUES (4,'Thomas', 'annie')  
INSERT Employees VALUES (5,'nolan', 'John')  
GO  
  
-- ===========  
SELECT EmployeeID, LastName, FirstName FROM Employees  
ORDER BY LastName, FirstName  
GO  
  
-- ===========  
-- specify collation: sorting uses case-insensitive collation, thus 'nolan' comes before 'Thomas'  
SELECT * FROM Employees  
ORDER BY LastName COLLATE Latin1_General_100_CI_AS, FirstName  
GO  
  
-- ===========  
-- retrieve employee by Name  
-- must use BIN2 collation for comparison in natively compiled stored procedures  
CREATE PROCEDURE usp_EmployeeByName @LastName nvarchar(20), @FirstName nvarchar(10)  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
  LANGUAGE = N'us_english'  
)  
  SELECT EmployeeID, LastName, FirstName FROM dbo.Employees  
  WHERE   
    LastName = @LastName AND  
    FirstName COLLATE Latin1_General_100_BIN2 = @FirstName  
  
END  
GO  
  
-- this does not return any rows, as EmployeeID 1 has first name 'john', which is not equal to 'John' in a binary collation  
EXEC usp_EmployeeByName 'thomas', 'John'  
  
-- this retrieves EmployeeID 1  
EXEC usp_EmployeeByName 'thomas', 'john'  
```  
  
## <a name="see-also"></a>関連項目  
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
