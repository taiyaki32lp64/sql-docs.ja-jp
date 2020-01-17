---
title: DML トリガーの作成 | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], DML triggers
- deferred name resolution, DML triggers
- WITH ENCRYPTION clause
- IF UPDATE
- SET statement, DML triggers
- DML triggers, programming
- testing column changes
- results [SQL Server], DML triggers
ms.assetid: b2b52258-642b-462e-8e0f-18c09d2eccf4
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ed3026ae450e50bcb2d9debf93c4b90eab3afad0
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72905534"
---
# <a name="create-dml-triggers"></a>DML トリガーの作成
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] および [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の CREATE TRIGGER ステートメントを使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)] DML トリガーを作成する方法について説明します。  
  
##  <a name="Top"></a> はじめに  
  
### <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 DML トリガーの作成に関する制限事項と制約事項の一覧については、「[CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)」を参照してください。  
  
###  <a name="Permissions"></a> Permissions  
 トリガーを作成するテーブルまたはビューに対する ALTER 権限が必要です。  
  
##  <a name="Procedures"></a> DML トリガーの作成方法  
 次のいずれかを使用します。  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** 、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース、 **[テーブル]** 、 **Purchasing.PurchaseOrderHeader**テーブルの順に展開します。  
  
3.  **[トリガー]** を右クリックし、 **[新しいトリガー]** をクリックします。  
  
4.  **[クエリ]** メニューの **[テンプレート パラメーターの値の指定]** をクリックします。 または、Ctrl キーと Shift キーを押しながら M キーを押して、 **[テンプレート パラメーターの値の指定]** ダイアログ ボックスを開きます。  
  
5.  **[テンプレート パラメーターの値の指定]** ダイアログ ボックスで、各パラメーターに次の値を入力します。  
  
    |パラメーター|[値]|  
    |---------------|-----------|  
    |Author|*名前*|  
    |Create Date|*今日の日付*|  
    |[説明]|ベンダーへの新しい購買発注の挿入を許可する前に、ベンダーの信用格付けを確認します。|  
    |Schema_Name|Purchasing|  
    |Trigger_Name|NewPODetail2|  
    |Table_Name|PurchaseOrderDetail|  
    |Data_Modification_Statement|一覧から UPDATE と DELETE を削除します。|  
  
6.  **[OK]** をクリックします。  
  
7.  **クエリ エディター**で、コメント `-- Insert statements for trigger here` を次のステートメントに置き換えます。  
  
    ```sql  
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
  
8.  構文が有効であることを検証するには、 **[クエリ]** メニューの **[解析]** をクリックします。 エラー メッセージが返された場合は、ステートメントと上記の情報を比較し、必要に応じて修正してからこの手順を繰り返します。  
  
9. DML トリガーを作成するには、 **[クエリ]** メニューの **[実行]** をクリックします。 DML トリガーがデータベース内のオブジェクトとして作成されます。  
  
10. オブジェクト エクスプローラーにリストされた DML トリガーを確認するには、 **[トリガー]** を右クリックして **[更新]** を選択します。  

 [はじめに](#Top)  
  
###  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[ファイル]** メニューの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例は、上と同じ DML トリガーを作成します。  
  
    ```sql  
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
  
 
  
