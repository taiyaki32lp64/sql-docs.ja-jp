---
title: クラスター化インデックスの作成 | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index creation [SQL Server], clustered indexes
- clustered indexes, creating
- clustered indexes, PRIMARY KEY constraint
- clustered indexes, UNIQUE constraint
- indexes [SQL Server], clustered
ms.assetid: 47148383-c2c7-4f08-a9e4-7016bf2d1d13
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 79ce697e86adcd7a2b11d4ec1d5f4564d51692e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024990"
---
# <a name="create-clustered-indexes"></a>クラスター化インデックスの作成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、テーブルにクラスター化インデックスを作成できます。 クラスター化インデックスは、いくつかの例外を除くすべてのテーブルに必要です。 クラスター化インデックスは、クエリ パフォーマンスを向上するだけではなく、必要に応じて再構築または再構成してテーブルの断片化を制御することができます。 また、クラスター化インデックスをビューに作成することもできます。 (クラスター化インデックスの定義は「 [クラスター化インデックスと非クラスター化インデックスの概念](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)」にあります。)  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [一般的な実装](#Implementations)  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **テーブルにクラスター化インデックスを作成するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Implementations"></a> 一般的な実装  
 クラスター化インデックスは、次のように実装されます。  
  
-   **PRIMARY KEY 制約と UNIQUE 制約**  
  
     PRIMARY KEY 制約を作成すると、テーブルにクラスター化インデックスが存在せず、一意の非クラスター化インデックスを指定しなかった場合、列に一意のクラスター化インデックスが自動的に作成されます。 主キー列には NULL 値を指定できません。  
  
     UNIQUE 制約を作成すると、既定では、一意な非クラスター化インデックスが作成され、UNIQUE 制約が適用されます。 テーブルにクラスター化インデックスが存在しない場合は、一意なクラスター化インデックスを指定できます。  
  
     制約の一部として作成されたインデックスには、自動的に制約名と同じ名前が指定されます。 詳細については、「 [Primary and Foreign Key Constraints](../../relational-databases/tables/primary-and-foreign-key-constraints.md) 」および「 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)」を参照してください。  
  
-   **制約に依存しないインデックス**  
  
     非クラスター化主キー制約が指定された場合、主キー列以外の列にクラスター化インデックスを作成できます。  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   クラスター化インデックスの構造を作成する場合、古い (作成元の) 構造と新しい (作成先の) 構造の両方を格納するディスク領域が、それぞれのファイルとファイル グループで必要になります。 古い構造の割り当ては、トランザクション全体がコミットされるまで解除されません。 並べ替え操作用に、余分な一時ディスク領域が必要になる場合もあります。 詳細については、「 [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)」をご参照ください。  
  
-   複数の非クラスター化インデックスが存在するヒープにクラスター化インデックスを作成する場合、すべての非クラスター化インデックスを再構築して、行識別子 (RID) の代わりにクラスター化キー値が含まれるようにする必要があります。 同様に、複数の非クラスター化インデックスを持つテーブルのクラスター化インデックスを削除すると、DROP 操作の一部として非クラスター化インデックスがすべて再構築されます。 大きなテーブルでは、この操作に相当な時間がかかる場合があります。  
  
     大きなテーブルにインデックスを構築する場合、最初にクラスター化インデックスを構築してから、非クラスター化インデックスを構築することをお勧めします。 既存のテーブルにインデックスを作成するときは、ONLINE オプションを ON に設定することを検討します。 ON に設定すると、テーブル ロックは長時間保持されません。 これにより、基になるテーブルに対するクエリまたは更新を続行できます。 詳しくは、「 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)」をご覧ください。  
  
-   クラスター化インデックスのインデックス キーには、ROW_OVERFLOW_DATA アロケーション ユニットに既存のデータを持つ **varchar** 列を含めることはできません。 クラスター化インデックスが **varchar** 列に作成され、既存のデータが IN_ROW_DATA アロケーション ユニットにある場合に、データを行外に押し出すような挿入処理や更新処理をその列に対して行うと失敗します。 行オーバーフロー データを含んでいる可能性のあるテーブルまたはインデックスに関する情報を取得するには、[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) 動的管理関数を使用します。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルまたはビューに対する ALTER 権限が必要です。 実行するには、 **sysadmin** 固定サーバー ロール、または **db_ddladmin** 固定データベース ロールおよび **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-clustered-index-by-using-object-explorer"></a>オブジェクト エクスプ ローラーを使用してクラスター化インデックスを作成するには  
  
1.  オブジェクト エクスプローラーで、クラスター化インデックスを作成するテーブルを展開します。  
  
2.  **[インデックス]** フォルダーを右クリックし、 **[新しいインデックス]** をポイントして、 **[クラスター化インデックス...]** を選択します。  
  
3.  **[新しいインデックス]** ダイアログ ボックスの **[全般]** ページで、 **[インデックス名]** ボックスに新しいインデックスの名前を入力します。  
  
4.  **[インデックス キー列]** で、 **[追加]** をクリックします。  
  
5.  _[table\_name_ **から列を選択]** ダイアログ ボックスで、クラスター化インデックスに追加するテーブル列のチェック ボックスをオンにします。  
  
6.  **[OK]** をクリックします。  
  
7.  **[新しいインデックス]** ダイアログ ボックスで、 **[OK]** をクリックします。  
  
#### <a name="to-create-a-clustered-index-by-using-the-table-designer"></a>テーブル デザイナーを使用してクラスター化インデックスを作成するには  
  
1.  オブジェクト エクスプローラーで、クラスター化インデックスを含むテーブルを作成するデータベースを展開します。  
  
2.  **[テーブル]** フォルダーを右クリックし、 **[新しいテーブル...]** をクリックします。  
  
3.  通常どおりに新しいテーブルを作成します。 詳しくは、「[テーブルの作成 &#40;データベース エンジン&#41;](../../relational-databases/tables/create-tables-database-engine.md)」を参照してください。  
  
4.  上の手順で作成した新しいテーブルを右クリックし、 **[デザイン]** をクリックします。  
  
5.  **[テーブル デザイナー]** メニューの **[インデックス/キー]** をクリックします。  
  
6.  **[インデックス/キー]** ダイアログ ボックスで、 **[追加]** をクリックします。  
  
7.  **[選択された主/一意キーまたはインデックス]** ボックスで、新しいインデックスを選択します。  
  
8.  グリッドで、 **[CLUSTERED として作成]** を選択し、プロパティ右のドロップダウン リストの **[はい]** を選択します。  
  
9. **[閉じる]** をクリックします。  
  
10. **[ファイル]** メニューの **[_table\_name_ の保存]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-clustered-index"></a>クラスター化インデックスを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Create a new table with three columns.  
    CREATE TABLE dbo.TestTable  
        (TestCol1 int NOT NULL,  
         TestCol2 nchar(10) NULL,  
         TestCol3 nvarchar(50) NULL);  
    GO  
    -- Create a clustered index called IX_TestTable_TestCol1  
    -- on the dbo.TestTable table using the TestCol1 column.  
    CREATE CLUSTERED INDEX IX_TestTable_TestCol1   
        ON dbo.TestTable (TestCol1);   
    GO  
    ```  
  
 詳細については、「[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [主キーの作成](../../relational-databases/tables/create-primary-keys.md)   
 [UNIQUE 制約の作成](../../relational-databases/tables/create-unique-constraints.md)  
  
  
