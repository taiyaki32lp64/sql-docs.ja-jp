---
title: インデックスの削除 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- removing indexes
- deleting indexes
- dropping indexes
- indexes [SQL Server], dropping
- index deletions [SQL Server]
ms.assetid: fd38a0ed-26c4-4c76-9ef7-e0a16147329d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 092d6e9432f22ef43a155d2a7d3ff03299bcd131
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162323"
---
# <a name="delete-an-index"></a>インデックスの削除
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、インデックスを削除する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **以下を使用してインデックスを削除するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 PRIMARY KEY 制約または UNIQUE 制約の結果として作成されたインデックスは、この方法を使用して削除することはできません。 このような場合には、制約を削除する必要があります。 制約および対応するインデックスを削除するには、 [から、](/sql/t-sql/statements/alter-table-transact-sql) ALTER TABLE [!INCLUDE[tsql](../../includes/tsql-md.md)]を DROP CONSTRAINT 句と共に使用します。 詳細については、「 [Delete Primary Keys](../tables/delete-primary-keys.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルまたはビューに対する ALTER 権限が必要です。 この権限は、固定サーバー ロール **sysadmin** と、固定データベース ロール **db_ddladmin** および **db_owner** に既定で許可されています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-delete-an-index-by-using-object-explorer"></a>オブジェクト エクスプローラーを使用してインデックスを削除するには  
  
1.  オブジェクト エクスプローラーで、インデックスを削除するテーブルが格納されているデータベースを展開します。  
  
2.  **[テーブル]** フォルダーを展開します。  
  
3.  削除するインデックスを含むテーブルを展開します。  
  
4.  **[インデックス]** フォルダーを展開します。  
  
5.  削除するインデックスを右クリックして、 **[削除]** をクリックします。  
  
6.  **[オブジェクトの削除]** ダイアログ ボックスで、 **[削除されるオブジェクト]** グリッドに目的のインデックスが表示されていることを確認し、 **[OK]** をクリックします。  
  
#### <a name="to-delete-an-index-using-table-designer"></a>テーブル デザイナーを使用してインデックスを削除するには  
  
1.  オブジェクト エクスプローラーで、インデックスを削除するテーブルが格納されているデータベースを展開します。  
  
2.  **[テーブル]** フォルダーを展開します。  
  
3.  削除するインデックスのあるテーブルを右クリックし、[デザイン] をクリックします。  
  
4.  **[テーブル デザイナー]** メニューの **[インデックス/キー]** をクリックします。  
  
5.  **[インデックス/キー]** ダイアログ ボックスで、削除するインデックスを選択します。  
  
6.  **[削除]** をクリックします。  
  
7.  **[閉じる]** をクリックします。  
  
8.  **[ファイル]** メニューの [ **table_name**_を保存_] を選びます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-delete-an-index"></a>インデックスを削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- delete the IX_ProductVendor_BusinessEntityID index  
    -- from the Purchasing.ProductVendor table  
    DROP INDEX IX_ProductVendor_BusinessEntityID   
        ON Purchasing.ProductVendor;  
    GO  
    ```  
  
 詳細については、「[DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)」を参照してください。  
  
  
