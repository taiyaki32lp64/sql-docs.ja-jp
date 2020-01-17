---
title: UNIQUE 制約の削除 | Microsoft Docs
ms.custom: ''
ms.date: 10/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- removing constraints
- UNIQUE constraints [SQL Server], deleting
- constraints [SQL Server], deleting
- deleting constraints
- constraints [SQL Server], unique
ms.assetid: 71e563fc-f5d7-4c2e-a42f-f0695a831f32
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e6790d66ad3a5f80a0964ada3c68311ef3d83b25
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016442"
---
# <a name="delete-unique-constraints"></a>UNIQUE 制約の削除
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して UNIQUE 制約を削除できます。 UNIQUE 制約を削除すると、制約式に含まれる 1 つ以上の列に入力される値に対する一意性の条件が取り除かれ、対応する一意なインデックスが削除されます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [セキュリティ](#Security)  
  
-   **UNIQUE 制約を削除する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-delete-a-unique-constraint-using-object-explorer"></a>オブジェクト エクスプローラーを使用して UNIQUE 制約を削除するには  
  
1.  オブジェクト エクスプローラーで、UNIQUE 制約を含むテーブルを展開し、 **[制約]** を展開します。  
  
2.  キーを右クリックし、 **[削除]** をクリックします。  
  
3.  **[オブジェクトの削除]** ダイアログ ボックスで正しいキーが指定されていることを確認し、 **[OK]** をクリックします。  
  
#### <a name="to-delete-a-unique-constraint-using-table-designer"></a>テーブル デザイナーを使用して UNIQUE 制約を削除するには  
  
1.  **オブジェクト エクスプローラー**で、UNIQUE 制約が設定されたテーブルを右クリックし、 **[デザイン]** をクリックします。  
  
2.  **[テーブル デザイナー]** メニューの **[インデックス/キー]** をクリックします。  
  
3.  **[インデックス/キー]** ダイアログ ボックスの **[Selected Primary/Unique Key and Index (選択された主/一意キーまたはインデックス)]** ボックスの一意キーをクリックします。  
  
4.  **[削除]** をクリックします。  
  
5.  **[ファイル]** メニューの **[<_テーブル名_> を保存]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-delete-a-unique-constraint"></a>UNIQUE 制約を削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- Return the name of unique constraint.  
    SELECT name  
    FROM sys.objects  
    WHERE type = 'UQ' AND OBJECT_NAME(parent_object_id) = N' DocExc';  
    GO  
    -- Delete the unique constraint.  
    ALTER TABLE dbo.DocExc   
    DROP CONSTRAINT UNQ_ColumnB_DocExc;  
    GO  
    ```  
  
 詳細については、「[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)」および「[sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)」を参照してください。  
  
###  <a name="TsqlExample"></a>  
