---
title: ビューを使用したデータ変更 | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8e41abc4ab3f798a3ee970061ddc21539403ef6b
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907510"
---
# <a name="modify-data-through-a-view"></a>ビューを使用したデータ変更
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、基になるデータベース テーブルのデータを変更できます。  
  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   「[CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)」の '更新可能なビュー' セクションを参照してください。  
  
  
###  <a name="Permissions"></a> Permissions  
 実行する操作に応じて、対象のテーブルに対する UPDATE 権限、INSERT 権限、または DELETE 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-modify-table-data-through-a-view"></a>ビューを介してテーブル データを変更するには  
  
1.  **オブジェクト エクスプローラー**で、ビューを含むデータベースを展開し、 **[ビュー]** を展開します。  
  
2.  ビューを右クリックし、 **[上位 200 行の編集]** を選択します。  
  
3.  場合により、変更対象の行を取得するために **SQL** ペインの SELECT ステートメントを変更する必要があります。  
  
4.  **結果** ペインで、変更または削除する行を見つけます。 行を削除するには、行を右クリックし、 **[削除]** を選択します。 1 つ以上の列のデータを変更するには、目的の列のデータを変更します。  
  
    > **重要!!** ビューが複数のベース テーブルを参照している場合は、行を削除できません。 1 つのベース テーブルに属している列のみを更新することができます。  
  
5.  行を挿入するには、行の最後までスクロールし、新しい値を挿入します。  

    > **重要:** ビューが複数のベース テーブルを参照している場合は、行を挿入できません。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-update-table-data-through-a-view"></a>ビューを介してテーブル データを更新するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
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
  
 詳細については、「[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)」を参照してください。  
  
#### <a name="to-insert-table-data-through-a-view"></a>ビューを介してテーブル データを挿入するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、ビュー `HumanResouces.Department` の該当する列を指定することによって、新しい行をベース テーブル `HumanResources.vEmployeeDepartmentHistory`に挿入します。 1 つのベース テーブルの列のみが指定され、ベース テーブルの他の列は既定値を持つため、このステートメントは成功します。  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    INSERT INTO HumanResources.vEmployeeDepartmentHistory (Department, GroupName)   
    VALUES ('MyDepartment', 'MyGroup');   
    GO  
    ```  
  
 詳細については、「[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)」を参照してください。  
  
  
