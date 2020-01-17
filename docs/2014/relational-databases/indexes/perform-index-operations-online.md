---
title: オンラインでのインデックス操作の実行 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index online operations [SQL Server]
- online index operations
- ONLINE option
ms.assetid: 1e43537c-bf67-4db3-9908-3cb45c6fdaa1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b9eceaff8ea7fee16eac3afef8bdc560d7fb1642
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63036216"
---
# <a name="perform-index-operations-online"></a>オンラインでのインデックス操作の実行
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、インデックスをオンラインで作成、再構築、または削除する方法について説明します。 ONLINE オプションにより、このようなインデックス操作中に、基になるテーブルやクラスター化インデックス データ、および関連付けられた任意の非クラスター化インデックスへの同時ユーザー アクセスが可能になります。 たとえば、あるユーザーがクラスター化インデックスを再構築している最中に、そのユーザーと他のユーザーが基になるデータの更新やクエリを続行できます。 クラスター化インデックスの構築や再構築などのデータ定義言語 (DDL) 操作をオフラインで実行するときは、これらの操作により、基になるデータや関連付けられたインデックスに排他ロックがかけられます。 このため、インデックス操作が完了するまで、基になるデータの変更やクエリを実行できません。  
  
> [!NOTE]  
>  オンラインでのインデックス操作は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションで使用できるわけではありません。 詳しくは「 [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」をご覧ください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **インデックスをオンラインで再構築するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   1 日 24 時間、週 7 日間、常時稼動のビジネス環境では、オンラインでのインデックス操作を実行することをお勧めします。このような環境では、インデックスの操作中に、ユーザーが同時に操作できることが必要不可欠です。  
  
-   次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで、ONLINE オプションを使用できます。  
  
    -   [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql)  
  
    -   [ALTER INDEX](/sql/t-sql/statements/alter-index-transact-sql)  
  
    -   [DROP INDEX](/sql/t-sql/statements/drop-index-transact-sql)  
  
    -   [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) (CLUSTERED インデックス オプションが指定されている UNIQUE 制約または PRIMARY KEY 制約を追加または削除するため)  
  
-   オンラインでのインデックスの作成、再構築、または削除に関する制限と制約については、「 [オンライン インデックス操作のガイドライン](guidelines-for-online-index-operations.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルまたはビューに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-rebuild-an-index-online"></a>インデックスをオンラインで再構築するには  
  
1.  オブジェクト エクスプローラーで、インデックスをオンラインで再構築するテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  **[テーブル]** フォルダーを展開します。  
  
3.  プラス記号をクリックして、オンラインでインデックスを再構築するテーブルを展開します。  
  
4.  **[インデックス]** フォルダーを展開します。  
  
5.  オンラインで再構築するインデックスを右クリックし、 **[プロパティ]** を選択します。  
  
6.  **[ページの選択]** の **[オプション]** を選択します。  
  
7.  **[DML のオンライン処理を許可する]** を選択し、一覧から **[True]** を選択します。  
  
8.  **[OK]** をクリックします。  
  
9. オンラインで再構築するインデックスを右クリックし、 **[再構築]** を選択します。  
  
10. **[インデックスの再構築]** ダイアログ ボックスで、 **[再構築するインデックス]** グリッドに目的のインデックスが表示されていることを確認し、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-rebuild-or-drop-an-index-online"></a>インデックスをオンラインで作成、再構築、または削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、既存のインデックスをオンラインで再構築します。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER INDEX AK_Employee_NationalIDNumber ON HumanResources.Employee  
    REBUILD WITH (ONLINE = ON);  
    GO  
    ```  
  
     次の例では、クラスター化インデックスをオンラインで削除し、 `NewGroup` 句を使用することで、結果のテーブル (ヒープ) をファイル グループ `MOVE TO` に移動します。 移動の前後で `sys.indexes`、 `sys.tables`、および `sys.filegroups` カタログ ビューを参照し、ファイル グループ内のインデックスとテーブルの配置を確認します。  
  
     [!code-sql[IndexDDL#DropIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/dropindex.sql#dropindex4)]  
  
 詳細については、「[ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)」を参照してください。  
  
  
