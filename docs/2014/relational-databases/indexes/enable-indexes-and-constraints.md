---
title: インデックスと制約の有効化 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexes [SQL Server], enabling
- nonclustered indexes [SQL Server], enabling a disabled index
- index enabling [SQL Server]
- disabled indexes [SQL Server], how to enable
- constraints [SQL Server], enabling
- clustered indexes, enabling disabled indexes
ms.assetid: c55c8865-322e-4ab0-ba04-ea1f56735353
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7d68f329aecdd1284bac311db4139470bba55e41
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162384"
---
# <a name="enable-indexes-and-constraints"></a>インデックスと制約の有効化
  このトピックでは、無効にされている [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインデックスを、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して有効にする方法を説明します。 無効にされたインデックスは、再構築されるか削除されるまで無効な状態のままとなります。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **以下を使用して無効なインデックスを有効にするには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   インデックスの再構築後、インデックスを無効にしたために無効になった制約を手動で有効にする必要があります。 PRIMARY KEY 制約と UNIQUE 制約については、関連するインデックスを再構築すると有効になります。 このインデックスを再構築しないと、PRIMARY KEY 制約や UNIQUE 制約を参照する FOREIGN KEY 制約を有効にすることはできません。 FOREIGN KEY 制約を有効にするには、ALTER TABLE CHECK CONSTRAINT ステートメントを使用します。  
  
-   ONLINE オプションが ON に設定されている場合、無効化されたクラスター化インデックスを再構築することはできません。  
  
-   クラスター化インデックスが無効または有効で、非クラスター化インデックスが無効になっている場合、クラスター化インデックスの操作により、無効化された非クラスター化インデックスには、次のような影響があります。  
  
    |クラスター化インデックスの操作|無効化された非クラスター化インデックス|  
    |----------------------------|-----------------------------------|  
    |ALTER INDEX REBUILD|無効化されたままです。|  
    |ALTER INDEX ALL REBUILD|再構築され、有効になります。|  
    |DROP INDEX|無効化されたままです。|  
    |CREATE INDEX WITH DROP_EXISTING|無効化されたままです。|  
  
     新しいクラスター化インデックスの作成操作による影響は ALTER INDEX ALL REBUILD と同じです。  
  
-   クラスター化インデックスに関連付けられらている非クラスター化インデックスに対して実行できる操作は、これらのインデックスの状態が無効であるか有効であるかによって異なります。 次の表に、非クラスター化インデックスに対して実行できる操作を示します。  
  
    |非クラスター化インデックスの操作|クラスター化インデックスと非クラスター化インデックスの両方が無効な場合|クラスター化インデックスが有効で、非クラスター化インデックスが無効または有効な場合|  
    |-------------------------------|--------------------------------------------------------------------|----------------------------------------------------------------------------------------|  
    |ALTER INDEX REBUILD|操作は失敗します。|操作は成功します。|  
    |DROP INDEX|操作は成功します。|操作は成功します。|  
    |CREATE INDEX WITH DROP_EXISTING|操作は失敗します。|操作は成功します。|  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルまたはビューに対する ALTER 権限が必要です。 DBCC DBREINDEX を使用している場合、ユーザーはテーブルを所有しているか、 **sysadmin** 固定サーバー ロールのメンバーであるか、 **db_ddladmin** 固定データベース ロールおよび **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-enable-a-disabled-index"></a>無効なインデックスを有効にするには  
  
1.  オブジェクト エクスプローラーで、インデックスを有効にするテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  プラス記号をクリックして、インデックスを有効にするテーブルを展開します。  
  
4.  プラス記号をクリックして **[インデックス]** フォルダーを展開します。  
  
5.  有効にするインデックスを右クリックし、 **[再構築]** を選択します。  
  
6.  **[インデックスの再構築]** ダイアログ ボックスで、 **[再構築するインデックス]** グリッドに目的のインデックスが表示されていることを確認し、 **[OK]** をクリックします。  
  
#### <a name="to-enable-all-indexes-on-a-table"></a>テーブルのすべてのインデックスを有効にするには  
  
1.  オブジェクト エクスプローラーで、インデックスを有効にするテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  プラス記号をクリックして、インデックスを有効にするテーブルを展開します。  
  
4.  **[インデックス]** フォルダーを右クリックし、 **[すべて再構築]** を選択します。  
  
5.  **[インデックスの再構築]** ダイアログ ボックスで、 **[再構築するインデックス]** グリッドに目的のインデックスが表示されていることを確認し、 **[OK]** をクリックします。 **[再構築するインデックス]** グリッドからインデックスを削除するには、インデックスを選択し、Del キーを押します。  
  
 **[インデックスの再構築]** ダイアログ ボックスには、次の情報が表示されます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-enable-a-disabled-index-using-alter-index"></a>無効にされたインデックスを ALTER INDEX を使用して有効にするには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Enables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table.  
  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    REBUILD;   
    GO  
    ```  
  
#### <a name="to-enable-a-disabled-index-using-create-index"></a>無効にされたインデックスを CREATE INDEX を使用して有効にするには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- re-creates the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    -- using the OrganizationLevel and OrganizationNode columns  
    -- and then deletes the existing IX_Employee_OrganizationLevel_OrganizationNode index  
    CREATE INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
       (OrganizationLevel, OrganizationNode)  
    WITH (DROP_EXISTING = ON);  
    GO  
    ```  
  
#### <a name="to-enable-a-disabled-index-using-dbcc-dbreindex"></a>無効にされたインデックスを DBCC DBREINDEX を使用して有効にするには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- enables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    DBCC DBREINDEX ("HumanResources.Employee", IX_Employee_OrganizationLevel_OrganizationNode);  
    GO  
    ```  
  
#### <a name="to-enable-all-indexes-on-a-table-using-alter-index"></a>テーブル上のすべてのインデックスを ALTER INDEX を使用して有効にするには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- enables all indexes  
    -- on the HumanResources.Employee table  
    ALTER INDEX ALL ON HumanResources.Employee  
    REBUILD;  
    GO  
    ```  
  
#### <a name="to-enable-all-indexes-on-a-table-using-dbcc-dbreindex"></a>テーブル上のすべてのインデックスを DBCC DBREINDEX を使用して有効にするには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- enables all indexes  
    -- on the HumanResources.Employee table  
    DBCC DBREINDEX ("HumanResources.Employee", " ");  
    GO  
    ```  
  
 詳細については、「[ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)」、「[CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)」、および「[DBCC DBREINDEX &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dbreindex-transact-sql)」を参照してください。  
  
  
