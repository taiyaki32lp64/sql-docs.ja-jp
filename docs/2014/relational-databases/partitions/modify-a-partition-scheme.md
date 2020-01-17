---
title: パーティション構成の変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 515de63f-dfc5-434d-9adb-f3b5992f745a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 56148cca72ca9561219a9ea14025b0bd0f2204b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206568"
---
# <a name="modify-a-partition-scheme"></a>パーティション構成の変更
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、パーティション テーブルに追加される次のパーティションを保持するファイル グループを指定することにより、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でパーティション構成を変更できます。 この操作は、NEXT USED プロパティをファイル グループに割り当てることで実行できます。 NEXT USED プロパティは、空のファイル グループか、またはパーティションを既に保持しているファイル グループに割り当てることができます。 つまり、ファイル グループでは、複数のパーティションを保持することができます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **以下を使用してパーティション テーブルまたはパーティション インデックスを作成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 ALTER PARTITION SCHEME の対象となるファイル グループは、オンラインになっている必要があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 次の権限を使って ALTER PARTITION SCHEME を実行できます。  
  
-   ALTER ANY DATASPACE 権限。 この権限は、既定では **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、および **db_ddladmin** 固定データベース ロールのメンバーに与えられています。  
  
-   パーティション構成が作成されたデータベースに対する CONTROL または ALTER 権限。  
  
-   パーティション構成が作成されたデータベースのサーバーに対する CONTROL SERVER または ALTER ANY DATABASE 権限。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **パーティション構成を変更するには:**  
  
 この操作は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]では実行できません。 パーティション構成を変更するには、最初にパーティション構成を削除し、パーティションの作成ウィザードを使用して必要なプロパティを持つ新しいパーティション構成を作成する必要があります。 詳細については、次を参照してください。[パーティション分割されてテーブルの作成と SQL Server Management Studio のインデックスを使用して](create-partitioned-tables-and-indexes.md#SSMSProcedure)**作成 Partitioned Tables and Indexes**します。  
  
#### <a name="to-delete-a-partition-scheme"></a>パーティション構成を削除するには  
  
1.  プラス記号をクリックして、パーティション構成を削除するデータベースを展開します。  
  
2.  プラス記号をクリックして **[ストレージ]** フォルダーを展開します。  
  
3.  プラス記号をクリックして **[パーティション構成]** フォルダーを展開します。  
  
4.  削除するパーティション構成を右クリックして、 **[削除]** をクリックします。  
  
5.  **[オブジェクトの削除]** ダイアログ ボックスで、正しいパーティション構成が選択されていることを確認し、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-modify-a-partition-scheme"></a>パーティション構成を変更するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- add five new filegroups to the AdventureWorks2012 database  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test1fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test2fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test3fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test4fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test5fg;  
    GO  
    -- if the "myRangePF1" partition function and the "myRangePS1" partition scheme exist,  
    -- drop them from the AdventureWorks2012 database  
    IF EXISTS (SELECT * FROM sys.partition_functions  
        WHERE name = 'myRangePF1')  
    DROP PARTITION FUNCTION myRangePF1;  
    GO  
    IF EXISTS (SELECT * FROM sys.partition_schemes  
        WHERE name = 'myRangePS1')  
    DROP PARTITION SCHEME myRangePS1;  
    GO  
    -- create the new partition function "myRangePF1" with four partition groups  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
    GO  
    -- create the new partition scheme "myRangePS1"that will use   
    -- the "myRangePF1" partition function with five file groups.  
    -- The last filegroup, "test5fg," will be kept empty but marked  
    -- as the next used filegroup in the partition scheme.  
    CREATE PARTITION SCHEME myRangePS1  
    AS PARTITION myRangePF1  
    TO (test1fg, test2fg, test3fg, test4fg, test5fg);  
    GO  
    --Split "myRangePS1" between boundary_values 100 and 1000  
    --to create two partitions between boundary_values 100 and 500  
    --and between boundary_values 500 and 1000.  
    ALTER PARTITION FUNCTION myRangePF1 ()  
    SPLIT RANGE (500);  
    GO  
    -- Allow the "myRangePS1" partition scheme to use the filegroup "test5fg"  
    -- for the partition with boundary_values of 100 and 500  
    ALTER PARTITION SCHEME myRangePS1  
    NEXT USED test5fg;  
    GO  
    ```  
  
 詳細については、「[ALTER PARTITION SCHEME &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-partition-scheme-transact-sql)」を参照してください。  
  
  
