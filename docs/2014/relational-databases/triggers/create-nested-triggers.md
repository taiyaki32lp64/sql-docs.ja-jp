---
title: 入れ子になったトリガーの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- recursive DML triggers [SQL Server]
- DML triggers, nested
- triggers [SQL Server], nested
- direct recursion [SQL Server]
- triggers [SQL Server], recursive
- DML triggers, recursive
- RECURSIVE_TRIGGERS option
- indirect recursion [SQL Server]
- nested DML triggers
ms.assetid: cd522dda-b4ab-41b8-82b0-02445bdba7af
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ba5b5edf57bf877827fefe4f8764b8b71124a550
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68196538"
---
# <a name="create-nested-triggers"></a>入れ子になったトリガーの作成
  あるトリガーが別のトリガーを起動する操作を実行するときは、DML トリガーと DDL トリガーの両方が入れ子になります。 このような操作では、他のトリガーを順次開始できます。 DML トリガーと DDL トリガーは、32 レベルまで入れ子にできます。 **nested triggers** サーバー構成オプションにより、AFTER トリガーを入れ子にできるかどうかを制御できます。 INSTEAD OF トリガーは、このサーバー オプションの設定とは無関係に入れ子にできます。INSTEAD OF トリガーにできるのは DML トリガーだけです。  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] トリガーからマネージド コードへの参照は、32 レベルの入れ子制限の 1 レベルとしてカウントされます。 マネージド コード内から呼び出されたメソッドは、この制限としてはカウントされません。  
  
 トリガーを入れ子にできる場合に、トリガーのチェーンのどれかが無限ループを開始すると、入れ子階層の上限を超えることになり、トリガーは終了します。  
  
 入れ子になったトリガーを使用して、前のトリガーの影響を受けた行のバックアップ コピーを保存するなど、システムの運用上有益な機能を実行することができます。 たとえば、 `PurchaseOrderDetail` トリガーが削除した `PurchaseOrderDetail` 行のバックアップ コピーを保存するトリガーを `delcascadetrig` に作成することができます。 `delcascadetrig` トリガーが有効な場合、 `PurchaseOrderID` から `PurchaseOrderHeader` 1965 が削除されると、 `PurchaseOrderDetail`から対応する行が削除されます。 このデータを保存するには、 `PurchaseOrderDetail` に DELETE トリガーを作成します。このトリガーでは削除されたデータが、別に作成されたテーブル `del_save`に保存されます。 例:  
  
```  
CREATE TRIGGER Purchasing.savedel  
   ON Purchasing.PurchaseOrderDetail  
FOR DELETE  
AS  
   INSERT del_save;  
   SELECT * FROM deleted;  
```  
  
 入れ子の順序に依存するトリガーを使用することはお勧めしません。 個別のトリガーを使用し、順番にデータ修正を行ってください。  
  
> [!NOTE]  
>  トリガーはトランザクション内で実行されるので、入れ子になったトリガーのいずれかのレベルで障害が発生すると、トランザクション全体が取り消され、すべてのデータ修正がロールバックされます。 どこで障害が発生したかを判断できるように、トリガーに PRINT ステートメントを含めてください。  
  
## <a name="recursive-triggers"></a>再帰トリガー  
 RECURSIVE_TRIGGERS データベース オプションが ON になっている場合を除いて、AFTER トリガーが自分自身を再帰呼び出しすることはありません。  
  
 再帰には、次の 2 種類があります。  
  
-   直接再帰  
  
     起動されたトリガーによる処理が、同じトリガーを再び起動する場合にこの再帰が発生します。 たとえば、アプリケーションで **T3**テーブルが更新され、これにより **Trig3** トリガーが起動されたとします。 **Trig3** がテーブル **T3** を更新するトリガーだとすると、テーブルが再度更新され、 **Trig3** が再び起動されることになります。  
  
     別の種類 (AFTER または INSTEAD OF) のトリガーが呼び出された後で、同じトリガーが呼び出されても、直接再帰が発生します。 つまり、同じ INSTEAD OF トリガーが 2 回呼び出されると、その間に AFTER トリガーが 1 回以上呼び出されていたとしても、INSTEAD OF トリガーの直接再帰が発生します。 同様に、同じ AFTER トリガーが 2 回呼び出されると、その間に INSTEAD OF トリガーが 1 回以上呼び出されていたとしても、AFTER トリガーの直接再帰が発生します。 たとえば、アプリケーションがテーブル **T4**を更新します。 この更新により、INSTEAD OF トリガー **Trig4** が起動します。 **Trig4** はテーブル **T5**を更新します。 この更新により、AFTER トリガー **Trig5** が起動します。 **Trig5** がテーブル **T4**を更新し、これにより INSTEAD OF トリガー **Trig4** が再び起動されます。 このようなイベントの連鎖は、 **Trig4**に対する直接再帰と見なされます。  
  
