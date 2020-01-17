---
title: インデックスと制約の無効化 | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql13.swb.disableindexes.f1
helpviewer_keywords:
- disabled indexes [SQL Server], index operations
- nonclustered indexes [SQL Server], disabling
- disabled indexes [SQL Server], guidelines
- clustered indexes, disabling
- constraints [SQL Server], disabling
- disabled indexes [SQL Server], viewing
- FOREIGN KEY constraints, disabling
- statistical information [SQL Server], indexes
- index disabling [SQL Server]
- indexed views [SQL Server], disabled indexes
ms.assetid: 2198f1af-fa44-47e9-92df-f4fde322ba18
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8e3fbbeed1224c6cd67c4292a6e263fb079d3ad5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107145"
---
# <a name="disable-indexes-and-constraints"></a>インデックスと制約の無効化
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、インデックスまたは制約を無効にする方法について説明します。 インデックスを無効にすると、ユーザーはそのインデックスにアクセスできなくなります。クラスター化インデックスの場合は、基になるテーブルのデータにもアクセスできなくなります。 ただし、インデックス定義はメタデータに残り、インデックス統計は非クラスター化インデックス上に保持されます。 ビュー上で非クラスター化インデックスまたはクラスター化インデックスを無効にすると、インデックス データが物理的に削除されます。 テーブルのクラスター化インデックスを無効にすると、データにアクセスできなくなります。つまり、データはテーブルに残りますが、そのインデックスを削除するか再構築するまでは、データ操作言語 (DML) 操作で使用できなくなります。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用してインデックスを無効化するには**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   無効なインデックスは保守されません。  
  
-   クエリ オプティマイザーは、クエリの実行プランの作成時に無効なインデックスを考慮しません。 また、無効化されたインデックスをテーブル ヒントで参照するクエリは失敗します。  
  
-   無効になっている既存のインデックスと同じ名前のインデックスを作成することはできません。  
  
-   無効化されたインデックスは削除できます。  
  
-   一意なインデックスを作成する場合、PRIMARY KEY 制約または UNIQUE 制約と、他のテーブルのインデックス付き列を参照するすべての FOREIGN KEY 制約も無効化されます。 クラスター化インデックスを無効にする場合、基になるテーブルを参照元または参照先とするすべての FOREIGN KEY 制約も無効になります。 インデックスを無効にすると、警告メッセージに制約名が表示されます。 インデックスを再構築した後で、ALTER TABLE CHECK CONSTRAINT ステートメントを使用してすべての制約を手動で有効にする必要があります。  
  
-   非クラスター化インデックスは、関連付けられたクラスター化インデックスを無効にすると自動的に無効になります。 非クラスター化インデックスを有効にするには、クラスター化インデックスを有効にする (テーブルまたはビューの場合) か、クラスター化インデックスを削除する (テーブルの場合) 必要があります。 ALTER INDEX ALL REBUILD ステートメントを使用してクラスター化インデックスを有効にした場合を除き、非クラスター化インデックスは明示的に有効にする必要があります。  
  
-   ALTER INDEX ALL REBUILD ステートメントを実行すると、ビューの無効化されたインデックスを除く、テーブル上の無効化されたインデックスがすべて再構築されて有効になります。 ビューのインデックスは、別の ALTER INDEX ALL REBUILD ステートメントで有効にする必要があります。  
  
-   テーブルのクラスター化インデックスを無効にすると、そのテーブルを参照しているビューのクラスター化インデックスおよび非クラスター化インデックスもすべて無効になります。 このようなインデックスは、参照先テーブルのインデックスと同時に再構築する必要があります。  
  
-   無効化されたクラスター化インデックスのデータ行には、クラスター化インデックスを削除または再構築する場合以外はアクセスできません。  
  
-   無効化された非クラスター化インデックスは、無効化されたクラスター化インデックスがテーブルに存在しなければオンラインで再構築できます。 ただし、ALTER INDEX REBUILD ステートメントまたは CREATE INDEX WITH DROP_EXISTING ステートメントのいずれかを使用している場合は常に、無効化されたクラスター化インデックスをオフラインで再構築する必要があります。 オンラインでのインデックス操作の詳細については、「 [オンラインでのインデックス操作の実行](../../relational-databases/indexes/perform-index-operations-online.md)」を参照してください。  
  
-   クラスター化インデックスが無効になっているテーブルに対して、CREATE STATISTICS ステートメントを正常に実行することはできません。  
  
