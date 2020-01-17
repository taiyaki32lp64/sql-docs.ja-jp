---
title: クラスター化インデックスの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 3cea4731ee665e401429679d764832247b2a2242
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63155373"
---
# <a name="create-clustered-indexes"></a>クラスター化インデックスの作成
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、テーブルにクラスター化インデックスを作成できます。 クラスター化インデックスは、いくつかの例外を除くすべてのテーブルに必要です。 クラスター化インデックスは、クエリ パフォーマンスを向上するだけではなく、必要に応じて再構築または再構成してテーブルの断片化を制御することができます。 また、クラスター化インデックスをビューに作成することもできます。 (クラスター化インデックスの定義は「 [クラスター化インデックスと非クラスター化インデックスの概念](clustered-and-nonclustered-indexes-described.md)」にあります。)  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [一般的な実装](#Implementations)  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **テーブルにクラスター化インデックスを作成するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Implementations"></a> 一般的な実装  
 クラスター化インデックスは、次のように実装されます。  
  
-   **PRIMARY KEY 制約と UNIQUE 制約**  
  
     PRIMARY KEY 制約を作成すると、テーブルにクラスター化インデックスが存在せず、一意の非クラスター化インデックスを指定しなかった場合、列に一意のクラスター化インデックスが自動的に作成されます。 主キー列には NULL 値を指定できません。  
  
     UNIQUE 制約を作成すると、既定では、一意な非クラスター化インデックスが作成され、UNIQUE 制約が適用されます。 テーブルにクラスター化インデックスが存在しない場合は、一意なクラスター化インデックスを指定できます。  
  
     制約の一部として作成されたインデックスには、自動的に制約名と同じ名前が指定されます。 詳細については、「 [Primary and Foreign Key Constraints](../tables/primary-and-foreign-key-constraints.md) 」および「 [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md)」を参照してください。  
  
-   **制約に依存しないインデックス**  
  
     非クラスター化主キー制約が指定された場合、主キー列以外の列にクラスター化インデックスを作成できます。  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   クラスター化インデックスの構造を作成する場合、古い (作成元の) 構造と新しい (作成先の) 構造の両方を格納するディスク領域が、それぞれのファイルとファイル グループで必要になります。 古い構造の割り当ては、トランザクション全体がコミットされるまで解除されません。 並べ替え操作用に、余分な一時ディスク領域が必要になる場合もあります。 詳細については、「 [Disk Space Requirements for Index DDL Operations](disk-space-requirements-for-index-ddl-operations.md)」をご参照ください。  
  
-   複数の非クラスター化インデックスが存在するヒープにクラスター化インデックスを作成する場合、すべての非クラスター化インデックスを再構築して、行識別子 (RID) の代わりにクラスター化キー値が含まれるようにする必要があります。 同様に、複数の非クラスター化インデックスを持つテーブルのクラスター化インデックスを削除すると、DROP 操作の一部として非クラスター化インデックスがすべて再構築されます。 大きなテーブルでは、この操作に相当な時間がかかる場合があります。  
  
     大きなテーブルにインデックスを構築する場合、最初にクラスター化インデックスを構築してから、非クラスター化インデックスを構築することをお勧めします。 既存のテーブルにインデックスを作成するときは、ONLINE オプションを ON に設定することを検討します。 ON に設定すると、テーブル ロックは長時間保持されません。 これにより、基になるテーブルに対するクエリまたは更新を続行できます。 詳しくは、「 [Perform Index Operations Online](perform-index-operations-online.md)」をご覧ください。  
  
-   クラスター化インデックスのインデックス キーには、ROW_OVERFLOW_DATA アロケーション ユニットに既存のデータを持つ `varchar` 列を含めることはできません。 クラスター化インデックスが `varchar` 列に作成され、その列の既存データが IN_ROW_DATA アロケーション ユニットにある場合、それ以後、既存データを行外に押し出すことになるような挿入や更新操作は失敗します。 行オーバーフロー データを含んでいる可能性のあるテーブルまたはインデックスに関する情報を取得するには、[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql) 動的管理関数を使用します。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルまたはビューに対する ALTER 権限が必要です。 実行するには、 **sysadmin** 固定サーバー ロール、または **db_ddladmin** 固定データベース ロールおよび **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-clustered-index-by-using-object-explorer"></a>オブジェクト エクスプ ローラーを使用してクラスター化インデックスを作成するには  
  
1.  オブジェクト エクスプローラーで、クラスター化インデックスを作成するテーブルを展開します。  
  
2.  **[インデックス]** フォルダーを右クリックし、 **[新しいインデックス]** をポイントして、 **[クラスター化インデックス...]** を選択します。  
  
3.  **[新しいインデックス]** ダイアログ ボックスの **[全般]** ページで、 **[インデックス名]** ボックスに新しいインデックスの名前を入力します。  
  
4.  **[インデックス キー列]** で、 **[追加]** をクリックします。  
  
5.  [_table_name_ **から列を選択**] ダイアログ ボックスで、クラスター化インデックスに追加するテーブル列のチェック ボックスをオンにします。  
  
6.  **[OK]** をクリックします。  
  
7.  **[新しいインデックス]** ダイアログ ボックスで、 **[OK]** をクリックします。  
  
#### <a name="to-create-a-clustered-index-by-using-the-table-designer"></a>テーブル デザイナーを使用してクラスター化インデックスを作成するには  
  
1.  オブジェクト エクスプローラーで、クラスター化インデックスを含むテーブルを作成するデータベースを展開します。  
  
2.  **[テーブル]** フォルダーを右クリックし、 **[新しいテーブル...]** をクリックします。  
  
3.  通常どおりに新しいテーブルを作成します。 詳しくは、「[テーブルの作成 &#40;データベース エンジン&#41;](../tables/create-tables-database-engine.md)」を参照してください。  
  
4.  上の手順で作成した新しいテーブルを右クリックし、 **[デザイン]** をクリックします。  
  
5.  **[テーブル デザイナー]** メニューの **[インデックス/キー]** をクリックします。  
  
6.  **[インデックス/キー]** ダイアログ ボックスで、 **[追加]** をクリックします。  
  
7.  **[選択された主/一意キーまたはインデックス]** ボックスで、新しいインデックスを選択します。  
  
8.  グリッドで、 **[CLUSTERED として作成]** を選択し、プロパティ右のドロップダウン リストの **[はい]** を選択します。  
  
9. **[閉じる]** をクリックします。  
  
10. **ファイル** メニューの **テーブル名**_の保存_をクリックします。  
  
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
  
 詳細については、「[CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [主キーの作成](../tables/create-primary-keys.md)   
 [UNIQUE 制約の作成](../tables/create-unique-constraints.md)  
  
  
