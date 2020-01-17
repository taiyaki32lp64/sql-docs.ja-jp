---
title: COLUMNS_UPDATED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COLUMNS_UPDATED_TSQL
- COLUMNS_UPDATED
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMNS_UPDATED function
- testing columns
- column testing [SQL Server]
- updated columns
ms.assetid: 765fde44-1f95-4015-80a4-45388f18a42c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ae6e3b08b3a29afb9282d28f33ec9406ab418b2c
ms.sourcegitcommit: 0d5b0aeee2a2b34fd448aec2e72c0fa8be473ebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2020
ms.locfileid: "75721927"
---
# <a name="columns_updated-transact-sql"></a>COLUMNS_UPDATED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

この関数は、テーブルまたはビューの挿入または更新された列を示す **varbinary** ビット パターンを返します。 `COLUMNS_UPDATED` は [!INCLUDE[tsql](../../includes/tsql-md.md)] の INSERT または UPDATE トリガーの内部のどこでも使用でき、そのトリガーが特定の動作を実行すべきかどうかをテストすることができます。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
COLUMNS_UPDATED ( )   
```  
  
## <a name="return-types"></a>戻り値の型
**varbinary**
  
## <a name="remarks"></a>解説  
`COLUMNS_UPDATED` は、実行される UPDATE または INSERT アクションを複数の列でテストします。 テストするには 1 つの列の UPDATE または INSERT の試行、次のように使用します。 [UPDATE()](../../t-sql/functions/update-trigger-functions-transact-sql.md)です。
  
`COLUMNS_UPDATED` は、左から右に順序付けられた 1 つまたは複数のバイトを返します。 各バイトの右端のビットは、最下位ビットです。 左端のバイトの右端のビットがテーブル内の最初のテーブル列を表し、右から 2 番目のビットは 2 番目の列を、それ以下のビットも同様の順で列を表します。 トリガーが作成されるテーブルに列が 9 個以上ある場合、`COLUMNS_UPDATED` は複数のバイトを返します。最下位バイトが左端になります。 INSERT 動作では、列には明示的な値または暗黙的な (NULL) 値が挿入されるので、`COLUMNS_UPDATED` は、すべての列に対して TRUE を返します。
  
特定の列に対する更新または挿入をテストするには、テスト対象列のビットごとの演算子および整数ビットマスクを使用した構文に従います。 たとえば、テーブル **t1** に、列 **C1**、**C2**、**C3**、**C4**、および **C5** があるとします。 列 **C2**、**C3**、および **C4** がすべて正常に更新されている (テーブル **t1** に UPDATE トリガーがある場合) かどうかを検証するには、 **& 14** を使用した構文に従います。 列 **C2** が更新されているかどうかだけをテストするには、 **& 2** を指定します。 実際の例については、[例 A](#a-using-columns_updated-to-test-the-first-eight-columns-of-a-table) と[例 B](#b-using-columns_updated-to-test-more-than-eight-columns) を参照してください。
  
`COLUMNS_UPDATED` は、[!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT または UPDATE トリガーの内部のどこでも使用できます。
  
INFORMATION_SCHEMA.COLUMNS ビューの ORDINAL_POSITION 列には、`COLUMNS_UPDATED` から返される列のビット パターンとの互換性がありません。 `COLUMNS_UPDATED` と互換性のあるビット パターンを取得するには、次の例に示すように、`INFORMATION_SCHEMA.COLUMNS` ビューに対してクエリを実行する際に、`COLUMNPROPERTY` システム関数の `ColumnID` プロパティを参照します。
  
```sql
SELECT TABLE_NAME, COLUMN_NAME,  
    COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME),  
    COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
```  

トリガーを列に適用すると、列の値が更されない場合でも、`COLUMNS_UPDATED` が `true` または `1` として返されます。 これは意図されたもので、トリガーでは挿入/更新/削除操作を許容するかどうかを決定するビジネス ロジックを実装する必要があります。 
  
## <a name="column-sets"></a>列セット
テーブルで列セットが定義されると、`COLUMNS_UPDATED` 関数は次のように動作します。
-   列セットのメンバーである列を明示的に更新すると、その列の対応するビットが 1 に設定され、列セットのビットが 1 に設定されます。  
-   列セットを明示的に更新すると、列セットのビットが 1 に設定され、そのテーブル内のすべてのスパース列のビットが 1 に設定されます。  
-   挿入操作では、すべてのビットが 1 に設定されます。  
  
     列セットを変更すると列セット内のすべての列のビットが 1 にリセットされるため、列セット内の変更されなかった列も変更されているように見えます。 列セットの詳細については、「[列セットの使用](../../relational-databases/tables/use-column-sets.md)」を参照してください。  
  
## <a name="examples"></a>例  
  
### <a name="a-using-columns_updated-to-test-the-first-eight-columns-of-a-table"></a>A. COLUMNS_UPDATED を使用して、テーブルの最初の 8 列をテストする  
この例では、`employeeData` と `auditEmployeeData` という 2 つのテーブルを作成します。 `employeeData` テーブルには、機密扱いの従業員給与支払い名簿情報が格納されており、人事部のメンバーが修正できます。 従業員の社会保障番号 (SSN)、年間給与、または銀行口座番号に変更があると、監査レコードが生成され、`auditEmployeeData` 監査テーブルに挿入されます。
  
`COLUMNS_UPDATED()` 関数を使用すると、従業員の機密情報を含む列に加えられた変更をすばやくテストできます。 この方法で `COLUMNS_UPDATED()` が正しく動作するのは、テーブルの最初の 8 列に対する変更を検出する場合だけです。
  
```sql
USE AdventureWorks2012;  
GO  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_NAME = 'employeeData')  
   DROP TABLE employeeData;  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_NAME = 'auditEmployeeData')  
   DROP TABLE auditEmployeeData;  