-   インデックスが無効であり、次の条件に一致する場合、AUTO_CREATE_STATISTICS データベース オプションを指定することで列の新しい統計が作成されます。  
  
    -   AUTO_CREATE_STATISTICS が ON に設定されている  
  
    -   列の統計がまだ存在しない  
  
    -   クエリの最適化で統計が必要である  
  
-   クラスター化インデックスが無効になっている場合、 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) は基になるテーブルに関する情報を返すことができません。代わりに、クラスター化インデックスが無効であることが報告されます。 [DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md) を使用して、無効化されたインデックスの断片化を解消することはできません。このステートメントはエラー メッセージを出力して失敗します。 無効化されたインデックスの再構築には [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md) を使用できます。  
  
-   新しいクラスター化インデックスを作成すると、以前に無効化された非クラスター化インデックスが有効になります。 詳しくは、「 [Enable Indexes and Constraints](../../relational-databases/indexes/enable-indexes-and-constraints.md)」をご覧ください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 ALTER INDEX を実行するには、少なくとも、テーブルまたはビューの ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-disable-an-index"></a>インデックスを無効にするには  
  
1.  オブジェクト エクスプローラーで、インデックスを無効にするテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  プラス記号をクリックして、インデックスを無効にするテーブルを展開します。  
  
4.  プラス記号をクリックして **[インデックス]** フォルダーを展開します。  
  
5.  無効にするインデックスを右クリックし、 **[無効化]** を選択します。  
  
6.  **[インデックスの無効化]** ダイアログ ボックスで、 **[無効にするインデックス]** グリッドに目的のインデックスが表示されていることを確認し、 **[OK]** をクリックします。  
  
#### <a name="to-disable-all-indexes-on-a-table"></a>テーブルのすべてのインデックスを無効にするには  
  
1.  オブジェクト エクスプローラーで、インデックスを無効にするテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  プラス記号をクリックして、インデックスを無効にするテーブルを展開します。  
  
4.  **[インデックス]** フォルダーを右クリックし、 **[すべて無効にする]** を選択します。  
  
5.  **[インデックスの無効化]** ダイアログ ボックスで、 **[無効にするインデックス]** グリッドに目的のインデックスが表示されていることを確認し、 **[OK]** をクリックします。 **[無効にするインデックス]** グリッドからインデックスを削除するには、インデックスを選択し、Del キーを押します。  
  
 **[無効にするインデックス]** ダイアログ ボックスには、次の情報が表示されます。  
  
 **Index Name**  
 インデックスの名前を表示します。 実行中は、状態を表すアイコンもこの列に表示されます。  
  
 **テーブル名**  
 インデックスが作成されているテーブルまたはビューの名前を表示します。  
  
 **[インデックスの種類]**  
 インデックスの種類を表示します:**クラスター化**、**非クラスター化**、**空間**、または **XML**。  
  
 **ステータス**  
 無効化操作の状態を表示します。 実行後の値は、次のいずれかになります。  
  
-   空白  
  
     実行前の **[状態]** は空白です。  
  
-   **[実行中]**  
  
     インデックスの無効化操作が開始されましたが、まだ完了していません。  
  
-   **Success**  
  
     インデックスの無効化操作は正常に終了しました。  
  
-   **Error**  
  
     インデックスの無効化操作の実行中にエラーが発生したため、操作が正常に終了しませんでした。  
  
-   **停止**  
  
     インデックスの無効化操作はユーザーによって中止されたため、正常に終了しませんでした。  
  
 **メッセージ**  
 無効化操作中にエラー メッセージのテキストを表示します。 実行中、エラーはハイパーリンクとして表示されます。 エラーの内容は、ハイパーリンクのテキストに示されます。 多くの場合、 **[メッセージ]** 列が狭いためにメッセージ テキスト全体が表示されません。 テキスト全体を表示するには、次の 2 つの方法があります。  
  
-   マウス ポインターをメッセージ セル上に移動して、ツールヒントにエラー テキストが表示されるようにします。  
  
-   ハイパーリンクをクリックして、エラー全体を表示するダイアログ ボックスを開きます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-disable-an-index"></a>インデックスを無効にするには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- disables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    DISABLE;  
    ```  
  
#### <a name="to-disable-all-indexes-on-a-table"></a>テーブルのすべてのインデックスを無効にするには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Disables all indexes on the HumanResources.Employee table.  
    ALTER INDEX ALL ON HumanResources.Employee  
    DISABLE;  
    ```  
  
 詳細については、「[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)」を参照してください。  
  
  
