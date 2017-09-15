---
title: "CHECK 制約の作成 | Microsoft Docs"
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- table constraints [SQL Server]
- attaching check constraints
- columns [SQL Server], constraints
- constraints [SQL Server], check
- CHECK constraints, attaching
ms.assetid: b8756304-9454-4d39-996a-64516831b7df
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5a7d6d12e6a2673fd38c8c7341c4703dd7588501
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="create-check-constraints"></a>CHECK 制約の作成
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用してテーブルで CHECK 制約を作成して、1 つ以上の列に入力できるデータ値を指定します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [セキュリティ](#Security)  
  
-   **新しい CHECK 制約を作成する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> アクセス許可  
 テーブルに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-new-check-constraint"></a>新しい CHECK 制約を作成するには  
  
1.  **オブジェクト エクスプローラー**で、CHECK 制約を追加するテーブルを展開し、 **[制約]** を右クリックして、 **[新しい制約]**をクリックします。  
  
2.  **[CHECK 制約]** ダイアログ ボックスで、 **[式]** フィールドをクリックして、省略記号 **[...]**をクリックします。  
  
3.  **[CHECK 制約式]** ダイアログ ボックスで、CHECK 制約の SQL 式を入力します。 たとえば、 `SellEndDate` テーブルの `Product` 列への入力を `SellStartDate` 列の日付と同じか、それよりも後の日付の値または NULL 値に限定するには、次のように入力します。  
  
    ```  
    SellEndDate >= SellStartDate OR SellEndDate IS NULL  
    ```  
  
     また、 `zip` 列への入力を 5 桁の数値に限定するには、次のように入力します。  
  
    ```  
    zip LIKE '[0-9][0-9][0-9][0-9][0-9]'  
    ```  
  
    > [!NOTE]  
    >  数値以外の制約値は、必ず単一引用符 (') で囲んでください。  
  
4.  クリックして **OK**です。  
  
5.  **[ID]** カテゴリでは、CHECK 制約の名前を変更し、制約の説明 (拡張プロパティ) を追加できます。  
  
6.  **テーブル デザイナー** のカテゴリでは、制約が適用されるタイミングを設定できます。  
  
    |**目的:**|**[はい] を選択するフィールド:**|  
    |-------------|---------------------------------------------|  
    |制約を作成する前に既に存在していたデータで制約をテストする|**[作成または有効化するときに既存データを確認]**|  
    |このテーブルでレプリケーション操作が発生するたびに制約を適用する|**[レプリケーションに対して適用]**|  
    |このテーブルの行を挿入または更新するたびに制約を適用する|**[INSERT および UPDATE に適用]**|  
  
7.  **[閉じる]**をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-new-check-constraint"></a>新しい CHECK 制約を作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]**をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]**をクリックします。  
  
    ```  
    ALTER TABLE dbo.DocExc   
       ADD ColumnD int NULL   
       CONSTRAINT CHK_ColumnD_DocExc   
       CHECK (ColumnD > 10 AND ColumnD < 50);  
    GO  
    -- Adding values that will pass the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (49);  
    GO  
    -- Adding values that will fail the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (55);  
    GO  
  
    ```  
  
 詳細については、「[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)」を参照してください。  
  
###  <a name="TsqlExample"></a>  
