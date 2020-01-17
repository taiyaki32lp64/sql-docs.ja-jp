---
title: インデックス オプションの設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- ALLOW_ROW_LOCKS option
- SORT_IN_TEMPDB option
- DROP_EXISTING clause
- large data, indexes
- PAD_INDEX
- STATISTICS_NORECOMPUTE
- MAXDOP index option, setting
- index options [SQL Server]
- MAXDOP index option
- IGNORE_DUP_KEY option
- ALLOW_PAGE_LOCKS option
- ONLINE
ms.assetid: 7969af33-e94c-41f7-ab89-9d9a2747cd5c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 24587f27710381ac787fe8045029df681e401af5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63036208"
---
# <a name="set-index-options"></a>インデックス オプションの設定
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] におけるインデックスのプロパティを、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して変更する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **以下を使用してインデックスのプロパティを変更するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   ALTER INDEX ステートメントに SET 句を使用することによって、次の各オプションが直ちにインデックスに適用されます:ALLOW_PAGE_LOCKS、ALLOW_ROW_LOCKS、IGNORE_DUP_KEY、STATISTICS_NORECOMPUTE。  
  
-   ALTER INDEX REBUILD または CREATE INDEX WITH DROP_EXISTING を使用してインデックスを再構築するときは、次の各オプションを設定できます:PAD_INDEX、FILLFACTOR、SORT_IN_TEMPDB、IGNORE_DUP_KEY、STATISTICS_NORECOMPUTE、ONLINE、ALLOW_ROW_LOCKS、ALLOW_PAGE_LOCKS、MAXDOP、DROP_EXISTING (CREATE INDEX のみ)。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルまたはビューに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-modify-the-properties-of-an-index-in-table-designer"></a>インデックスのプロパティをテーブル デザイナーで変更するには  
  
1.  オブジェクト エクスプローラーで、インデックスのプロパティの変更対象となるテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  インデックスのプロパティを変更するテーブルを右クリックし、 **[デザイン]** を選択します。  
  
4.  **[テーブル デザイナー]** メニューの **[インデックス/キー]** をクリックします。  
  
5.  変更するインデックスを選択します。 対応するプロパティがメイン グリッドに表示されます。  
  
6.  該当するプロパティの設定を変更してインデックスをカスタマイズします。  
  
7.  **[閉じる]** をクリックします。  
  
8.  **[ファイル]** メニューの [ **table_name**_を保存_] を選びます。  
  
#### <a name="to-modify-the-properties-of-an-index-in-object-explorer"></a>インデックスのプロパティをオブジェクト エクスプローラーで変更するには  
  
1.  オブジェクト エクスプローラーで、インデックスのプロパティの変更対象となるテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  インデックスのプロパティを変更するテーブルのプラス記号をクリックして展開します。  
  
4.  プラス記号をクリックして **[インデックス]** フォルダーを展開します。  
  
5.  プロパティを変更するインデックスを右クリックし、 **[プロパティ]** を選択します。  
  
6.  **[ページの選択]** の **[オプション]** を選択します。  
  
7.  該当するプロパティの設定を変更してインデックスをカスタマイズします。  
  
8.  インデックス列の位置を追加、削除、または変更するには、 **インデックスのプロパティ -**  **全般** _全般_ ページをクリックします。 詳細については、「 [Index Properties F1 Help](index-properties-f1-help.md)」をご覧ください。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-see-the-properties-of-all-the-indexes-in-a-table"></a>テーブル内のすべてのインデックスのプロパティを表示するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT i.name AS index_name,   
        i.type_desc,   
        i.is_unique,   
        ds.type_desc AS filegroup_or_partition_scheme,   
        ds.name AS filegroup_or_partition_scheme_name,   
        i.ignore_dup_key,   
        i.is_primary_key,   
        i.is_unique_constraint,   
        i.fill_factor,   
        i.is_padded,   
        i.is_disabled,   
        i.allow_row_locks,   
        i.allow_page_locks,   
        i.has_filter,   
        i.filter_definition  
    FROM sys.indexes AS i  
       INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
    WHERE is_hypothetical = 0 AND i.index_id <> 0   
       AND i.object_id = OBJECT_ID('HumanResources.Employee');   
    GO  
  
    ```  
  
#### <a name="to-set-the-properties-of-an-index"></a>インデックスのプロパティを設定するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
     [!code-sql[IndexDDL#AlterIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex4)]  
  
     [!code-sql[IndexDDL#AlterIndex2](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex2)]  
  
 詳細については、「[ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)」を参照してください。  
  
  
