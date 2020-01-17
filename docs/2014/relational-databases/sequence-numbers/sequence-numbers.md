---
title: シーケンス番号 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- sequence number object, overview
- sequence [Database Engine]
- autonumbers, sequences
- sequence numbers [SQL Server]
- sequence number object
ms.assetid: c900e30d-2fd3-4d5f-98ee-7832f37e79d1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a942136314702d5fe87c1997f20dcb19a74df13d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63184409"
---
# <a name="sequence-numbers"></a>シーケンス番号
  シーケンスは、シーケンスが作成された仕様に従って数値のシーケンスを生成するユーザー定義のスキーマ バインド オブジェクトです。 数値のシーケンスは、定義された間隔で昇順または降順に生成され、要求に応じて繰り返されます。 ID 列とは異なり、シーケンスはテーブルには関連付けられていません。 アプリケーションは、シーケンス オブジェクトを参照して、次の値を受け取ります。 シーケンスとテーブルの関係は、アプリケーションによって制御されます。 ユーザー アプリケーションは、シーケンス オブジェクトを参照し、複数の行およびテーブルにわたって値キーを調整できます。  
  
 シーケンスは、テーブルとは別に、 **CREATE SEQUENCE** ステートメントを使用して作成されます。 オプションを使用することにより、増分、最大値、最小値、始点、自動再開機能、およびパフォーマンスを向上させるためのキャッシュ動作を制御できます。 オプションの詳細については、 [「CREATE SEQUENCE」](/sql/t-sql/statements/create-sequence-transact-sql)を参照してください。  
  
 行の挿入時に生成される ID 列値とは異なり、アプリケーションは、 [NEXT VALUE FOR](/sql/t-sql/functions/next-value-for-transact-sql) 関数を呼び出すことにより、行を挿入する前に次のシーケンス番号を取得できます。 番号がテーブルに挿入されない場合でも、シーケンス番号は、NEXT VALUE FOR が呼び出されたときに割り当てられます。 NEXT VALUE FOR 関数は、テーブル定義内の列の既定値として使用できます。 一度に複数のシーケンス番号の範囲を取得するには、 [sp_sequence_get_range](/sql/relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql) を使用します。  
  
 シーケンスは、任意の整数データ型として定義できます。 シーケンスのデータ型を指定しなかった場合、既定で `bigint` 型が使用されます。  
  
## <a name="using-sequences"></a>シーケンスの使用  
 シーケンスは、次のシナリオで ID 列の代わりに使用します。  
  
-   テーブルへの挿入を行う前に、アプリケーションが数値を必要とする。  
  
-   アプリケーションが、複数のテーブル間またはテーブル内の複数の列間で、単一の番号シリーズを共有する必要がある。  
  
-   指定した番号に達したときに、アプリケーションが番号シリーズを再開する必要がある。 たとえば、1 ～ 10 の値を割り当てた後、アプリケーションは再び 1 ～ 10 の値を割り当てます。  
  
-   アプリケーションが、シーケンス値を別のフィールドで並べ替える必要がある。 NEXT VALUE FOR 関数は、OVER 句を関数呼び出しに適用できます。 OVER 句によって、返される値は OVER 句の ORDER BY 句の順で生成されることが保証されます。  
  
-   アプリケーションが、同時に複数の番号を割り当てる必要がある。 たとえば、アプリケーションで 5 つの連続する番号を予約する必要がある場合などです。 ID 値を要求したときに他のプロセスが番号を同時に発行していた場合、非連続的な ID 値が生成される場合があります。 sp_sequence_get_range を呼び出すことにより、シーケンス内の番号を一度に取得できます。  
  
-   増分値など、シーケンスの仕様を変更する必要がある。  
  
