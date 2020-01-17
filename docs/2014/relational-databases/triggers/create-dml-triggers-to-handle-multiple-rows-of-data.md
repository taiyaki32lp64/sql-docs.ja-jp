---
title: 複数行のデータを処理するための DML トリガーの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- multiple row DML triggers
- UPDATE statement [SQL Server], DML triggers
- DELETE statement [SQL Server], DML triggers
- multirow DML triggers [SQL Server]
- INSERT statement [SQL Server], DML triggers
- DML triggers, multirow
ms.assetid: d476c124-596b-4b27-a883-812b6b50a735
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d960ae015bb2e52daa183e1f55d6ff119f234b18
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62676455"
---
# <a name="create-dml-triggers-to-handle-multiple-rows-of-data"></a>複数行のデータを処理するための DML トリガーの作成
  DML トリガーのコードを記述するときは、トリガーを起動するステートメントが、1 行だけではなく複数行のデータに影響する場合があることを考慮してください。 この動作は UPDATE トリガーや DELETE トリガーの場合によく見られます。UPDATE ステートメントや DELETE ステートメントが複数行に影響を与えることが多いためです。 INSERT トリガーの場合は、INSERT ステートメントが 1 行単位で追加を行うため、この動作はあまり見られません。 ただし、INSERT トリガーは INSERT INTO (*table_name*) SELECT ステートメントにより起動されることもあります。その場合は、1 回のトリガーの呼び出しで複数行が挿入される可能性があります。  
  
 複数行への影響について考慮することは、DML トリガーの機能によって 1 つのテーブルから自動的に集計値が再計算され、その結果を他のテーブルに保存して集計を続行するような場合は、特に重要です。  
  
> [!NOTE]  
>  パフォーマンスが低下する可能性があるので、トリガーにカーソルを使用することはお勧めしません。 複数行に影響を与えるトリガーを設計する場合は、カーソルではなく行セットをベースにしたロジックを使用してください。  
  
## <a name="examples"></a>使用例  
 次の例の DML トリガーはどれも、ある列の集計の途中経過を [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースの別のテーブル内に保存するように設計されています。  
  
### <a name="a-storing-a-running-total-for-a-single-row-insert"></a>A. 単一の行を挿入する場合の集計途中経過の格納  
 最初の例の DML トリガーは、 `PurchaseOrderDetail` テーブルに 1 行のデータが追加される場合、つまり 1 行単位の挿入は問題なく実行できます。 INSERT ステートメントにより DML トリガーが起動され、トリガーの実行中に **inserted** テーブルに新しい行が追加されます。 `UPDATE` ステートメントでは行の `LineTotal` 列の値が読み取られ、その値が `SubTotal` テーブルの `PurchaseOrderHeader` 列の既存の値に加算されます。 `WHERE` 句により、 `PurchaseOrderDetail` テーブルで更新された行が `PurchaseOrderID` inserted **テーブルの行の** に一致することが保証されます。  
  
```  
-- Trigger is valid for single-row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail  
ON Purchasing.PurchaseOrderDetail  
AFTER INSERT AS  
   UPDATE PurchaseOrderHeader  
   SET SubTotal = SubTotal + LineTotal  
   FROM inserted  
   WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID ;  
```  
  
### <a name="b-storing-a-running-total-for-a-multirow-or-single-row-insert"></a>B. 複数または単一の行を挿入する場合の集計途中経過の格納  
 複数行を挿入する場合は、例 A で示した DML トリガーは正しく実行されない可能性があります。UPDATE ステートメントの代入式の右側の式 (`SubTotal` + `LineTotal`) は必ず単一の値になり、値のリストを指定することはできません。 したがって、このトリガーの結果は、 **inserted** テーブル内の 1 行から値を取得して、その値を、特定の `SubTotal` 値に対する `PurchaseOrderHeader` テーブルの既存の `PurchaseOrderID` 値に追加することになります。 この操作では、1 つの `PurchaseOrderID` が **inserted** テーブルに複数登録されている場合には、予想どおりの結果が得られないことがあります。  
  
 `PurchaseOrderHeader` テーブルを正しく更新するには、 **inserted** テーブルに複数の行がある場合を考慮してトリガーを作成する必要があります。 これを行うには、 `SUM` ごとに `LineTotal` inserted **テーブル内の行グループで** の合計を計算する `PurchaseOrderID`関数を使用します。 `SUM` 関数は、相関サブクエリ (かっこ内の `SELECT` ステートメント) に指定します。 このサブクエリは、 `PurchaseOrderID` テーブルの **に一致するか、これと相関関係にある** inserted `PurchaseOrderID` テーブルの `PurchaseOrderHeader` の各値を返します。  
  
```  
-- Trigger is valid for multirow and single-row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail2  
ON Purchasing.PurchaseOrderDetail  
AFTER INSERT AS  
   UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal +   
      (SELECT SUM(LineTotal)  
      FROM inserted  
      WHERE PurchaseOrderHeader.PurchaseOrderID  
       = inserted.PurchaseOrderID)  
   WHERE PurchaseOrderHeader.PurchaseOrderID IN  
      (SELECT PurchaseOrderID FROM inserted);  
```  
  
 このトリガーは 1 行だけの挿入でも正しく実行されます。この場合、 `LineTotal` 値の列の合計は、1 つの行だけの値になります。 ただし、このトリガーでは、相関サブクエリと `IN` 句で使用されている `WHERE` 演算子のために、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]による追加の処理を必要とします。 これは、1 行単位の挿入操作の場合は必要ありません。  
  
### <a name="c-storing-a-running-total-based-on-the-type-of-insert"></a>C. 挿入の種類に基づいた集計の途中経過の格納  
 処理対象の行数に応じて最適の方法を使用するようにトリガーを変更できます。 たとえば、1 行だけの挿入と複数行の挿入を区別するには、トリガーのロジックで `@@ROWCOUNT` 関数を使用します。  
  
```  
-- Trigger valid for multirow and single row inserts  
-- and optimal for single row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail3  
ON Purchasing.PurchaseOrderDetail  
FOR INSERT AS  
IF @@ROWCOUNT = 1  
BEGIN  
   UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal + LineTotal  
   FROM inserted  
   WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
END  
ELSE  
BEGIN  
      UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal +   
      (SELECT SUM(LineTotal)  
      FROM inserted  
      WHERE PurchaseOrderHeader.PurchaseOrderID  
       = inserted.PurchaseOrderID)  
   WHERE PurchaseOrderHeader.PurchaseOrderID IN  
      (SELECT PurchaseOrderID FROM inserted)  
END;  
```  
  
## <a name="see-also"></a>参照  
 [DML トリガー](dml-triggers.md)  
  
  
