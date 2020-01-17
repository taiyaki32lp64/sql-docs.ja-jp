---
title: ビューを使用したデータ変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- data modifications [SQL Server], views
- views [SQL Server], modifying data through
- modifying data [SQL Server], views
ms.assetid: 410e2812-4ebe-48b2-b95f-c7784f1c4336
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5d87430c64bac133523d7001a88a894bb3985a5f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211676"
---
# <a name="modify-data-through-a-view"></a>ビューを使用したデータ変更
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、基になるデータベース テーブルのデータを変更できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **ビューを介してテーブル データを変更するを使用します。**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   「[CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql)」の '更新可能なビュー' セクションを参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 実行する操作に応じて、対象のテーブルに対する UPDATE 権限、INSERT 権限、または DELETE 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-modify-table-data-through-a-view"></a>ビューを介してテーブル データを変更するには  
  
1.  **オブジェクト エクスプローラー**で、ビューを含むデータベースを展開し、 **[ビュー]** を展開します。  
  
2.  ビューを右クリックし、 **[上位 200 行の編集]** を選択します。  
  
3.  場合により、変更対象の行を取得するために **SQL** ペインの SELECT ステートメントを変更する必要があります。  
  
4.  **結果** ペインで、変更または削除する行を見つけます。 行を削除するには、行を右クリックし、 **[削除]** を選択します。 1 つ以上の列のデータを変更するには、目的の列のデータを変更します。  
  
    > [!IMPORTANT]  
    >  ビューが複数のベース テーブルを参照している場合は、行を削除できません。 1 つのベース テーブルに属している列のみを更新することができます。  
  
5.  行を挿入するには、行の最後までスクロールし、新しい値を挿入します。  
  
    > [!IMPORTANT]  
    >  ビューが複数のベース テーブルを参照している場合は、行を挿入できません。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-update-table-data-through-a-view"></a>ビューを介してテーブル データを更新するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、ビュー `StartDate` の列を参照することによって特定の従業員の `EndDate` 列および `HumanResources.vEmployeeDepartmentHistory`列の値を変更します。 このビューは、2 つのテーブルの値を返します。 変更対象の列の所属先は 1 つのベース テーブルであるため、このステートメントは成功します。  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    UPDATE HumanResources.vEmployeeDepartmentHistory  
    SET StartDate = '20110203', EndDate = GETDATE()   
    WHERE LastName = N'Smith' AND FirstName = 'Samantha';   
    GO  
    ```  
  
 詳細については、「[UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)」を参照してください。  
  
#### <a name="to-insert-table-data-through-a-view"></a>ビューを介してテーブル データを挿入するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、ビュー `HumanResouces.Department` の該当する列を指定することによって、新しい行をベース テーブル `HumanResources.vEmployeeDepartmentHistory`に挿入します。 1 つのベース テーブルの列のみが指定され、ベース テーブルの他の列は既定値を持つため、このステートメントは成功します。  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    INSERT INTO HumanResources.vEmployeeDepartmentHistory (Department, GroupName)   
    VALUES ('MyDepartment', 'MyGroup');   
    GO  
    ```  
  
 詳細については、「[INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)」を参照してください。  
  
  
