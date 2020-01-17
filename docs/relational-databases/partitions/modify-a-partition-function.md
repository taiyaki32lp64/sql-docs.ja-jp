---
title: パーティション関数の変更 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: ae5bfc09-f27a-4ea9-9518-485278b11674
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 62d3177a3fc8b0b88e3cd65e8675041be3250a3a
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907346"
---
# <a name="modify-a-partition-function"></a>パーティション関数の変更
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用してパーティション テーブルまたはパーティション インデックスのパーティション関数で、指定するパーティションの数を 1 つずつ増減させることにより、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でのテーブルまたはインデックスのパーティション分割方法を変更できます。 パーティションを追加するには、既存のパーティションを 2 つのパーティションに分割し、新しいパーティションの境界を再定義します。 パーティションを削除するには、2 つのパーティションの境界を 1 つのパーティションにマージします。 この最後の操作により、1 つのパーティションが再作成され、もう 1 つのパーティションは未割り当てのままになります。  
  
> [!CAUTION]  
>  複数のテーブルやインデックスで同じパーティション関数を使用できます。 パーティション関数を変更すると、1 回のトランザクションでそれらのテーブルやインデックスすべてに影響します。 パーティション関数を変更する場合は、事前にその依存関係を確認してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **次を使用してパーティション関数を変更するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   ALTER PARTITION FUNCTION は、1 つのパーティションを 2 つに分割するか、または 2 つのパーティションを 1 つにマージする目的にのみ使用できます。 テーブルまたはインデックスのパーティション分割方法を変更する (たとえば 10 個のパーティションから 5 個のパーティションに変更する) には、次のいずれかの方法を使用できます。  
  
    -   適切なパーティション関数でパーティション テーブルを新規作成し、INSERT INTO ...SELECT FROM [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントまたは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の**パーティションの管理ウィザード**で古いテーブルから新しいテーブルにデータを挿入します。  
  
    -   パーティション分割されたクラスター化インデックスを、ヒープ上に作成します。  
  
        > [!NOTE]  
        >  パーティション分割されたクラスター化インデックスを削除すると、パーティション分割されたヒープが生成されます。  
  
    -   [!INCLUDE[tsql](../../includes/tsql-md.md)] の CREATE INDEX ステートメントと DROP EXISTING = ON 句を使用して、既存のパーティション インデックスを削除および再構築します。  
  
    -   一連の ALTER PARTITION FUNCTION ステートメントを実行します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、パーティション関数の変更に関するレプリケーションはサポートされていません。 パブリケーション データベースのパーティション関数に変更を加える場合は、サブスクリプション データベースでこの操作を手動で実行する必要があります。  
  
-   ALTER PARTITION FUNCTION の影響を受けるすべてのファイル グループは、オンラインである必要があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 次の権限のいずれかを使用すると、ALTER PARTITION FUNCTION を実行できます。  
  
-   ALTER ANY DATASPACE 権限。 この権限は、既定では **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、および **db_ddladmin** 固定データベース ロールのメンバーに与えられています。  
  
-   パーティション関数が作成されたデータベースでの CONTROL または ALTER 権限。  
  
-   パーティション関数が作成されたデータベースのサーバーでの CONTROL SERVER または ALTER ANY DATABASE 権限。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **パーティション関数を変更するには:**  
  
 この操作は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]では実行できません。 パーティション関数を変更するには、最初にパーティション関数を削除し、パーティションの作成ウィザードを使用して必要なプロパティを持つ新しいパーティション関数を作成する必要があります。 詳細については、「  
  
#### <a name="to-delete-a-partition-function"></a>パーティション関数を削除するには  
  
1.  パーティション関数を削除するデータベースを展開し、 **ストレージ** フォルダーを展開します。  
  
2.  **パーティション関数** フォルダーを展開します。  
  
3.  削除するパーティション関数を右クリックして、 **[削除]** をクリックします。  
  
4.  **[オブジェクトの削除]** ダイアログ ボックスで、正しいパーティション関数が選択されていることを確認し、 **[OK]** をクリックします。  

##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-split-a-single-partition-into-two-partitions"></a>1 つのパーティションを 2 つのパーティションに分割するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- Look for a previous version of the partition function "myRangePF1" and deletes it if it is found.  
    IF EXISTS (SELECT * FROM sys.partition_functions  
        WHERE name = 'myRangePF1')  
        DROP PARTITION FUNCTION myRangePF1;  
    GO  
    -- Create a new partition function called "myRangePF1" that partitions a table into four partitions.  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
    GO  
    --Split the partition between boundary_values 100 and 1000  
    --to create two partitions between boundary_values 100 and 500  
    --and between boundary_values 500 and 1000.  
    ALTER PARTITION FUNCTION myRangePF1 ()  
    SPLIT RANGE (500);  
    ```  
  
#### <a name="to-merge-two-partitions-into-one-partition"></a>2 つのパーティションを 1 つのパーティションにマージするには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- Look for a previous version of the partition function "myRangePF1" and deletes it if it is found.  
    IF EXISTS (SELECT * FROM sys.partition_functions  
        WHERE name = 'myRangePF1')  
        DROP PARTITION FUNCTION myRangePF1;  
    GO  
    -- Create a new partition function called "myRangePF1" that partitions a table into four partitions.  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
    GO  
    --Merge the partitions between boundary_values 1 and 100  
    --and between boundary_values 100 and 1000 to create one partition  
    --between boundary_values 1 and 1000.  
    ALTER PARTITION FUNCTION myRangePF1 ()  
    MERGE RANGE (100);  
    ```  
  
 詳細については、「[ALTER PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)」を参照してください。  
  
  