GO  
CREATE TABLE dbo.employeeData (  
   emp_id int NOT NULL PRIMARY KEY,  
   emp_bankAccountNumber char (10) NOT NULL,  
   emp_salary int NOT NULL,  
   emp_SSN char (11) NOT NULL,  
   emp_lname nchar (32) NOT NULL,  
   emp_fname nchar (32) NOT NULL,  
   emp_manager int NOT NULL  
   );  
GO  
CREATE TABLE dbo.auditEmployeeData (  
   audit_log_id uniqueidentifier DEFAULT NEWID() PRIMARY KEY,  
   audit_log_type char (3) NOT NULL,  
   audit_emp_id int NOT NULL,  
   audit_emp_bankAccountNumber char (10) NULL,  
   audit_emp_salary int NULL,  
   audit_emp_SSN char (11) NULL,  
   audit_user sysname DEFAULT SUSER_SNAME(),  
   audit_changed datetime DEFAULT GETDATE()  
   );  
GO  
CREATE TRIGGER dbo.updEmployeeData   
ON dbo.employeeData   
AFTER UPDATE AS  
/* Check whether columns 2, 3 or 4 have been updated. If any or all  
columns 2, 3 or 4 have been changed, create an audit record.
The bitmask is: power(2, (2-1)) + power(2, (3-1)) + power(2, (4-1)) = 14.
This bitmask translates into base_10 as: 2 + 4 + 8 = 14.
To test whether all columns 2, 3, and 4 are updated, use = 14 instead of > 0  
(below). */
  
   IF (COLUMNS_UPDATED() & 14) > 0  
/* Use IF (COLUMNS_UPDATED() & 14) = 14 to see whether all columns 2, 3,   
and 4 are updated. */  
      BEGIN  
-- Audit OLD record.  
      INSERT INTO dbo.auditEmployeeData  
         (audit_log_type,  
         audit_emp_id,  
         audit_emp_bankAccountNumber,  
         audit_emp_salary,  
         audit_emp_SSN)  
         SELECT 'OLD',   
            del.emp_id,  
            del.emp_bankAccountNumber,  
            del.emp_salary,  
            del.emp_SSN  
         FROM deleted del;  
  
-- Audit NEW record.  
      INSERT INTO dbo.auditEmployeeData  
         (audit_log_type,  
         audit_emp_id,  
         audit_emp_bankAccountNumber,  
         audit_emp_salary,  
         audit_emp_SSN)  
         SELECT 'NEW',  
            ins.emp_id,  
            ins.emp_bankAccountNumber,  
            ins.emp_salary,  
            ins.emp_SSN  
         FROM inserted ins;  
   END;  
GO  
  
/* Inserting a new employee does not cause the UPDATE trigger to fire. */  
INSERT INTO employeeData  
   VALUES ( 101, 'USA-987-01', 23000, 'R-M53550M', N'Mendel', N'Roland', 32);  
GO  
  
/* Updating the employee record for employee number 101 to change the   
salary to 51000 causes the UPDATE trigger to fire and an audit trail to   
be produced. */  
  
UPDATE dbo.employeeData  
   SET emp_salary = 51000  
   WHERE emp_id = 101;  
GO  
SELECT * FROM auditEmployeeData;  
GO  
  
/* Updating the employee record for employee number 101 to change both   
the bank account number and social security number (SSN) causes the   
UPDATE trigger to fire and an audit trail to be produced. */  
  
UPDATE dbo.employeeData  
   SET emp_bankAccountNumber = '133146A0', emp_SSN = 'R-M53550M'  
   WHERE emp_id = 101;  
GO  
SELECT * FROM dbo.auditEmployeeData;  
  
GO  
```  
  
### <a name="b-using-columns_updated-to-test-more-than-eight-columns"></a>B. COLUMNS_UPDATED を使用して、9 列以上をテストする  
最初の 8 つのテーブル列以外の列に影響を与える更新をテストするには、`SUBSTRING` 関数を使用して、`COLUMNS_UPDATED` から返された正しいビットをテストします。 この例では、`AdventureWorks2012.Person.Person` テーブルの列 `3`、`5`、および `9` に影響を与える更新をテストしています。
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Person.uContact2', N'TR') IS NOT NULL  
    DROP TRIGGER Person.uContact2;  
GO  
CREATE TRIGGER Person.uContact2 ON Person.Person  
AFTER UPDATE AS  
    IF ( (SUBSTRING(COLUMNS_UPDATED(), 1, 1) & 20 = 20)   
        AND (SUBSTRING(COLUMNS_UPDATED(), 2, 1) & 1 = 1) )   
    PRINT 'Columns 3, 5 and 9 updated';  
GO  
  
UPDATE Person.Person   
   SET NameStyle = NameStyle,  
      FirstName=FirstName,  
      EmailPromotion=EmailPromotion;  
GO  
```  
  
## <a name="see-also"></a>参照
[ビットごとの演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
[CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
[UPDATE&#40;&#41; &#40;Transact-SQL&#41;](../../t-sql/functions/update-trigger-functions-transact-sql.md)
  
  
