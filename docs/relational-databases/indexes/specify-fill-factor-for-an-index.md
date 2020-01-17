---
title: インデックスの FILL FACTOR の指定 | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- fill factor [SQL Server]
- page splits [SQL Server]
ms.assetid: 237a577e-b42b-4adb-90cf-aa7fb174f3ab
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4badf632e87404b0c3496564abec6ca9a56e3747
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909522"
---
# <a name="specify-fill-factor-for-an-index"></a>インデックスの FILL FACTOR の指定
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  このトピックでは、FILL FACTOR について説明すると共に、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して [!INCLUDE[tsql](../../includes/tsql-md.md)]のインデックスの FILL FACTOR 値を指定する方法について説明します。  
  
 FILL FACTOR オプションは、インデックス データ ストレージとパフォーマンスの微調整を行うために用意されています。 インデックスの作成または再構築を行うとき、各リーフ レベルのページのデータを格納する領域の割合が FILL FACTOR 値によって決まり、今後インデックスのサイズが大きくなる場合に備えて指定した各ページ上の残りの空き領域が予約されます。 たとえば、FILL FACTOR 値を 80 に指定すると、基になるテーブルにデータを追加したときにインデックスのサイズを拡張するための領域として、各リーフ レベルのページの 20% が空き領域として確保されます。 空き領域は、インデックスの最後ではなく、インデックス行の間に確保されます。  
  
 有効な FILL FACTOR 値は 1 ～ 100 (パーセント) です。サーバー全体の既定値は 0 で、これはリーフ レベルのページの全容量が使用されることを意味します。  
  
> [!NOTE]  
>  FILL FACTOR 値 0 と 100 の機能は、まったく同じです。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [パフォーマンスに関する考慮事項](#Performance)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用してインデックスの FILL FACTOR を指定するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Performance"></a> パフォーマンスに関する考慮事項  
  
#### <a name="page-splits"></a>ページ分割  
 適切な FILL FACTOR 値を選択すると、基になるテーブルにデータが追加されたときにインデックスのサイズを拡張するのに十分な領域が確保され、ページ分割が実行される可能性が低くなります。フル インデックス ページに新しい行を追加すると、新しい行を挿入する領域を確保するために、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] により行の約半分が新しいページに移動されます。 この再構成をページ分割といいます。 ページ分割により新しいレコード用の領域が確保されますが、この操作の実行には時間がかかることがあります。また、ページ分割はリソースを集中的に消費する操作です。 さらに、I/O 操作を増加させる断片化の原因となることもあります。 ページ分割が頻繁に行われる場合は、新規または既存の FILL FACTOR 値を使用してデータを再配布して、インデックスを再構築できます。 詳細については、「 [インデックスの再編成と再構築](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)」を参照してください。  
  
 FILL FACTOR 値を 0 以外の小さな値に設定すると、インデックスのサイズが大きくなったときにページを分割する必要性を減少させることができますが、さらに多くの保存領域が必要になり、読み取りのパフォーマンスが低下する場合があります。 挿入や更新が頻繁に実行されるアプリケーションでも、データベース読み取り回数はデータベース書き込み回数よりも 5 ～ 10 倍多くなるのが普通です。 したがって、既定値以外の FILL FACTOR 値を指定すると、FILL FACTOR の設定に反比例してデータベース読み取りのパフォーマンスが低下する可能性があります。 たとえば、FILL FACTOR 値を 50 に指定すると、データベース読み取りのパフォーマンスが 1/2 に低下することがあります。 インデックスに多くのページが含まれていて、データを取得するには、ディスク I/O 操作を増加させる必要があるため、読み取りのパフォーマンスが低下します。  
  
#### <a name="adding-data-to-the-end-of-the-table"></a>テーブルの最後へのデータの追加  
 新しいデータがテーブル全体に均等に分散される場合は、0 および 100 以外の FILL FACTOR を指定するとパフォーマンスが向上する可能性があります。 ただし、すべてのデータがテーブルの最後に追加されると、インデックス ページ内の空き領域は埋められません。 たとえば、インデックス キー列が IDENTITY 列であると、新しい行のキーが常に増加し、インデックス行はインデックスの最後に論理的に追加されます。 行のサイズを大きくするデータで既存の行が更新される場合は、FILL FACTOR 値を 100 未満にしてください。 各ページ上の追加のバイトにより、行の追加の長さによって発生するページ分割を最小限にすることができます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルまたはビューに対する ALTER 権限が必要です。 実行するには、 **sysadmin** 固定サーバー ロール、または **db_ddladmin** 固定データベース ロールおよび **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-specify-a-fill-factor-by-using-table-designer"></a>テーブル デザイナーを使用して FILL FACTOR を指定するには  
  
1.  オブジェクト エクスプローラーで、インデックスの FILL FACTOR を指定するテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  インデックスの FILL FACTOR を指定するテーブルを右クリックし、 **[デザイン]** を選択します。  
  
4.  **[テーブル デザイナー]** メニューの **[インデックス/キー]** をクリックします。  
  
5.  FILL FACTOR を指定するインデックスを選択します。  
  
6.  **[FILL の指定]** を展開し、 **[FILL FACTOR]** 行を選択し、目的の FILL FACTOR を行に入力します。  
  
7.  **[閉じる]** をクリックします。  
  
8.  **ファイル** メニューの **table_name**_を保存_を選びます。  
  
#### <a name="to-specify-a-fill-factor-in-an-index-by-using-object-explorer"></a>オブジェクト エクスプローラーを使用してインデックスの FILL FACTOR を指定するには  
  
1.  オブジェクト エクスプローラーで、インデックスの FILL FACTOR を指定するテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  プラス記号をクリックして、インデックスの FILL FACTOR を指定するテーブルを展開します。  
  
4.  プラス記号をクリックして **[インデックス]** フォルダーを展開します。  
  
5.  FILL FACTOR を指定するインデックスを右クリックし、 **[プロパティ]** を選択します。  
  
6.  **[ページの選択]** の **[オプション]** を選択します。  
  
7.  **[FILL FACTOR]** 行に、目的の FILL FACTOR を入力します。  
  
8.  **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-specify-a-fill-factor-in-an-existing-index"></a>既存のインデックスの FILL FACTOR を指定するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、既存のインデックスを再構築し、再構築処理中に指定された FILL FACTOR を適用します。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Rebuilds the IX_Employee_OrganizationLevel_OrganizationNode index   
    -- with a fill factor of 80 on the HumanResources.Employee table.  
  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    REBUILD WITH (FILLFACTOR = 80);   
    GO  
    ```  
  
#### <a name="another-way-to-specify-a-fill-factor-in-an-index"></a>別の方法でインデックスの FILL FACTOR を指定する  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    /* Drops and re-creates the IX_Employee_OrganizationLevel_OrganizationNode index on the HumanResources.Employee table with a fill factor of 80.  
    */  
  
    CREATE INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
       (OrganizationLevel, OrganizationNode)   
    WITH (DROP_EXISTING = ON, FILLFACTOR = 80);   
    GO  
    ```  
  
 詳細については、「[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)」を参照してください。  
  
  
