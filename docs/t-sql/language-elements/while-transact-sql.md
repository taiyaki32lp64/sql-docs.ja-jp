---
title: WHILE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WHILE_TSQL
- WHILE
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], repeated executions
- statement blocks [SQL Server]
- repeated statement executions
- nested WHILE loops
- WHILE keyword
ms.assetid: 52dd29ab-25d7-4fd3-a960-ac55c30c9ea9
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3ee098b61c233bb3012ab1505553873c30edd5d
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095879"
---
# <a name="while-transact-sql"></a>WHILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]


  SQL ステートメントまたはステートメント ブロックの実行を繰り返すための条件を設定します。 指定した条件が true の場合に限り、ステートメントは繰り返し実行します。 WHILE ループ内のステートメントの実行は、ループ内から BREAK キーワードおよび CONTINUE キーワードによって制御することができます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
WHILE Boolean_expression   
     { sql_statement | statement_block | BREAK | CONTINUE }  
  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
WHILE Boolean_expression   
     { sql_statement | statement_block | BREAK }  
  
```  
  
## <a name="arguments"></a>引数  
 *Boolean_expression*  
 **TRUE** または **FALSE** を返す[式](../../t-sql/language-elements/expressions-transact-sql.md)です。 ブール式が SELECT ステートメントを含む場合は、SELECT ステートメントをかっこで囲む必要があります。  
  
 {*sql_statement* | *statement_block*}  
 1 つの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、またはステートメント ブロックとして定義した一連のステートメントです。 ステートメント ブロックを定義するには、流れ制御キーワードの BEGIN と END を使用してください。  
  
 BREAK  
 最も内側の WHILE ループから抜けます。 ループの終了位置を示す END キーワード以降のすべてのステートメントが実行されます。  
  
 CONTINUE  
 CONTINUE キーワード以降のすべてのステートメントを無視し、WHILE ループを再開します。  
  
## <a name="remarks"></a>Remarks  
 2 つ以上の WHILE ループを入れ子にする場合、内側の BREAK が終了すると、1 つ外側のループに出ます。 まず、この内側ループの終了の後にあるステートメントがすべて実行され、次にこの外側のループの実行が再開されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-break-and-continue-with-nested-ifelse-and-while"></a>A. BREAK と CONTINUE を、入れ子にされた IF...ELSE および WHILE と組み合わせて使用する  
 次の例では、製品の平均表示価格が `$300` を下回る場合、`WHILE` ループが価格を倍にして、最高価格を選択します。 最高価格が `$500` 以下の場合は、`WHILE` ループが再開し、再び価格を倍にします。 このループは、最高価格が `$500` を超えるまで価格を倍増し続け、その後 `WHILE` ループから抜け出してメッセージを出力します。  
  
```  
USE AdventureWorks2012;  
GO  
WHILE (SELECT AVG(ListPrice) FROM Production.Product) < $300  
BEGIN  
   UPDATE Production.Product  
      SET ListPrice = ListPrice * 2  
   SELECT MAX(ListPrice) FROM Production.Product  
   IF (SELECT MAX(ListPrice) FROM Production.Product) > $500  
      BREAK  
   ELSE  
      CONTINUE  
END  
PRINT 'Too much for the market to bear';  
```  
  
### <a name="b-using-while-in-a-cursor"></a>B. カーソルで WHILE を使用する  
 次の例では、`@@FETCH_STATUS` を使用して `WHILE` ループ内のカーソルの動作を制御します。  
  
```  
DECLARE @EmployeeID as nvarchar(256)
DECLARE @Title as nvarchar(50)

DECLARE Employee_Cursor CURSOR FOR  
SELECT LoginID, JobTitle   
FROM AdventureWorks2012.HumanResources.Employee  
WHERE JobTitle = 'Marketing Specialist';  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor INTO @EmployeeID, @Title;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      Print '   ' + @EmployeeID + '      '+  @Title 
      FETCH NEXT FROM Employee_Cursor INTO @EmployeeID, @Title;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO 
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-simple-while-loop"></a>C: シンプルな While ループ  
 次の例では、製品の平均表示価格が `$300` を下回る場合、`WHILE` ループが価格を倍にして、最高価格を選択します。 最高価格が `$500` 以下の場合は、`WHILE` ループが再開し、再び価格を倍にします。 このループは、最高価格が `$500` を超えるまで価格を倍増し続け、その後 `WHILE` ループから抜け出します。  
  
```  
-- Uses AdventureWorks  
  
WHILE ( SELECT AVG(ListPrice) FROM dbo.DimProduct) < $300  
BEGIN  
    UPDATE dbo.DimProduct  
        SET ListPrice = ListPrice * 2;  
    SELECT MAX ( ListPrice) FROM dbo.DimProduct  
    IF ( SELECT MAX (ListPrice) FROM dbo.DimProduct) > $500  
        BREAK;  
END  
  
```  
  
## <a name="see-also"></a>参照  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [フロー制御言語 &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [カーソル &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  


