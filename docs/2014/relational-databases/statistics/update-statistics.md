---
title: 統計の更新 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- updating statistics
- statistics [SQL Server], updating
ms.assetid: 4b97c0b4-03ff-4cfb-9c3f-3b33290b7a2c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7c9a628f912f382f3ee8a87276aa34d0e54e37ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63033660"
---
# <a name="update-statistics"></a>統計の更新
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]のテーブルまたはインデックス付きビューについての、クエリの最適化に関する統計を更新します。 既定では、統計はクエリ プランを改善するためにクエリ オプティマイザーによって必要に応じて更新されますが、UPDATE STATISTICS またはストアド プロシージャ `sp_updatestats` を使用して既定の更新より頻繁に統計を更新することでクエリのパフォーマンスを向上させることができる場合もあります。  
  
 統計を更新すると、クエリが最新の統計を使用してコンパイルされるようになります。 ただし、統計の更新によりクエリが再コンパイルされます。 パフォーマンスの向上を目的とする場合、クエリ プランの改善とクエリの再コンパイルに要する時間の間にはトレードオフの関係があるため、あまり頻繁に統計を更新しないようにすることをお勧めします。 実際のトレードオフはアプリケーションによって異なります。 統計の更新では、tempdb を使用して、統計を作成するための行のサンプルを並べ替えます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **統計オブジェクトを更新するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 UPDATE STATISTICS を使用するか、または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で変更する場合は、テーブルまたはビューに対する ALTER 権限が必要です `sp_updatestats`を使用する場合は、 **sysadmin** 固定サーバー ロールのメンバーシップまたはデータベース (**dbo**) の所有権が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-update-a-statistics-object"></a>統計オブジェクトを更新するには  
  
1.  **オブジェクト エクスプローラー**で、統計を更新するデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  プラス記号をクリックして、統計を更新するテーブルを展開します。  
  
4.  プラス記号をクリックして **[統計]** フォルダーを展開します。  
  
5.  更新する統計オブジェクトを右クリックし、 **[プロパティ]** を選択します。  
  
6.  **統計のプロパティ -** _statistics_name_ダイアログ ボックスで、**これらの列の統計を更新**チェック ボックスをオンにして **[ok]** .  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-update-a-specific-statistics-object"></a>特定の統計オブジェクトを更新するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- The following example updates the statistics for the AK_SalesOrderDetail_rowguid index of the SalesOrderDetail table.   
    UPDATE STATISTICS Sales.SalesOrderDetail AK_SalesOrderDetail_rowguid;   
    GO  
    ```  
  
#### <a name="to-update-all-statistics-in-a-table"></a>テーブルのすべての統計を更新するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- The following example updates the statistics for all indexes on the SalesOrderDetail table.   
    UPDATE STATISTICS Sales.SalesOrderDetail;   
    GO  
    ```  
  
 詳細については、「[UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql)」を参照してください。  
  
#### <a name="to-update-all-statistics-in-a-database"></a>データベースのすべての統計を更新するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- The following example updates the statistics for all tables in the database.   
    EXEC sp_updatestats;  
    ```  
  
 詳細については、「[sp_updatestats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)」を参照してください。  
  
  