## <a name="limitations"></a>制限事項  
 値を変更できない ID 列とは異なり、シーケンス値はテーブルへの挿入後に自動的に保護されません。 シーケンス値が変更されるのを防止するには、テーブルで更新トリガーを使用して、変更をロールバックします。  
  
 シーケンス値に対して、一意性は自動的には適用されません。 シーケンス値を再利用する機能は仕様です。 テーブルのシーケンス値が一意の値になる必要がある場合は、列に一意なインデックスを作成します。 テーブルのグループ全体でテーブルのシーケンス値が一意になる必要がある場合は、更新ステートメントやシーケンス番号の循環によって発生する重複を防ぐためのトリガーを作成します。  
  
 シーケンス オブジェクトは、定義に従って番号を生成しますが、その番号がどのように使用されるかについては制御しません。 トランザクションがロールバックされたとき、シーケンス オブジェクトが複数のテーブルで共有されているとき、またはテーブルのシーケンス番号を使用することなくシーケンス番号が割り当てられたときは、非連続的なシーケンス番号がテーブルに挿入される可能性があります。 CACHE オプションを使用してシーケンス番号を作成する際に予期しないシャットダウン (電源障害など) が発生すると、キャッシュ内のシーケンス番号が失われる可能性があります。  
  
 1 つの [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメント内で同じシーケンス ジェネレーターを指定する `NEXT VALUE FOR` 関数のインスタンスが複数ある場合、これらすべてのインスタンスは、その [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントによって処理される特定の行について同じ値を返します。 この動作は、ANSI 標準と一貫性があります。  
  
## <a name="typical-use"></a>一般的な使用方法  
 -2,147,483,648 ～ 2,147,483,647 まで 1 ずつ増分される整数のシーケンス番号を作成するには、次のステートメントを使用します。  
  
```  
CREATE SEQUENCE Schema.SequenceName  
    AS int  
    INCREMENT BY 1 ;  
```  
  
 ID 列のように 1 ～ 2,147,483,647 まで 1 ずつ増分される整数のシーケンス番号を作成するには、次のステートメントを使用します。  
  
```  
CREATE SEQUENCE Schema.SequenceName  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
  
```  
  
## <a name="managing-sequences"></a>シーケンスの管理  
 シーケンスの詳細については、「 [sys.sequences](/sql/relational-databases/system-catalog-views/sys-sequences-transact-sql)」を参照してください。  
  
## <a name="examples"></a>使用例  
 関連する例については、「[CREATE SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-sequence-transact-sql)」、「[NEXT VALUE FOR &#40;Transact-SQL&#41;](/sql/t-sql/functions/next-value-for-transact-sql)」、および「[sp_sequence_get_range](/sql/relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql)」を参照してください。  
  
### <a name="a-using-a-sequence-number-in-a-single-table"></a>A. 1 つのテーブルでシーケンス番号を使用する  
 次の例では、Test という名前のスキーマ、Orders という名前のテーブル、および CountBy1 という名前のシーケンスを作成した後、NEXT VALUE FOR 関数を使用してテーブルに行を挿入します。  
  
```  
--Create the Test schema  
CREATE SCHEMA Test ;  
GO  
  
-- Create a table  
CREATE TABLE Test.Orders  
    (OrderID int PRIMARY KEY,  
    Name varchar(20) NOT NULL,  
    Qty int NOT NULL);  
GO  
  
-- Create a sequence  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
-- Insert three records  
INSERT Test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Tire', 2) ;  
INSERT test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Seat', 1) ;  
INSERT test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Brake', 1) ;  
GO  
  
-- View the table  
SELECT * FROM Test.Orders ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../../includes/ssresult-md.md)]  
  
 `OrderID  Name    Qty`  
  
 `1        Tire    2`  
  
 `2        Seat    1`  
  
 `3        Brake   1`  
  
### <a name="b-calling-next-value-for-before-inserting-a-row"></a>B. 行を挿入する前に NEXT VALUE FOR を呼び出す  
 次の例では、例 A で作成した `Orders` テーブルを使用して、 `@nextID`という名前の変数を宣言します。次に、NEXT VALUE FOR 関数を使用して、この変数を、次に使用できるシーケンス番号に設定します。 アプリケーションは、潜在的な注文の `OrderID` 番号を顧客に提示した後、注文を確認するなど、注文に関する処理を行うものと考えられます。 この処理にどれだけの時間がかかろうとも、またこの処理中に他の注文がいくつ追加されようとも、この接続によって元の番号は保持されます。 最後に、 `INSERT` ステートメントによって注文が `Orders` テーブルに追加されます。  
  
```  
DECLARE @NextID int ;  
SET @NextID = NEXT VALUE FOR Test.CountBy1;  
-- Some work happens  
INSERT Test.Orders (OrderID, Name, Qty)  
    VALUES (@NextID, 'Rim', 2) ;  
GO  
  
```  
  
### <a name="c-using-a-sequence-number-in-multiple-tables"></a>C. 複数のテーブルでシーケンス番号を使用する  
 次の例では、生産ラインの監視プロセスが、ワークショップ全体で発生するイベントの通知を受信すると仮定します。 各イベントは、単調に増加する一意な `EventID` 番号を受け取ります。 すべてのイベントは、同じ `EventID` シーケンス番号を使用します。したがって、すべてのイベントが集約されたレポートで、それぞれのイベントを一意に識別できます。 ただし、イベント データは、イベントの種類に応じて、3 つの異なるテーブルに格納されます。 このコード例では、 `Audit`という名前のスキーマ、 `EventCounter`という名前のシーケンス、およびそれぞれが `EventCounter` シーケンスを既定値として使用する 3 つのテーブルを作成します。 次に、3 つのテーブルに行を追加し、クエリを実行して結果を取得します。  
  
```  
CREATE SCHEMA Audit ;  
GO  
CREATE SEQUENCE Audit.EventCounter  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
CREATE TABLE Audit.ProcessEvents  
(  
    EventID int PRIMARY KEY CLUSTERED   
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EventCode nvarchar(5) NOT NULL,  
    Description nvarchar(300) NULL  
) ;  
GO  
  
CREATE TABLE Audit.ErrorEvents  
(  
    EventID int PRIMARY KEY CLUSTERED  
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EquipmentID int NULL,  
    ErrorNumber int NOT NULL,  
    EventDesc nvarchar(256) NULL  
) ;  
GO  
  
CREATE TABLE Audit.StartStopEvents  
(  
    EventID int PRIMARY KEY CLUSTERED  
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EquipmentID int NOT NULL,  
    StartOrStop bit NOT NULL  
) ;  
GO  
  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (248, 0) ;  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (72, 0) ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (2735,   
    'Clean room temperature 18 degrees C.') ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (18, 'Spin rate threashold exceeded.') ;  
INSERT Audit.ErrorEvents (EquipmentID, ErrorNumber, EventDesc)   
    VALUES (248, 82, 'Feeder jam') ;  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (248, 1) ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (1841, 'Central feed in bypass mode.') ;  
-- The following statement combines all events, though not all fields.  
SELECT EventID, EventTime, Description FROM Audit.ProcessEvents   
UNION SELECT EventID, EventTime, EventDesc FROM Audit.ErrorEvents   
UNION SELECT EventID, EventTime,   
CASE StartOrStop   
    WHEN 0 THEN 'Start'   
    ELSE 'Stop'  
END   
FROM Audit.StartStopEvents  
ORDER BY EventID ;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../../includes/ssresult-md.md)]  
  
 `EventID  EventTime                Description`  
  
 `1        2009-11-02 15:00:51.157  Start`  
  
 `2        2009-11-02 15:00:51.160  Start`  
  
 `3        2009-11-02 15:00:51.167  Clean room temperature 18 degrees C.`  
  
 `4        2009-11-02 15:00:51.167  Spin rate threshold exceeded.`  
  
 `5        2009-11-02 15:00:51.173  Feeder jam`  
  
 `6        2009-11-02 15:00:51.177  Stop`  
  
 `7        2009-11-02 15:00:51.180  Central feed in bypass mode.`  
  
### <a name="d-generating-repeating-sequence-numbers-in-a-result-set"></a>D. 結果セットで循環するシーケンス番号を生成する  
 次の例は、シーケンス番号に関する 2 つの機能を示しています。これらは、サイクル処理の機能と、SELECT ステートメントで `NEXT VALUE FOR` を使用した機能です。  
  
```  
CREATE SEQUENCE CountBy5  
   AS tinyint  
    START WITH 1  
    INCREMENT BY 1  
    MINVALUE 1  
    MAXVALUE 5  
    CYCLE ;  
GO  
  
SELECT NEXT VALUE FOR CountBy5 AS SurveyGroup, Name FROM sys.objects ;  
GO  
```  
  
### <a name="e-generating-sequence-numbers-for-a-result-set-by-using-the-over-clause"></a>E. OVER 句を使用して結果セットのシーケンス番号を生成する  
 次の例では、結果セットをシーケンス番号列に追加する前に、 `OVER` 句を使用して `Name` の順に並べ替えます。  
  
```  
USE AdventureWorks2012 ;  
GO  
  
CREATE SCHEMA Samples ;  
GO  
  
CREATE SEQUENCE Samples.IDLabel  
    AS tinyint  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
### <a name="f-resetting-the-sequence-number"></a>F. シーケンス番号をリセットする  
 例 E では、`Samples.IDLabel` のシーケンス番号の最初の 79 個の番号が使用されました (`AdventureWorks2012` のバージョンによっては結果の数が異なる場合があります)。次のコードを実行すると、後続の 79 個のシーケンス番号 (80 ～ 158) が使用されます。  
  
```  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
 次のステートメントを実行すると、`Samples.IDLabel` シーケンスが最初から開始されます。  
  
```  
ALTER SEQUENCE Samples.IDLabel  
RESTART WITH 1 ;  
```  
  
 再び SELECT ステートメントを実行して、 `Samples.IDLabel` シーケンス番号が 1 から開始されていることを確認します。  
  
```  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
### <a name="g-changing-a-table-from-identity-to-sequence"></a>G. ID からシーケンスにテーブルを変更する  
 次の例では、1 つのスキーマと、サンプルの 3 つの行が含まれたテーブルを作成します。 次に、新しい列を追加し、古い列を削除します。  
  
```  
-- Create a schema  
CREATE SCHEMA Test ;  
GO  
  
-- Create a table  
CREATE TABLE Test.Department  
    (  
        DepartmentID smallint IDENTITY(1,1) NOT NULL,  
        Name nvarchar(100) NOT NULL,  
        GroupName nvarchar(100) NOT NULL  
    CONSTRAINT PK_Department_DepartmentID PRIMARY KEY CLUSTERED   
         (DepartmentID ASC)   
    ) ;  
GO  
  
-- Insert three rows into the table  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Engineering', 'Research and Development');  
GO  
  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Tool Design', 'Research and Development');  
GO  
  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Sales', 'Sales and Marketing');  
GO  
  
-- View the table that will be changed  
SELECT * FROM Test.Department ;  
GO  
  
-- End of portion creating a sample table  
--------------------------------------------------------  
-- Add the new column that does not have the IDENTITY property  
ALTER TABLE Test.Department   
    ADD DepartmentIDNew smallint NULL  
GO  
  
-- Copy values from the old column to the new column  
UPDATE Test.Department  
    SET DepartmentIDNew = DepartmentID ;  
GO  
  
-- Drop the primary key constraint on the old column  
ALTER TABLE Test.Department  
    DROP CONSTRAINT [PK_Department_DepartmentID];  
-- Drop the old column  
ALTER TABLE Test.Department  
    DROP COLUMN DepartmentID ;  
GO  
  
-- Rename the new column to the old columns name  
EXEC sp_rename 'Test.Department.DepartmentIDNew',   
    'DepartmentID', 'COLUMN';  
GO  
  
-- Change the new column to NOT NULL  
ALTER TABLE Test.Department  
    ALTER COLUMN DepartmentID smallint NOT NULL ;  
-- Add the unique primary key constraint  
ALTER TABLE Test.Department  
    ADD CONSTRAINT PK_Department_DepartmentID PRIMARY KEY CLUSTERED   
         (DepartmentID ASC) ;  
-- Get the highest current value from the DepartmentID column   
-- and create a sequence to use with the column. (Returns 3.)  
SELECT MAX(DepartmentID) FROM Test.Department ;  
-- Use the next desired value (4) as the START WITH VALUE;  
CREATE SEQUENCE Test.DeptSeq  
    AS smallint  
    START WITH 4  
    INCREMENT BY 1 ;  
GO  
  
-- Add a default value for the DepartmentID column  
ALTER TABLE Test.Department  
    ADD CONSTRAINT DefSequence DEFAULT (NEXT VALUE FOR Test.DeptSeq)   
        FOR DepartmentID;  
GO  
  
-- View the result  
SELECT DepartmentID, Name, GroupName  
FROM Test.Department ;   
-- Test insert  
INSERT Test.Department (Name, GroupName)  
    VALUES ('Audit', 'Quality Assurance') ;  
GO  
  
-- View the result  
SELECT DepartmentID, Name, GroupName  
FROM Test.Department ;  
GO  
  
```  
  
 `SELECT *` を使用する [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントは、最初の列としてではなく最後の列として、新しい列を受け取ります。 この動作を許容できない場合は、新しいテーブルを作成してデータをそこに移動した後、新しいテーブルに対する権限を再作成する必要があります。  
  
## <a name="related-content"></a>関連コンテンツ  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-sequence-transact-sql)  
  
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-sequence-transact-sql)  
  
 [DROP SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-sequence-transact-sql)  
  
 [IDENTITY &#40;Property&#41; &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property)  
  
  
