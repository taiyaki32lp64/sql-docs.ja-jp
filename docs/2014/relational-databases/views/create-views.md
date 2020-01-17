---
title: ビューの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], creating
ms.assetid: 0b7bd2a1-544c-42ba-8e7b-4822f34d7b64
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 27748ee6f4c70ebbcb4d1d28738130ddea07232b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211660"
---
# <a name="create-views"></a>ビューの作成
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、ビューを作成できます。 ビューは、次の目的で使用できます。  
  
-   各ユーザーのデータベースに対する認識を特化、簡素化、およびカスタマイズする。  
  
-   基になるベース テーブルに直接アクセスする権限をユーザーに与えずに、ユーザーがビューを介してデータにアクセスできるように設定することにより、セキュリティのメカニズムとして使用する。  
  
-   テーブルのスキーマが変更された場合に、そのテーブルをエミュレートするための後方互換性インターフェイスを提供する。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **以下を使用してビューを作成するには**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 ビューは現在のデータベースでのみ作成できます。  
  
 1 つのビューで保持できる列の数は最大 1,024 です。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースの CREATE VIEW 権限と、ビューが作成されているスキーマの ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-view-by-using-the-query-and-view-designer"></a>クエリおよびビュー デザイナーを使用してビューを作成するには  
  
1.  **オブジェクト エクスプローラー**で、新しいビューを作成するデータベースを展開します。  
  
2.  **[ビュー]** フォルダーを右クリックし、 **[新しいビュー]** をクリックします。  
  
3.  **[テーブルの追加]** ダイアログ ボックスで、新しいビューに含める 1 つまたは複数の要素を、[テーブル]、[ビュー]、[関数]、および [シノニム] のいずれかのタブから選択します。  
  
4.  **[追加]** をクリックし、 **[閉じる]** をクリックします。  
  
5.  **ダイアグラム ペイン**で、新しいビューに含める列またはその他の要素を選択します。  
  
6.  **抽出条件ペイン**で、列の追加の並べ替え条件またはフィルター条件を選択します。  
  
7.  **ファイル** メニューの **view name**_の保存_をクリックします。  
  
8.  **[名前の選択]** ダイアログ ボックスで、新しいビューの名前を入力し、 **[OK]** をクリックします。  
  
     クエリおよびビュー デザイナーの詳細については、「[クエリおよびビュー デザイナー &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)」を参照してください。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-view"></a>ビューを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    CREATE VIEW HumanResources.EmployeeHireDate  
    AS  
    SELECT p.FirstName, p.LastName, e.HireDate  
    FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
    ON e.BusinessEntityID = p.BusinessEntityID ;   
    GO  
    -- Query the view  
    SELECT FirstName, LastName, HireDate  
    FROM HumanResources.EmployeeHireDate  
    ORDER BY LastName;  
  
    ```  
  
 詳細については、「[CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql)」を参照してください。  
  
  