-   間接再帰  
  
     起動されたトリガーが実行した処理によって、同じ種類 (AFTER または INSTEAD OF) の別のトリガーが起動する場合、この再帰が発生します。 この 2 番目のトリガーにより、最初のトリガーを再度起動する操作が実行されます。 つまり、ある INSTEAD OF トリガーが 2 回呼び出され、その間に別の INSTEAD OF トリガーが呼び出されていると、間接再帰が発生します。 同様に、ある AFTER トリガーが 2 回呼び出され、その間に別の AFTER トリガーが呼び出されていると、間接再帰が発生します。 たとえば、アプリケーションがテーブル **T1**を更新します。 この更新により、AFTER トリガー **Trig1** が起動します。 **Trig1** がテーブル **T2**を更新し、これにより AFTER トリガー **Trig2** が起動します。 次に、**Trig2** がテーブル **T1** を更新し、これにより AFTER トリガー **Trig1** が再び起動します。  
  
 RECURSIVE_TRIGGERS データベース オプションが OFF の場合は、AFTER トリガーの直接再帰呼び出しのみが回避されます。 AFTER トリガーの間接再帰を無効にするには、 **nested triggers** サーバー オプションを **0**に設定します。  
  
## <a name="examples"></a>使用例  
 次の例では、再帰トリガーを使用して、自己参照型リレーションシップ (トランジティブ クロージャとも呼ばれます) を解決する方法を示しています。 たとえば、 `emp_mgr` テーブルで、次のものが定義されているとします。  
  
-   会社内の従業員 (`emp`)  
  
-   各従業員の管理者 (`mgr`)  
  
-   各従業員へ報告を行う、組織構成内の従業員の総数 (`NoOfReports`)  
  
 再帰的な UPDATE トリガーを使用すると、新しい従業員のレコードが挿入されたときに `NoOfReports` 列を最新の状態に更新できます。 INSERT トリガーにより、その従業員の管理者のレコードの `NoOfReports` 列の値が更新されます。これにより組織構成の上部に向かって、その他のレコードの `NoOfReports` 列が再帰的に更新されます。  
  
```  
USE AdventureWorks2012;  
GO  
-- Turn recursive triggers ON in the database.  
ALTER DATABASE AdventureWorks2012  
   SET RECURSIVE_TRIGGERS ON;  
GO  
CREATE TABLE dbo.emp_mgr (  
   emp char(30) PRIMARY KEY,  
    mgr char(30) NULL FOREIGN KEY REFERENCES emp_mgr(emp),  
    NoOfReports int DEFAULT 0  
);  
GO  
CREATE TRIGGER dbo.emp_mgrins ON dbo.emp_mgr  
FOR INSERT  
AS  
DECLARE @e char(30), @m char(30);  
DECLARE c1 CURSOR FOR  
   SELECT emp_mgr.emp  
   FROM   emp_mgr, inserted  
   WHERE emp_mgr.emp = inserted.mgr;  
  
OPEN c1;  
FETCH NEXT FROM c1 INTO @e;  
WHILE @@fetch_status = 0  
BEGIN  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports + 1 -- Add 1 for newly  
   WHERE emp_mgr.emp = @e ;                           -- added employee.  
  
   FETCH NEXT FROM c1 INTO @e;  
END  
CLOSE c1;  
DEALLOCATE c1;  
GO  
-- This recursive UPDATE trigger works assuming:  
--   1. Only singleton updates on emp_mgr.  
--   2. No inserts in the middle of the org tree.  
CREATE TRIGGER dbo.emp_mgrupd ON dbo.emp_mgr FOR UPDATE  
AS  
IF UPDATE (mgr)  
BEGIN  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports + 1 -- Increment mgr's  
   FROM inserted                            -- (no. of reports) by  
   WHERE emp_mgr.emp = inserted.mgr;         -- 1 for the new report.  
  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports - 1 -- Decrement mgr's  
   FROM deleted                             -- (no. of reports) by 1  
   WHERE emp_mgr.emp = deleted.mgr;          -- for the new report.  
END  
GO  
-- Insert some test data rows.  
INSERT dbo.emp_mgr(emp, mgr) VALUES  
    ('Harry', NULL)  
    ,('Alice', 'Harry')  
    ,('Paul', 'Alice')  
    ,('Joe', 'Alice')  
    ,('Dave', 'Joe');  
GO  
SELECT emp,mgr,NoOfReports  
FROM dbo.emp_mgr;  
GO  
-- Change Dave's manager from Joe to Harry  
UPDATE dbo.emp_mgr SET mgr = 'Harry'  
WHERE emp = 'Dave';  
GO  
SELECT emp,mgr,NoOfReports FROM emp_mgr;  
  
GO  
```  
  
 以下は、更新を行う前の状態です。  
  
```  
emp                            mgr                           NoOfReports  
------------------------------ ----------------------------- -----------  
Alice                          Harry                          2  
Dave                           Joe                            0  
Harry                          NULL                           1  
Joe                            Alice                          1  
Paul                           Alice                          0  
```  
  
 以下は、更新を行った後の状態です。  
  
```  
emp                            mgr                           NoOfReports  
------------------------------ ----------------------------- -----------  
Alice                          Harry                          2  
Dave                           Harry                          0  
Harry                          NULL                           2  
Joe                            Alice                          0  
Paul                           Alice                          0  
```  
  
 **入れ子になったトリガーのオプションを設定するには**  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
 **RECURSIVE_TRIGGERS データベース オプションを設定するには**  
  
-   [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
## <a name="see-also"></a>関連項目  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [nested triggers サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md)  
  
  
