---
title: テーブル間での列のコピー (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- copying columns
- columns [SQL Server], copying
ms.assetid: 5f5e70dc-69f9-44b8-bc48-b5d51ac20d77
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 67df7c541b0c664f200f6cf77affc0c809dbc719
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62736355"
---
# <a name="copy-columns-from-one-table-to-another-database-engine"></a>テーブル間での列のコピー (データベース エンジン)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]で列の定義のみ、または定義とデータの両方をコピーすることで、あるテーブルから別のテーブルに列をコピーする方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **列をコピーする方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 別名データ型の列をデータベース間でコピーする場合、コピー先のデータベースで同じ別名データ型を使用できない場合があります。 その場合、コピー先データベースで使用できる基本データ型の中で最も近いデータ型がその列に割り当てられます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>テーブル間で列の定義をコピーするには  
  
1.  コピーする列を含むテーブルおよびコピー先のテーブルを右クリックして **[デザイン]** をクリックし、それらのテーブルを開きます。  
  
2.  コピーする列を含むテーブルのタブをクリックして、コピーする列を選択します。  
  
3.  **[編集]** メニューの **[コピー]** をクリックします。  
  
4.  列をコピーする先のテーブルのタブをクリックします。  
  
5.  コピーした列を挿入する列を選択し、 **[編集]** メニューの **[貼り付け]** をクリックします。  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>テーブル間でデータをコピーするには  
  
1.  前述の列定義のコピーの指示に従います。  
  
    > [!NOTE]  
    >  テーブル間でデータのコピーを始める前に、コピー先の列のデータ型が、コピー元の列のデータ型と互換性があることを確認してください。  
  
2.  オブジェクト エクスプローラーで、**[ビュー]** ノードを右クリックし、**[新しいビュー]** をクリックします。  
  
3.  **[クエリ デザイナー]** メニューの **[クエリ タイプの変更]** をポイントし、 **[結果の挿入]** をクリックします。  
  
4.  **[挿入先のテーブル選択]** ダイアログ ボックスで、データのコピー先のテーブルを選択し、 **[OK]** をクリックします。  
  
     同じテーブル内で行をコピーする場合は、コピー先テーブルと同じコピー元テーブルを追加します。  
  
    > [!NOTE]  
    >  **[クエリ デザイナー]** は、更新できるテーブルおよびビューを事前に判別できません。 そのため、 **[挿入先のテーブル選択]** ダイアログ ボックスのテーブルのボックスには、クエリを実行するデータ接続で使用できるテーブルおよびビューがすべて表示されます。行をコピーできないテーブルおよびビューも表示されます。  
  
5.  ダイアグラム ペインの本体を右クリックし、ショートカット メニューの **[テーブルの追加]** をクリックします。  
  
6.  **[テーブルの追加]** ダイアログ ボックスで、データのコピー元の各テーブルを選択し、 **[追加]** をクリックし、 **[閉じる]** をクリックします。  
  
     テーブルが省略形でダイアグラム ペインに表示されます。  
  
7.  省略形のテーブルで、データのコピー元の列のボックスをオンにします。  
  
8.  抽出条件ペインの **[追加]** 列で、各コピー先の列に対してデータのコピー元の列を選択します。  
  
9. 抽出条件ペインに検索条件を入力して、コピーする行を指定します。 詳細については、「[検索条件の指定 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)」を参照してください。  
  
     検索条件を指定しなかった場合は、コピー元テーブルのすべての行がコピー先テーブルにコピーされます。  
  
10. 集計情報をコピーする場合は、 **[グループ化]** を指定します。 詳細については、「[テーブルにあるすべての行の値の要約または集計 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-or-aggregate-values-for-all-rows-in-a-table-visual-database-tools.md)」を参照してください。  
  
11. **[SQL の実行]** ボタンをクリックしてクエリを実行します。  
  
     結果の挿入クエリを実行しても、 [結果ペイン](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)に結果は表示されません。 代わりに、コピーされた行数を示すメッセージが表示されます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>テーブル間で列の定義をコピーするには  
  
1.  Transact-SQL ステートメントを使用して、個々の列をあるテーブルから別の既存のテーブルにコピーすることはできません。 ただし、SELECT INTO を使用して、既定のファイル グループに新しいテーブルを作成し、クエリの結果得られた行をそのテーブルに挿入することができます。 詳細については、「[INTO 句 &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-into-clause-transact-sql)」を参照してください。  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>テーブル間でデータをコピーするには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE dbo.EmployeeSales  
    ( BusinessEntityID   varchar(11) NOT NULL,  
      SalesYTD money NOT NULL  
    );  
    GO  
    INSERT INTO dbo.EmployeeSales  
        SELECT BusinessEntityID, SalesYTD   
        FROM Sales.SalesPerson;  
    GO  
    ```  
  
  
